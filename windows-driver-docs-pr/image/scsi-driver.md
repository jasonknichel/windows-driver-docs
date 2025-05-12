---
title: SCSI Driver
description: SCSI driver
ms.date: 05/01/2025
---

# SCSI driver

The kernel-mode still image driver for SCSI buses supports **ReadFile** by creating a command descriptor block (CDB) that includes a SCSI **Read** command. It supports **WriteFile** by creating a CDB that includes a SCSI **Write** command. User-mode minidrivers can specify customized CDBs by calling [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol). For more information, see [SCSI Still Image I/O Control Codes](/windows-hardware/drivers/ddi/_image/index). See the Microsoft Windows SDK documentation for descriptions of **ReadFile** and **WriteFile**.
