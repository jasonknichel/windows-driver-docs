---
title: HID Clients Overview
description: The HID Clients are drivers, services, or applications that communicate using the HID API and often represent a specific type of device (for example a sensor, a keyboard, or a mouse).
keywords:
- HID clients
- drivers
- services
- HID API
- HID Collection
ms.date: 09/18/2024
ms.topic: concept-article
---

# HID Clients Overview

Human Interface Devices (HID) clients are drivers, services, or applications that communicate using the HID API and often represent a specific type of device such as a sensor, keyboard, or mouse. A hardware ID or a specific HID Collection identifies devices which communicate via the HID API.

| Article | Description |
|--|--|
| [HID usages](./hid-usages.md) | HID usages identify the intended use of HID controls and what the controls actually measure. |
| [HID Collections](./hid-collections.md) | A HID collection is a meaningful grouping of HID controls and their respective [HID usages](./hid-usages.md) |
| [Opening HID collections](./opening-hid-collections.md) | This article describes how a HID Client can communicate with the HID Class driver (HIDClass) to operate the device's HID collections. |
| [Handling HID Reports](./handling-hid-reports.md) | This article describes the mechanisms that user-mode applications and kernel-mode drivers use for handling [HID reports](./hid-api.md) |
| [Freeing Resources](./freeing-resources.md) | User-mode applications and kernel-mode drivers that are HID clients should always free any resources that are no longer required. |
| [Installing HID clients](./installing-hid-clients.md) | This article describes the following requirements for installing HIDClass devices in Microsoft Windows. |
| [HIDClass Hardware IDs for Top-Level Collections](./hidclass-hardware-ids-for-top-level-collections.md) | This article specifies the hardware IDs that the HID class driver generates for top-level collections. |
| [Keyboard and mouse HID client drivers](./keyboard-and-mouse-hid-client-drivers.md) | This article discusses keyboard and mouse HID client drivers. Keyboards and mice represent the first set of HID clients that were standardized in the HID Usage tables and implemented in Windows operating systems. |
| [Sensor HID class driver](./sensor-hid-class-driver.md) | Starting with Windows 8, the Windows operating system includes an in-box sensor HID Class driver (SensorsHIDClassDriver.dll), that supports 11 types of sensors that communicate using the HID transport. |
| [Airplane mode radio management](./airplane-mode-radio-management.md) | Starting with Windows 8, the Windows operating system provides support via HID, for airplane mode radio management controls. |
| [Display brightness control](./display-brightness-control.md) | A standardized solution allows keyboards (external or embedded on laptops), to control a laptop's or tablet's screen brightness through HID. |
