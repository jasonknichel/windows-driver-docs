---
title: Windows Support for USB Type-C Connectors
description: Windows support for USB Type-C connector and tasks for OEMs who are building USB Type-C systems.
ms.date: 04/22/2025
ms.topic: concept-article
---

# Windows support for USB Type-C connectors

This article is intended for OEMs who want to build a Windows system with USB Type-C connector. You can use OS features that allow for faster charging, power delivery, dual role, alternate modes, and error notifications through Billboard devices.

A traditional USB connection uses a cable with a USB A and USB B connector on each end. The USB A connector always plugs in to the host side and the USB B connector connects the function side, which is a device (phone) or peripheral (mouse, keyboard). By using those connectors, you can only connect a host to a function; never a host to another host or a function to another function. The host is the power source provider and the function consumes power from the host.

The traditional configuration limits some scenarios. For example, if a mobile device wants to connect to a peripheral, the device must act as the host and deliver power to the connected device.

The USB Type-C connector, introduced by the USB-IF, defined in the USB 3.1 specification, addresses those limitations. Windows 10 introduced native support for those features.

:::image type="content" source="images/typecccomp.jpg" alt-text="Picture of micro-USB and USB Type-C connectors for comparison.":::

## Feature summary

- Supports faster charging, up to 100 watts with power delivery (PD) over USB Type-C.
- Uses a single connector for both USB Hosts and USB Devices.
- Switches USB roles to support a USB host or device.
- Switches power roles between sourcing and sinking power.
- Supports other protocols like DisplayPort and Thunderbolt over USB Type-C.
- Introduces USB Billboard device class to provide error notifications for Alternate Modes.

## Official specifications

- [USB Type-C specification](https://usb.org/document-library/usb-type-cr-cable-and-connector-specification-revision-20)
- [USB Power Delivery](https://www.usb.org/sites/default/files/D2T2-1%20-%20USB%20Power%20Delivery.pdf)
- [Billboard Devices specification](https://www.usb.org/document-library/billboard-device-class-spec-revision-121-and-adopters-agreement#:~:text=The%20USB%20Billboard%20Device%20Class%20definition%20describes%20the,to%20provide%20support%20details%20in%20a%20human-readable%20format.)
- [UCSI Specification](https://www.intel.com/content/www/us/en/products/docs/io/universal-serial-bus/usb-type-c-ucsi-spec.html)

## Hardware design

USB Type-C connector is reversible and symmetric.

:::image type="content" source="images/usb-type-c.png" alt-text="Picture of a USB Type-C symmetric cable.":::

The main components are the USB Type-C connector and its port or PD controller that manages the CC pin logic for the connector. Such systems typically have a dual-role controller that can swap the USB role from host to function. It has Display-Out module that allows video signal to be transmitted over USB. Optionally it can support BC1.2 charger detection.

- [Hardware design of a USB Type-C system](architecture--usb-type-c-in-a-windows-system.md)
- [Hardware design for a USB Type-C system with an embedded controller](ucsi.md)

Consider recommendations for the design and development of USB components. Include minimum hardware requirements, Windows Hardware Compatibility Program requirements, and other recommendations that build on those requirements.

- [Hardware component guidelines USB](/windows-hardware/design/component-guidelines/universal-serial-bus--usb-)

## Choose a driver model

Use this flow chart to determine a solution for your USB Type-C system.

:::image type="content" source="images/drivers-c.png" alt-text="A flow chart to determine a solution for your USB Type-C system.":::

| If your system... | Recommended solution... |
|--|--|
| Doesn't implement PD state machines | Write a client driver to the UcmTcpciCx class extension.<br/><br/>[Write a USB Type-C port controller driver](write-a-usb-type-c-port-controller-driver.md) |
| Implements PD state machines in hardware or firmware and support USB Type-C Connector System Software Interface (UCSI) over ACPI | Load the Microsoft provided in-box drivers, UcmUcsiCx.sys, and UcmUcsiAcpiClient.sys.<br/><br/>See [UCSI driver](ucsi.md). |
| Implements PD state machines in hardware or firmware, but either doesn't support UCSI, or supports UCSI but requires a transport other than ACPI | Write a client driver for the UcmCx class extension.<br/><br/>[Write a USB Type-C connector driver](bring-up-a-usb-type-c-connector-on-a-windows-system.md)<br/><br/>[Write a USB Type-C Policy Manager client driver](policy-manager-client.md) |
| Implements UCSI but requires a transport other than ACPI | Write a client driver to the UcmUcsiCx class extension.<br/><br/>Use [this sample template](https://github.com/Microsoft/Windows-driver-samples/tree/main/usb/UcmCxUcsi) and modify it based on a transport that your hardware uses.<br/><br/>[Write a UCSI client driver](write-a-ucsi-driver.md) |

## Bring up drivers

- USB Function driver bring-up is only required if you support USB Function mode. If you previously implemented a USB Function driver for a USB micro-B connector, describe the appropriate connectors as USB Type-C in the ACPI tables for the USB Function driver to continue working.

    For more information, see [instructions about writing a USB Function driver](developing-windows-drivers-for-usb-function-controllers.md).

- USB Role-Switch driver bring-up is only required for devices that have a Dual Role controller that assumes both Host and Function roles. To bring-up the USB Role-Switch driver, you need to modify the ACPI tables to enable the Microsoft in-box USB role-switch driver.

    For more information, see the [guidance for bringing up the USB Role Switch Driver](dual-role-controller-bringup-for-a-usb-type-c-system.md).

- A USB Connector Manager Driver is required for Windows to manage the USB Type-C ports on a system. The bring-up tasks for a USB Connector Manager driver depend on the driver that you choose for the USB Type-C ports: The Microsoft in-box UCSI (UcmUcsiCx.sys and UcmUcsiAcpiClient.sys) driver, a UcmCx client driver, or a UcmTcpciCx client driver. For more information, see the links in the preceding section that describe how to choose the right solution for your USB Type-C system.

## Test

Perform various functional and stress tests on systems and devices that expose a USB Type-C connector.

- **[Test USB Type-C systems with USB Type-C ConnEx](test-usb-type-c-systems-with-mutt-connex-c.md)**: Run USB tests included in the Windows Hardware Lab Kit (HLK).
- **Run USB function HLK tests with a C-to-A cable**: Search for *Windows USB Device* in the HLK.
- **Certification and compliance**: Attend power delivery and USB Type-C compliance workshops hosted by the standards bodies.

## See also

- [FAQ: USB Type-C connector on a Windows system](faq--usb-type-c-connector-on-a-windows-system.yml)
- [Fix USB-C problems in Windows](https://support.microsoft.com/windows/fix-usb-c-problems-in-windows-f4e0e529-74f5-cdae-3194-43743f30eed2)
