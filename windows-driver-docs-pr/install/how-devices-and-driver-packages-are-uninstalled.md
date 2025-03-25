---
title: How Devices and Driver Packages are Uninstalled
description: How Devices and Driver Packages are Uninstalled
ms.date: 06/04/2024
ms.topic: concept-article
---

# How Devices and Driver Packages are Uninstalled

This page describes how software uninstalls a device and removes a driver package from the [driver store](driver-store.md).

## Uninstalling the Device

To remove the device node (*devnode*) that represents a physical device, use one of the following:

* To uninstall only the specified device, use a device installation application that calls the [SetupAPI](setupapi.md) function [**SetupDiCallClassInstaller**](/windows/win32/api/setupapi/nf-setupapi-setupdicallclassinstaller) with a request of [**DIF_REMOVE**](./dif-remove.md).

* To uninstall the specified device and any devices below it in the device tree, use a device installation application that calls the [**DiUninstallDevice**](/windows/win32/api/newdev/nf-newdev-diuninstalldevice) function.

When a device is uninstalled using one of these methods, the Plug and Play (PnP) manager removes the association between the driver binary files and the device.

The device remains in the kernel PnP tree and the [driver package](driver-packages.md) remains in the [driver store](driver-store.md). If the PnP manager re-enumerates the device (for example if the device is unplugged and then plugged in again), the PnP manager treats it as a new device instance and installs the driver package from the driver store.

For info on how an end user can uninstall a device, see  [Using Device Manager to Uninstall Devices and Driver Packages](using-device-manager-to-uninstall-devices-and-driver-packages.md).

## Deleting a Driver Package from the Driver Store

To delete a [driver package](driver-packages.md) from the [driver store](driver-store.md), you must:
* Ensure no devices are installed with the driver package. 
* Remove the driver package from the driver store.

To perform both of these steps with one action, you can do one of the following:

* Starting in Windows 10, version 1607, from the command prompt, use `pnputil /delete-driver <example.inf> /uninstall`. For info on PnPUtil commands, see [PnPUtil Command Syntax](../devtest/pnputil-command-syntax.md).
* Starting in Windows 10, version 1703, a device installation application can call [**DiUninstallDriverW**](/windows/win32/api/newdev/nf-newdev-diuninstalldriverw).

On Windows 10, version 1511 and earlier:

1. Identify all devices currently installed with the driver package and update them so that they do not depend on the driver package. You can do one of the following:
    1. Install a different driver package on the device.
    1. Use [DiInstallDevice](/windows/win32/api/newdev/nf-newdev-diinstalldevice) with the `DIIDFLAG_INSTALLNULLDRIVER` flag to install the null driver on the device.
    1. [Uninstall the device](#uninstalling-the-device).
1. The device installation application then calls [**SetupUninstallOEMInf**](/windows/win32/api/setupapi/nf-setupapi-setupuninstalloeminfa) to remove the driver package.

Deleting a driver package from the driver store removes associated metadata from the PnP manager's internal database and deletes related INF files from the system INF directory.

After the driver package has been removed, it is no longer available to be installed on a device. To reinstall, download the driver package again from the original source, such as Windows Update.

Manually deleting the [driver package](driver-packages.md) from the [driver store](driver-store.md) may result in unpredictable behavior.
