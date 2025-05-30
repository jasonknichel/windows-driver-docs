---
title: Boot Parameters to Load a Partial Checked Build
description: Boot Parameters to Load a Partial Checked Build
keywords:
- partial checked build boot options WDK
- boot parameters WDK
- boot entry parameters WDK
- loading partial checked builds WDK boot options
ms.date: 07/19/2024
ms.topic: reference
---

# Boot Parameters to Load a Partial Checked Build

A *partial checked build* contains checked build versions of the kernel and HAL and a free build of the remainder of the operating system.

> [!NOTE]
> Checked builds were available on older versions of Windows, before Windows 10 version 1803.
> Use tools such as Driver Verifier and GFlags to check driver code.

## Configuring a Partial Checked Build in Windows

To configure a partial checked build use the [**BCDedit /set**](./bcdedit--set.md) command and the **kernel** and **hal** options.

The following commands configure a boot entry to use the checked versions of the kernel and hardware abstraction layer (HAL).

```console
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} kernel ntoskrnl.chk
```

```console
bcdedit /set {18b123cd-2bf6-11db-bfae-00e018e2b8db} hal halacpi.chk
```

To view the results of the commands, type **bcdedit /enum**. The **/enum** option lists all of the boot entries. The boot entry that has been modified to use the checked versions of the kernel and HAL has also been configured for kernel debugging over a serial connection.

```console
## Windows Boot Loader
-------------------
identifier              {18b123cd-2bf6-11db-bfae-00e018e2b8db}
device                  partition=C:
path                    \Windows\system32\winload.exe
description             PartialCheckedBuild
locale                  en-US
inherit                 {bootloadersettings}
debugtype               serial
debugport               1
baudrate                115200
osdevice                partition=C:
systemroot              \Windows
kernel                  ntoskrnl.chk
hal                     halacpi.chk
resumeobject            {d7094401-2641-11db-baba-00e018e2b8db}
nx                      OptIn
debug                   Yes
```
