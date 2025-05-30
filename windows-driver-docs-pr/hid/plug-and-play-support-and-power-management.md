---
title: Plug and Play Support for I2C
description: This article describes plug and play support for devices that support HID over the I2C.
ms.date: 10/22/2024
ms.topic: concept-article
---

# Plug and Play support for I2C

This article describes plug and play support for devices that support HID over the I2C transport.

## Driver Loading

Windows loads the HID I2C class driver based on a compatible identifier match between a hardware identifier and the INF. The Advanced Configuration and Power Interface (ACPI) generates the identifier. The hardware identifier is generated for the I2C device node in ACPI. All HID I2C compatible devices must expose the compatibility identifier, in addition to a unique hardware identifier.

The ACPI 5.0 Specification includes support for HID Class Devices. The ACPI definitions for HID I2C are as follows.

| Field | Value | ACPI object | Format | Comments |
|--- | --- | ---- | ---- | ---- |
| Compatible ID | PNP0C50 | \_CID | String in the format of ACPI0C50 or PNP0C50 |CompatibleID |
| Hardware ID | Vendor Specific | \_HID | String in the format of VVVVdddd (e.g NVDA0001) | VendorID + DeviceID |
| Subsystem | Vendor Specific | \_SUB | String in the format of VVVVssss (e.g INTL1234) | SubVendorID + SubSystemID |
| Hardware Revision | Vendor Specific | \_HRV | 0xRRRR (two-byte revision) | RevisionID |
| Current Resource Settings | Vendor Specific | \_CRS | Byte stream | Must include I2CSerialBus and GPIO_INT for I2C controller and GPIO interrupts resp. |
| Device Specific Method | GUID {3CDFF6F7-4267-4555-AD05-B30A3D8938DE} | \_DSM | Package | Defines a structure that contains the HID Descriptor address. |

 Every HID I2C device must provide the following mandatory fields:

- Compatible ID
- Hardware ID
- Hardware Revision
- Current Resource Settings
- Device Specific Method

For more information, see the [Advanced Configuration and Power Interface Specification Version 5.0](https://uefi.org/acpi/specs).

The following hardware IDs and compatible IDs provide an example for a random HID I2C device. These details are based on a sample device that reports itself as a HID with one top-level collection of class "vendor specific."

Advanced Configuration and Power Interface (ACPI) generates the following Hardware IDs and Compatible IDs to load the HID I2C Transport driver:

**Hardware Identifiers**: Compatible Identifiers

**ACPI\\Vid_xxxx&Pid_yyyy&Rev_zzzz;**: ACPI\\PNP0C50

**ACPI\\Vid_xxxxPid_yyyy;**:

**ACPI\\xxxxyyyy;**:

In the previous example, the Hardware ID was generated by using the values extracted from the \_HID ACPI method for the sample device. The Compatible ID is generated by using the values extracted from the \_CID ACPI method for the sample device. The Compatible ID for a HID over I2C must always be PNP0C50 for version 1.0.

**Note**  If you supply an INF, you should only use the hardware identifiers in the left column of the previous table. (Don't use the compatible identifier in the right column.)

The Hardware ID for the HID Client device node generated by the HIDClass.sys component is as follows:

**Hardware Identifier**: Compatible Identifier

**HID\\VEN_MSFT&DEV_0010&REV_0002&Col01;**: N/A

**-HID\\VEN_MSFT&DEV_0010&Col01 HID\\MSFT0010&Col01;**: N/A

**-HID\\\*MSFT0010Col01**: N/A

**-HID_DEVICE_UP:FF00_U:0001;**: N/A

**-HID_DEVICE**: N/A

HIDClass.sys generates the Hardware ID and is identical for all transports. This identifier is based on values passed to HIDClass.sys from HIDI2C.sys (extracted from ACPI).

### Device enumeration sequence

Once a HID I2C device driver (HIDI2C.sys) is loaded, it starts to communicate with the device over the I2C bus. The first operation the driver performs is the device enumeration sequence.

The following list gives the enumeration sequence. The order of this list might change in future versions of Windows.

1. Retrieve [ACPI Source Language (ASL)](https://uefi.org/htmlspecs/ACPI_Spec_6_4_html/19_ASL_Reference/ACPI_Source_Language_Reference.html?highlight=acpi%20source%20language)  code for HID I2C DEVICE from System BIOS.

2. Retrieve HID Descriptor from the Device.
    - Write HID Descriptor Address
    - Read HID Descriptor

3. Issue a SET_POWER to the Device.
    - Write SET_POWER Command

4. Issue a RESET (Host Initiated Reset) to the Device.
    - Write RESET Command
    - Device asserts GPIO interrupt
    - Read value (0x00 0x00) from input register

5. Retrieve report descriptor from the device.
    - Write report descriptor address
    - Read report descriptor

If the HOST fails to successfully complete any of steps 1-5 with the DEVICE, the HIDI2C driver might load with error value of *Code 10*. There's no retry logic built into any of these commands.

**Note:** Steps 4 and 5 may be done in parallel to optimize for time on I2C. Since report descriptors are (a) static and (b) long, Windows 8 may issue a request for 5 while it's waiting for a response from the device on 4.

## Supported HID I2C commands

HIDI2C.SYS driver supports the following commands:

| Command | How it's used | When it's used |
| --- | ---- | --- |
| Reset | Windows supports the Host Initiated Reset. | Windows issues this command during the following scenarios - device initialization - disable/enable - uninstall/reinstall |
| Get/Set_Report | Windows supports the Get/Set_Report commands. | Windows issues this command during the following scenarios - when a HID client driver issues a get/set feature report request - when a HID client driver issues a synchronous input/output report |
| Set_Power | Windows supports the Set_Power command | Windows issues this command during the following scenarios - when the system transitions to a low power S3 / connected standby state - when the system is shut off. |
