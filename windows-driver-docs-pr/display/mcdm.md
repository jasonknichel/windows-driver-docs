---
title: Microsoft Compute Driver Model Overview
description: Overview of Microsoft Compute Driver Model
ms.date: 04/24/2025
ms.topic: concept-article
---

# Microsoft Compute Driver Model overview

In Windows 10 version 1903 (WDDM 2.6) and later, the Microsoft Compute Driver Model (MCDM) can be used to write a driver for devices that support compute-only functionality.

An MCDM driver, or compute-only driver, is a scaled down subset of Windows Display Driver Model 2.0+ (WDDM). In WDDM terminology, the driver must advertise itself as a *"render-only" device without display functionality*. The kernel support for "rendering devices" is flexible, as the rendering commands executed by the device are opaque to WDDM. In other words, WDDM can easily support any type of device with an opaque command buffer design.

Unlike WDDM, Windows 10 v1903 and earlier versions of MCDM require the device to have a memory management unit (MMU). The engines of an MCDM device can't require [physical mode](gpu-virtual-memory-in-wddm-2-0.md). Instead, MCDM devices must use virtual address space protection to support multi-tasking in the presence of malicious applications.

An exception exists to support prototype MCDM hardware without an MMU. Beginning with Windows 10 version 2004, prototype MCDM devices can only be used by a single process at a time. These devices are recognized by the absence of supporting either IOMMU or GPU-MMU.

For more information, see the following articles:

* [MCDM architecture](mcdm-architecture.md)
* [MCDM KM driver implementation guidelines](mcdm-implementation-guidelines.md)

For information about the subset of Direct3D 12 features that a compute-only driver can expose in user mode, see [The Direct3D 12 Core 1.0 Feature Level](/windows/win32/direct3d12/core-feature-levels).
