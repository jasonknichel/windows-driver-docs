---
title: Sensor Device Driver Design Guide
description: Sensor device driver design guide
ms.assetid: 74e8ae08-3e61-41be-aed0-e733dc6072cf
ms.date: 05/15/2025
ms.topic: concept-article
---

# Introduction to the Sensor and Location Platform in Windows

The Windows operating system provides native support for sensor devices. This support includes location sensors such as GPS devices. As part of this support, the platform provides a standard way for device manufacturers to expose sensor devices to software developers and consumers. At the same time, the platform gives developers a standardized API and device driver interface (DDI) to work with sensors and sensor data. This section summarizes the Windows sensor and location platform, discusses the various parts of the platform, and describes how the pieces work together to provide a comprehensive system for working with sensors.

## Sensor Device Overview

Sensors come in many configurations and, from a certain perspective, almost anything that provides data about physical phenomena can be called a sensor. Although we typically think of sensors as hardware devices, logical sensors can also provide information through emulation of sensor functionality in software or firmware. Also, a single hardware device can contain multiple sensors.

The sensor and location platform organizes sensors into **categories**, which represent broad classes of sensor devices, and **types**, which represent specific kinds of sensors. For example, a sensor in a video game controller can detect the position and movement of a player's hand. This kind of sensor is an orientation sensor. Its type is a 3-D accelerometer. In code, Windows represents categories and types by using globally unique identifiers (GUIDs), many of which are predefined. Device manufacturers can create new categories and types by defining and publishing new GUIDs, when required.

Location devices comprise one especially interesting category. By now, most people are familiar with global positioning systems (GPS). In Windows, a GPS is a kind of sensor that is part of the Location category. The Location category could include other sensor types. Some sensor types are software based. For example, an IP resolver provides location information using an Internet address. A cellular phone tower triangulator determines location based on nearby towers. Another sensor finds location from the presence of Wi-Fi networks.

## About the Platform

The Windows sensor and location platform consists of the following developer and user components:

- The DDI. Windows provides a standard way for sensor devices to connect to the computer and to provide data to other subsystems.
- The Windows Sensor API provides a set of methods, properties, and events to work with connected sensors and sensor data.
- The Windows Location API, which is built on the Windows Sensor API, provides a set of programming objects. These objects include scripting objects, for working with location information.
- The Control Panel gives computer users control over location settings.

The following sections describe each of these components.

### Device Driver Interface

Sensor manufacturers can create device drivers to connect sensors with Windows. Sensor device drivers are implemented by using the Windows Portable Devices (WPD) driver model, which is based on the Windows User Mode Driver Framework (UMDF). Many device drivers are written using these frameworks. Because these technologies are established, experienced device driver programmers find writing a sensor driver to be a familiar task. The sensor DDI uses specific UMDF and WPD data types and interfaces. It also defines sensor-specific WPD commands and parameters when needed.

To help make it easier to write a device driver that exposes a sensor to Windows (and to the sensor and location platform in particular), the operating system includes a driver class extension. A required component for sensor device drivers, this COM object provides a simple set of interfaces that enable programmers to implement a sensor driver without writing lots of boilerplate code. The class extension can also reduce, or even eliminate, the need to manage WPD calls. This documentation contains detailed information about the sensor DDI and class extension object.

### Sensor API

The Windows Sensor API enables C++ developers to create sensor-based programs by using a set of COM interfaces. The API provides interfaces for common sensor programming tasks. These tasks include managing sensors by category, type, or ID. You can also manage sensor events, work with individual sensors and sensor collections, and handle sensor data. The Windows SDK includes header files, documentation, samples, and tools to help guide software developers on how to use sensors in Windows programs.

### Location API

The Location API provides an easy way to retrieve data about geographic location while protecting user privacy. The Location API provides its functionality through a set of COM interfaces that represent objects. Programmers who understand how to use COM can use these objects. Scripting support gives easy access to location data for projects that run in the local computer zone, such as gadgets. The Windows SDK includes header files, documentation (including scripting reference documentation), samples, and tools to help guide Web and software developers on how to use location information in their programs.

### User Control Panel

Windows includes a control panel that allows computer users to enable or disable location settings. Because the settings can expose sensitive data, this user interface gives users control over whether programs have access to their location.

## Whitepapers

| Title | Description |
|--|--|
| [HID Sensors Usages](/windows-hardware/design/whitepapers/hid-sensors-usages) | This paper provides information about the HID Sensor Class Driver for Windows 8 and later operating systems. |
| [Integrating Ambient Light Sensors with Computers Running Windows 10 Creators Update](/windows-hardware/design/whitepapers/integrating-ambient-light-sensors-with-computers-running-windows-10-creators-update) | This paper provides information about ambient light sensor (ALS) features in the Windows 10 operating system. |
| [Integrating Motion and Orientation Sensors](/windows-hardware/design/whitepapers/integrating-motion-and-orientation-sensors) | This paper is intended to help OEMs, ODMs, and IHVs understand motion and orientation sensor capabilities and requirements for Windows 10 and earlier operating systems. |

## Related sections

- [Sensors DDI reference](/windows-hardware/drivers/ddi/_sensors/)
