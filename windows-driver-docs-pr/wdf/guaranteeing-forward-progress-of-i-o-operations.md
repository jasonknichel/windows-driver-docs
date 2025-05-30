---
title: Guaranteeing Forward Progress of I/O Operations
description: Guaranteeing Forward Progress of I/O Operations
keywords:
- guaranteed forward progress WDK KMDF
- forward progress, guaranteed WDK KMDF
- low-memory situations WDK KMDF
- I/O queues WDK KMDF , guaranteed forward progress
ms.date: 02/19/2025
ms.topic: how-to
---

# Guaranteeing Forward Progress of I/O Operations


To avoid losing critical system data, some drivers, such as storage drivers for the system's paging device, must perform at least some of their supported I/O operations without failure. One potential cause of a driver failure is a low-memory situation. If the framework or the driver can't allocate enough memory to handle an I/O request, they might have to fail the I/O request by [completing](completing-i-o-requests.md) it with an error status value.

In versions of KMDF prior to version 1.9, the framework always fails an I/O request if it can't allocate a framework request object for an I/O request packet (IRP) that the I/o manager sent to the driver. To provide drivers the ability to process I/O requests during low-memory situations, versions 1.9 and later of the framework provide a *guaranteed forward progress* capability for I/O queues.

This capability enables the framework and the driver to preallocate memory for sets of request objects and request-related driver context buffers, respectively. The framework and driver use this preallocated memory only when the amount of system memory is low.

### Features of Guaranteed Forward Progress

By using the framework's guaranteed forward progress for I/O queues, a driver can:

-   Ask the framework to preallocate a set of request objects to use with a specific I/O queue during low-memory situations.

-   Provide a callback function that preallocates request-specific resources that the driver can use when it receives preallocated request objects from the framework during low-memory situations.

-   Provide another callback function that allocates driver-specific resources for an I/O request when a low-memory situation hasn't been detected. If this callback function's allocation fails because of a low-memory situation, it can indicate whether the framework should use one of its preallocated request objects.

-   Specify which I/O requests require the use of preallocated request objects. Options include using preallocated objects for all IRPs, using them only if a paging I/O operation is in progress, or having an extra driver callback function examine each IRP to determine whether to use a preallocated object.

If your driver implements guaranteed forward progress for one or more of its I/O queues, it can better [process I/O requests](processing-i-o-requests.md) during low-memory situations. You can implement guaranteed forward progress for a device's default I/O queue, and for any I/O queue that your driver configures by calling [**WdfDeviceConfigureRequestDispatching**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching).

The framework's guaranteed forward progress capability works for your driver only if both your driver and the driver's [I/O targets](./introduction-to-i-o-targets.md) implement guaranteed forward progress. In other words, if a driver implements guaranteed forward progress for a device, all lower-level drivers in the device's driver stack must also implement guaranteed forward progress.

### Enabling Guaranteed Forward Progress for an I/O Queue

To enable guaranteed forward progress for an I/O queue, your driver initializes a [**WDF\_IO\_QUEUE\_FORWARD\_PROGRESS\_POLICY**](/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_forward_progress_policy) structure and then calls the [**WdfIoQueueAssignForwardProgressPolicy**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy) method. If the driver calls [**WdfDeviceConfigureRequestDispatching**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching) to configure an I/O queue, it must do so before it calls **WdfIoQueueAssignForwardProgressPolicy**.

When the driver calls [**WdfIoQueueAssignForwardProgressPolicy**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy), it can specify the following three event callback functions, all of which are optional:

<a href="" id="evtioallocateresourcesforreservedrequest"></a>[*EvtIoAllocateResourcesForReservedRequest*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request)  
A driver's [*EvtIoAllocateResourcesForReservedRequest*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request) callback function allocates and stores request-specific resources for request objects that the framework reserves for low-memory situations.

The framework calls this callback function each time it creates a reserved request object. The driver should allocate request-specific resources for one I/O request, typically by using the reserved request object's [context space](framework-object-context-space.md).

<a href="" id="evtioallocaterequestresources"></a>[*EvtIoAllocateRequestResources*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources)  
A driver's [*EvtIoAllocateRequestResources*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources) callback function allocates request-specific resources for immediate use. It's called immediately after the framework receives an IRP and creates a request object for the IRP.

If the callback function's attempt to allocate resources fails, it returns an error status value. The framework deletes the newly created request object and uses one of its reserved request objects. In turn, the driver's [request handler](request-handlers.md) uses request-specific resources that its [*EvtIoAllocateRequestResources*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources) callback function previously allocated.

<a href="" id="evtiowdmirpforforwardprogress"></a>[*EvtIoWdmIrpForForwardProgress*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_wdm_irp_for_forward_progress)
A driver's [*EvtIoWdmIrpForForwardProgress*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_wdm_irp_for_forward_progress) callback function examines an IRP and tells the framework whether to use a reserved request object for the IRP or to fail the I/O request by completing it with an error status value.

The framework calls this callback function only if it can't create a new request object and you indicated (by setting a flag in the driver's [**WDF\_IO\_QUEUE\_FORWARD\_PROGRESS\_POLICY**](/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_forward_progress_policy) structure) that you want the driver to examine IRPs during low-memory situations. In other words, your driver can assess each IRP and decide if it must process it even during low-memory situations.

When your driver calls [**WdfIoQueueAssignForwardProgressPolicy**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy), it also specifies the number of reserved request objects for the framework to preallocate for low-memory situations. Choose the number of request objects that are appropriate for your device and driver. To prevent reduced performance, your driver should typically specify a number that approximates the number of I/O requests that the driver and device can handle in parallel.

However, if your driver's call to [**WdfIoQueueAssignForwardProgressPolicy**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy) and its [*EvtIoAllocateResourcesForReservedRequest*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request) callback function preallocate too many reserved request objects or too much request-specific resource memory, your driver can contribute to the low-memory situations that you're trying to handle. To determine the best numbers to choose, test the performance of your driver and device, and include low-memory simulations.

Before [**WdfIoQueueAssignForwardProgressPolicy**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy) returns, the framework creates and reserves the number of request objects that the driver specified. Each time that it reserves a request object, the framework immediately calls the driver's [*EvtIoAllocateResourcesForReservedRequest*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request) callback function. The driver can use this callback function to allocate and save request-specific resources, in case the framework actually uses the reserved request objects.

When one of the driver's [request handlers](request-handlers.md) receives an I/O request from the I/O queue, it can call the [**WdfRequestIsReserved**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestisreserved) method to determine whether the framework preallocated the request object for low-memory situations. If this method returns **TRUE**, the driver should use resources that its [*EvtIoAllocateResourcesForReservedRequest*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request) callback function reserved.

If the framework uses one of its reserved request objects, it returns the object to its set of reserved objects after the driver completes the request. The framework saves the request object and any context space that the driver created by calling [**WdfDeviceInitSetRequestAttributes**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes) or [**WdfObjectAllocateContext**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectallocatecontext), for reuse if another low-memory situation occurs.

### How the Framework and Driver Support Guaranteed Forward Progress

The following steps describe how the driver and framework support guaranteed forward progress for an I/O queue:

1.  The driver calls [**WdfIoQueueAssignForwardProgressPolicy**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy).

    In response, the framework allocates and stores the number of request objects that the driver specifies. If the driver previously called [**WdfDeviceInitSetRequestAttributes**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes), each allocation includes context space that **WdfDeviceInitSetRequestAttributes** specified.

    If the driver provided an [*EvtIoAllocateResourcesForReservedRequest*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request) callback function, the framework calls the callback function each time that it allocates and stores a request object.

2.  The framework receives an I/O request packet (IRP) that the I/O manager is sending to the driver.

    The framework attempts to allocate a request object for the IRP. If the I/O queue that the driver created for the request type supports guaranteed forward progress, the next step depends on whether the allocation succeeds or fails:

    -   The request object allocation succeeds.

        If the driver provided an [*EvtIoAllocateRequestResources*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources) callback function, the framework calls it. If the callback function returns `STATUS_SUCCESS`, the framework adds the request to the I/O queue. If the callback function returns an error status value, the framework deletes the request object that it just created and uses one of its preallocated request objects. When the driver's request handler receives the request object, it determines whether the request object was preallocated and therefore whether it should use the driver's preallocated resources.

        If the driver didn't provide an [*EvtIoAllocateRequestResources*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources) callback function, the framework adds the request to the I/O queue, just as if the driver didn't enable guaranteed forward progress.

    -   The request object allocation fails.

        What the framework does next depends on the value that the driver provided for the **ForwardProgressReservedPolicy** member of the [**WDF\_IO\_QUEUE\_FORWARD\_PROGRESS\_POLICY**](/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_forward_progress_policy) structure. This member informs the framework when to use a reserved request: always, only if the I/O request is a paging I/O operation, or only if the [*EvtIoWdmIrpForForwardProgress*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_wdm_irp_for_forward_progress) callback function indicates that a reserved request should be used.

    In all cases, the driver's request handlers can call [**WdfRequestIsReserved**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestisreserved) to determine whether the framework used a reserved request object. If the framework used a reserved request object, the driver should use the request resources that its [*EvtIoAllocateResourcesForReservedRequest*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request) callback function allocated.

### Guaranteed Forward Progress Scenario

You're writing a driver for a storage device that might contain the system's paging file. It's important that read and write operations to the paging file succeed.

To achieve this goal, you decide to create separate I/O queues for read and write operations and to enable guaranteed forward progress for both of these I/O queues. You also decide to create a third I/O queue for all other request types without enabling guaranteed forward progress.

Your driver stack and device can process four write operations in parallel, so you set the **TotalForwardProgressRequests** member of the [**WDF\_IO\_QUEUE\_FORWARD\_PROGRESS\_POLICY**](/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_forward_progress_policy) structure to 4 before calling [**WdfIoQueueAssignForwardProgressPolicy**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueassignforwardprogresspolicy).

You decide that guaranteeing forward progress is only important if your driver's device is the paging device, so your driver sets the **ForwardProgressReservedPolicy** member of the WDF\_IO\_QUEUE\_FORWARD\_PROGRESS\_POLICY structure to [**WdfIoForwardProgressReservedPolicyPagingIO**](/windows-hardware/drivers/ddi/wdfio/ne-wdfio-_wdf_io_forward_progress_reserved_policy).

Because your driver requires a framework memory object for each read and write request, you decide that your driver should preallocate some memory objects to use for its calls to [**WdfIoTargetFormatRequestForRead**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforread) and [**WdfIoTargetFormatRequestForWrite**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforwrite) in low-memory situations.

Therefore, the driver provides an [*EvtIoAllocateResourcesForReservedRequest*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request) callback function for the read queue and another one for the write queue. Each time that the framework calls one of these callback functions, the callback function calls [**WdfMemoryCreate**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate) and saves the returned object handle for low-memory situations. Because the callback function receives a handle to a preallocated request object, it can parent the memory object to the request object. (A driver for a DMA device might also preallocate [framework DMA objects](framework-dma-objects.md).)

The [request handlers](request-handlers.md) for the read and write queues must determine whether each received request object is one that the framework reserved for low-memory situations. A request handler can call [**WdfRequestIsReserved**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestisreserved), or it can compare the request object handle with the ones that the [*EvtIoAllocateResourcesForReservedRequest*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_resources_for_reserved_request) callback function received previously.

The driver also provides an [*EvtIoAllocateRequestResources*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_allocate_request_resources) callback function for the read queue and another one for the write queue. The framework calls one of these callback functions when it receives a read or write request from the I/O manager and successfully creates a request object. Each of these callback functions calls [**WdfMemoryCreate**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate) to allocate a memory object for a request. If the allocation fails, the callback function returns an error status value to notify the framework that a low-memory situation has occurred. The framework, detecting the error return value, deletes the request object that it just created and uses one of its preallocated objects.

This driver doesn't provide an [*EvtIoWdmIrpForForwardProgress*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_wdm_irp_for_forward_progress) callback function, because it doesn't need to examine individual read or write IRPs before the framework adds them to an I/O queue.

When a driver implements guaranteed forward progress for a device, all lower-level drivers in the device's driver stack must also implement guaranteed forward progress.
