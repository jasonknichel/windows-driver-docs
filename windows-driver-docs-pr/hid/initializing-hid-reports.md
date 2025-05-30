---
title: Initializing HID Reports
description: Initializing HID Reports
keywords:
- HID reports WDK , initializing
- reports WDK HID , initializing
- initializing reports
- controls WDK HID
ms.date: 10/22/2024
ms.topic: concept-article
---

# Initializing HID Reports

This article describes how user-mode applications and kernel-mode drivers initialize a HID report before using the [HIDClass support routines](/windows-hardware/drivers/ddi/_hid) or the HID class driver IOCTLs.

To initialize a report buffer, an application or driver creates a zero-initialized buffer of the required size, in bytes, for the report type. The *Xxx*ReportByteLength members of a HID collection's [**HIDP_CAPS**](/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps) structure specify the required size of input, output, and feature reports. After initializing a report buffer, an application or driver can use **HidP_Set***Xxx* routines to set control data in the report. On the first use of a report, the **HidP_Set***Xxx* routines set the report ID to the one associated with a specified [HID usage](hid-usages.md). If the application or driver subsequently attempts to set a usage that is incompatible with the report ID, the **HidP_Set***Xxx* routines return a status of HIDP_STATUS_INCOMPATIBLE_REPORT_ID.
