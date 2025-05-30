---
title: Overview of Virtual Machine Multiple Queues (VMMQ)
description: Learn how virtual machine multiple queues extends Native RSS to a Hyper-V virtual environment.
ms.date: 12/19/2024
ms:custom: UpdateFrequency3
ms.topic: concept-article
---

# Overview of virtual machine multiple queues (VMMQ)

Virtual machine multiple queues (VMMQ) is a NIC offload technology that extends [Native Receive side scaling (RSSv1)](introduction-to-receive-side-scaling.md) to a [Hyper-V](overview-of-hyper-v.md) virtual environment.

VMMQ provides scalable network traffic processing for [virtual ports (VPorts)](virtual-ports--vports-.md) in the parent partition of a virtualized node. A VPort represents an internal port on the NIC switch of a network adapter that supports [single root I/O virtualization (SR-IOV)](overview-of-single-root-i-o-virtualization--sr-iov-.md). For an overview of the SR-IOV interface and its components, see [SR-IOV Architecture](sr-iov-architecture.md). Previously, RSS processing wasn't available for VPorts. VMMQ extends the native RSS feature to VPorts that are associated with the physical function (PF) of a NIC, including the default VPort.

VMMQ works by efficiently distributing network traffic within the NIC hardware. You can assign multiple hardware queues from the NIC to a single PF VPort. The NIC distributes network traffic across these queues using RSS hashing, placing packets directly onto the assigned processor. Offloading traffic distribution to the NIC improves CPU performance because the software doesn't have to complete this task.

You might want to enable the VMMQ feature to reduce the host CPU consumption and enable higher throughput to the virtual system by spreading the CPU load across multiple processors. You can add VMMQ support to new or existing NDIS 6.60 and later drivers. If an adapter supports VMMQ, the driver is vendor-supplied, and if the OS is Windows Server 2019, then VMMQ is enabled by default. If the adapter doesn’t support VMMQ, the driver is system-supplied, or if the OS is Windows Server 2016, then VMMQ is disabled by default or not available. If the OS is earlier than Windows Server 2016, then VMMQ isn't available.

VMMQ is available for the VPorts exposed in the parent partition regardless of whether the NIC is operating in [SR-IOV](overview-of-single-root-i-o-virtualization--sr-iov-.md) or [Virtual Machine Queue (VMQ)](virtual-machine-queue-architecture.md) mode.

## Expected feature interactions

- [Network Virtualization using Generic Routing Encapsulation (NVGRE)](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md) and [Virtual Extensive Local Area Network (VXLAN)](https://www.rfc-editor.org/info/rfc7348): The NIC calculates the hash for spreading receive queues based on the inner headers of the packets.

- [SR-IOV](overview-of-single-root-i-o-virtualization--sr-iov-.md): The NIC can support VMMQ and SR-IOV simultaneously.

## Related content

- [VMMQ send and receive processing](vmmq-send-and-receive-processing.md)
- [Advertising VMMQ capabilities](advertising-vmmq-capabilities.md)
- [Standardized INF keywords for VMMQ](standardized-inf-keywords-for-vmmq.md)
- [Allocating VPorts for VMMQ](allocating-vports-for-vmmq.md)
- [Enabling, disabling, and updating VMMQ on a VPort](updating-vmmq-on-a-vport.md)
