---
title: Loading and Unloading a Minifilter
description: Describes how minifilter drivers are loaded and unloaded.
keywords:
- filter manager WDK file system minifilter , loading/unloading drivers
- minifilter drivers WDK , driver loading
- file system minifilter drivers WDK , driver loading
- driver loading WDK file system
- loading drivers WDK file system
- unloading drivers
ms.date: 12/18/2024
ms.topic: concept-article
---

# Loading and unloading a minifilter

This article explains how file system minifilter drivers (minifilters) can be dynamically loaded and unloaded in a Windows environment. It covers the initialization and registration process, instance management, and the teardown procedures for ensuring proper cleanup and resource management during driver unload operations.

## Loading a minifilter

A minifilter is loaded according to existing [load order group definitions](load-order-groups-and-altitudes-for-minifilter-drivers.md) if the minifilter's [INF file](creating-an-inf-file-for-a-minifilter-driver.md) specifies a driver start type of SERVICE_BOOT_START, SERVICE_SYSTEM_START, or SERVICE_AUTO_START. This loading order supports interoperability with [legacy filter drivers](/previous-versions/windows/drivers/ifs/about-file-system-legacy-filter-drivers).

A minifilter can be loaded at any time while the system is running. It can be loaded in the following ways.

* Through a service start request (```sc start```, ```net start```, or the service APIs).

* Through an explicit load request (```fltmc load```, [**FltLoadFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltloadfilter), or [**FilterLoad**](/windows/win32/api/fltuser/nf-fltuser-filterload)).

The Filter Manager (*FltMgr*) calls the minifilter's [**DriverEntry**](writing-a-driverentry-routine-for-a-minifilter-driver.md) routine once the driver is loaded. At this time, the minifilter can perform initialization that will apply to all of its instances. Within its **DriverEntry** routine, the minifilter calls the following *FltMgr* routines:

* [**FltRegisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter) to register callback routines with *FltMgr*.
* [**FltStartFiltering**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering) to notify *FltMgr* that it's ready to start attaching to volumes and filtering I/O requests.

Minifilter driver instances are defined in the [INF file](creating-an-inf-file-for-a-minifilter-driver.md) used to install the minifilter. A minifilter's INF file must define a default instance. It can also define more instances beyond the default. These instance definitions apply across all volumes, and include the following information:

* The instance name
* Its altitude
* Flags that indicate whether the instance can be attached automatically, manually, or both.

The default instance is used:

* To order minifilters so that *FltMgr* calls the minifilter's mount and instance setup callback routines in the correct order.
* With explicit attachment requests when the caller doesn't specify an instance name.

*FltMgr* automatically notifies a minifilter about an available volume by calling its [*InstanceSetupCallback*](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_setup_callback) routine on the first create operation after the volume is mounted. This call can occur:

* Before [**FltStartFiltering**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering) returns, when *FltMgr* enumerates existing volumes at system startup.

* During runtime, when a volume is mounted or as a result of an explicit attachment request (```fltmc attach```, [**FltAttachVolume**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltattachvolume), or [**FilterAttach**](/windows/win32/api/fltuser/nf-fltuser-filterattach)).

## Unloading a minifilter

A minifilter instance is torn down when:

* The minifilter is unloaded.

* The volume that the minifilter instance is attached to is being dismounted.

* An explicit detach request is made (```fltmc detach```, [**FltDetachVolume**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdetachvolume), or [**FilterDetach**](/windows/win32/api/fltuser/nf-fltuser-filterdetach)). If the minifilter registers an [*InstanceQueryTeardownCallback*](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_query_teardown_callback) routine, it can fail an explicit detach request by calling **FilterDetach** or **FltDetachVolume**.

The teardown proceeds as follows:

* If the minifilter registered an [*InstanceTeardownStartCallback*](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback) callback routine, *FltMgr* calls it at the beginning of the teardown process. In this routine, the minifilter should:

  * Complete all pending operations.
  * Cancel or complete other work such as I/O requests generated by the minifilter.
  * Stop queuing new work items.

* During instance teardown:

  * Any currently executing preoperation or postoperation callback routines continue normal processing.
  * Any I/O request that is waiting for a postoperation callback can be "drained" or canceled.
  * Any I/O requests generated by the minifilter continue normal processing until they're complete.

* If the minifilter registered an [*InstanceTeardownCompleteCallback*](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback) routine, *FltMgr* calls this routine after all outstanding I/O operations are completed. In this routine, the minifilter closes any files that are still open.

* After all outstanding references to the instance are released, *FltMgr* deletes remaining contexts and the instance is completely torn down.

A minifilter can be unloaded in the following ways while the system is running:

* Through a service stop request (sc stop, net stop, or the service APIs).

* Through an explicit unload request (```fltmc unload```, [**FltUnloadFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunloadfilter), or [**FilterUnload**](/windows/win32/api/fltuser/nf-fltuser-filterunload)). The minifilter will be unloaded regardless of any dependencies registered to the service control manager (SCM).

A minifilter's [*FilterUnloadCallback*](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback) routine is called when the minifilter is unloaded. This routine closes any open communication server ports, calls [**FltUnregisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunregisterfilter), and performs any needed cleanup. Registering this routine is optional. However, if the minifilter doesn't register a *FilterUnloadCallback* routine, the minifilter can't be unloaded. For more information about this routine, see [Writing a FilterUnloadCallback Routine](writing-a-filterunloadcallback-routine.md).

## Filter Manager Routines for Loading and Unloading minifilters

*FltMgr* provides the following support routines for explicit load and unload requests, which can be issued from user mode or kernel mode:

* [**FilterLoad**](/windows/win32/api/fltuser/nf-fltuser-filterload)

* [**FilterUnload**](/windows/win32/api/fltuser/nf-fltuser-filterunload)

* [**FltLoadFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltloadfilter)

* [**FltUnloadFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunloadfilter)

The following routines are used to register and unregister callback routines for the setup and teardown of a minifilter instance:

* [**FltRegisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)

* [**FltStartFiltering**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering)

* [**FltUnregisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunregisterfilter)

## Minifilter Driver Callback Routines for Instance Setup, Teardown, and Unload

The following minifilter driver callback routines are stored as members of the [**FLT_REGISTRATION**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration) structure that is passed as a parameter to [**FltRegisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter):

| Callback Routine Member Name | Callback Routine Type |
| --------------------- | --------------------- |
| **InstanceSetupCallback** | [PFLT_INSTANCE_SETUP_CALLBACK](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_setup_callback) |
| **InstanceQueryTeardownCallback** | [PFLT_INSTANCE_QUERY_TEARDOWN_CALLBACK](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_query_teardown_callback) |
| **InstanceTeardownStartCallback** | [PFLT_INSTANCE_TEARDOWN_CALLBACK](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback) |
| **InstanceTeardownCompleteCallback** | [PFLT_INSTANCE_TEARDOWN_CALLBACK](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback) |
| **FilterUnloadCallback** | [PFLT_FILTER_UNLOAD_CALLBACK](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)

