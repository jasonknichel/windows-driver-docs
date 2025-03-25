---
description: The WPD Driver Samples
title: The WPD Driver Samples
ms.date: 12/05/2024
ms.topic: concept-article
---

# The WPD Driver Samples


The Windows Portable Devices Driver Kit includes five sample WPD drivers. These drivers are briefly described in the following table. A more detailed description of these drivers appears later in the documentation.

If you are not familiar with the WPD driver model, begin with the **WpdHelloWorldDriver**.

 

| Sample                                                            | Description                                                                                                                                                                                    |
|-------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [WpdHelloWorldDriver](the-sample-driver-architecture.md)         | A basic sample driver that supports a single device object and multiple read-only properties. This driver simulates hardware interaction.                                                      |
| [WpdBasicHardwareDriver](the-wpdbasichardwaredriver-sample.md)   | A sample driver that interacts with simple sensors. This driver allows WPD applications to receive sensor data and to set the interval at which that data arrives.                             |
| [WpdMultiTransportDriver](the-wpdmultitransportdriver-sample.md) | A sample driver that demonstrates the creation of a single access point for devices that support multiple transports. This driver simulates hardware interaction.                              |
| [WpdWudfSampleDriver](the-wpdwudfsampledriver-sample.md)         | A comprehensive sample driver that demonstrates the WPD device driver interface (DDI). This sample driver simulates hardware interaction.                                                      |
| [WpdServiceSampleDriver](the-wpdservicesampledriver-sample.md)   | A sample driver that demonstrates support for a Contacts service. (Services are an extension of the functional objects that are supported by WPD.) This driver simulates hardware interaction. |


 

