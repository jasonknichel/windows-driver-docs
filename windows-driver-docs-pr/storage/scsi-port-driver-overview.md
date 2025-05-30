---
title: SCSI Port Driver Overview
description: SCSI Port Driver Overview
keywords:
- storage port drivers WDK , SCSI Port driver
- SCSI Port drivers WDK storage
ms.date: 06/26/2024
ms.topic: concept-article
---

# SCSI Port Driver Overview

Windows provides a SCSI Port driver as a standard feature of the Windows storage architecture. The Windows storage architecture also provides the [Storport Driver](storport-driver-overview.md), which is the recommended alternative to SCSI Port for high-performance devices.

The SCSI Port driver streamlines the Windows storage subsystem by emulating a simplified SCSI adapter. Storage class drivers load on top of the SCSI port driver. This architecture allows you to write Windows storage class drivers with minimal concern for the unique hardware features of each SCSI adapter.

The emulation capabilities of the SCSI Port driver also allow you to develop minidrivers that are simpler to design and code than a monolithic port driver. In other words, using the SCSI Port driver allows you to focus on developing a miniport driver that handles the particular features of your adapter.

To use the SCSI Port support routines, link to one of the SCSI Port support libraries, *scsiport.lib* or *scsiwmi.lib*. These SCSI Port libraries handle all interaction between the miniport driver and the hardware abstraction layers (HAL) of the operating system. Miniport drivers must not link directly to the HAL support library, *hal.lib*, nor should they link directly to the *ntoskrnl.lib* or *libcntpr.lib* support libraries. SCSI miniport drivers to are incorrectly linked don't qualify for the [Windows Hardware Compatibility Program](/windows-hardware/design/compatibility/).

The following articles examine the key features of the SCSI Port driver.

- [Capabilities Provided by SCSI Port](capabilities-provided-by-scsi-port.md)

- [SCSI Port Driver Support Routines](scsi-port-driver-support-routines.md)

- [SCSI Port's Interface with the Storage Class Driver](scsi-port-s-srb-interface-with-the-storage-class-driver.md)

- [SCSI Port's Interface with SCSI Port Miniport Drivers](scsi-port-s-interface-with-scsi-port-miniport-drivers.md)

- [SCSI Port I/O Model](scsi-port-i-o-model.md)

A general discussion of SCSI Port miniport drivers is provided in [SCSI Miniport Drivers](scsi-miniport-drivers.md).
