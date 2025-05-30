---
title: Enable DMA Remapping for Device Drivers
description: Enable and opt-into Direct Memory Access(DMA) remapping to ensure compatibility with Kernel DMA Protection and DMAGuard policies.
ms.date: 01/22/2025
ms.topic: how-to
---

# Enable DMA remapping for device drivers

To ensure compatibility with [Kernel DMA Protection](/windows/security/information-protection/kernel-dma-protection-for-thunderbolt) and [DMAGuard Policy](/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy), PCIe device drivers can opt into Direct Memory Access (DMA) remapping.

DMA remapping for device drivers protects against memory corruption and malicious DMA attacks, and provides a higher level of compatibility for devices. Also, devices with DMA remapping-compatible drivers can start and perform DMA regardless of lock screen status.

On Kernel DMA Protection enabled systems, DMAGuard Policy might block devices, with DMA remapping-incompatible drivers, connected to [external](./dsd-for-pcie-root-ports.md#identifying-externally-exposed-pcie-root-ports)/[exposed](./dsd-for-pcie-root-ports.md#identifying-internal-pcie-ports-accessible-to-users-and-requiring-dma-protection) PCIe ports (for example, M.2, Thunderbolt), depending on the policy value set by the system administrator.

## Driver requirements for enabling and opting into DMA remapping

Drivers perform DMA using the following interfaces:

- [WDF DMA interfaces](../wdf/introduction-to-dma-in-windows-driver-framework.md)

- [WDM interfaces](/windows-hardware/drivers/ddi/wdm/)

- [NDIS interfaces](/windows-hardware/drivers/ddi/_netvista/)

To adjust the DMA remapping policy for your driver, add an INF directive. There are two possible methods: a per-device (recommended and preferred) mechanism and a per-driver (legacy) mechanism.

## Per-device opt-in mechanism

For Windows 24H2 and later versions, use this per-device method. The per-device opt-in overrides the legacy per-driver method, if present (for example, the **DmaRemappingCompatible** key is ignored if **RemappingSupported** is set).

Add an INF directive such as the following to the device enumeration section:

```inf
[MyDriver_Device.NT.HW]
AddReg=DMA_Remapping_OptIn_AddReg

[DMA_Remapping_OptIn_AddReg]
HKR,"DMA Management","RemappingSupported",0x00010001,1
```

Valid values for **DMA Management\RemappingSupported**:

| Value | Meaning |
|--|--|
| 0 | Opt-out. Indicates the device and driver are incompatible with DMA remapping. |
| 1 | Opt-in. Indicates the device and driver are fully compatible with DMA remapping. |
| No registry key | Let the system determine the policy. |

Optionally, you can add RemappingFlags to further control the behavior:

```inf
[DMA_Remapping_OptIn_AddReg]
HKR,"DMA Management","RemappingSupported",0x00010001,1
HKR,"DMA Management","RemappingFlags",0x00010001,0x00000001
```

Valid values for **DMA Management\RemappingFlags**:

| Value | Meaning |
|--|--|
| 0 | If **RemappingSupported** is 1, opt-in unconditionally. |
| 1 | If **RemappingSupported** is 1, opt-in but only when one or more of the following conditions are met: A. The device is an external device (for example, Thunderbolt); B. DMA verification is enabled in Driver Verifier |
| No registry key | Same as 0 value. |

These registry keys appear under the enumeration tree: ``HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\PCI\<device instance path>\Device Parameters\DMA Management``

### Per-driver opt-in mechanism

Only use this per-driver method for Windows versions up to Windows 11 23H2. It is recommended to use the [per-device method](#per-device-opt-in-mechanism).

Add an INF directive such as the following to the service installation section:

```inf
[MyServiceInstall_AddReg]
HKR,Parameters,DmaRemappingCompatible,0x00010001,1    ; where 1 = opt-in
```
  
Valid values for **DmaRemappingCompatible**:

| Value | Meaning |
|--|--|
| 0 | Opt-out. Indicates that your driver is incompatible with DMA remapping. |
| 1 | Opt-in. Indicates that your driver is fully compatible with DMA remapping. |
| 2 | Opt-in, but only when one or more of the following conditions are met: A. The device is an external device (for example, Thunderbolt); B. DMA verification is enabled in Driver Verifier |
| 3 | Opt-in |
| No registry key | Let the system determine the policy. |

When testing your driver, enable Driver Verifier. For testing purposes under Driver Verifier, the value of the INF directive for opting in external devices is promoted to 1.

The registry key appears under the service installation tree: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\<driver name>\Parameters`.

> [!WARNING]
> DMA remapping isn't supported for graphics device drivers.

## Validating that DMA remapping is enabled for a specific device driver instance

Use the latest Windows build with VT-d/AMD-Vi enabled to test driver functionality on Intel x64 and AMD64 systems.

To check if a specific driver opted into DMA remapping, look in Device Manager, in the device's **Details** tab, for the values corresponding to the DMA remapping policy property. A driver can query the [**DEVPKEY_Device_DmaRemappingPolicy**](../install/devpkey-device-dmaremappingpolicy.md) property to determine the DMA remapping capability of the device. See potential return values on that page, and note that these return values aren't the same as the values for **DmaRemappingCompatible** listed in the previous section.

![Device Manager Details Tab.](images/device-details-tab-1903.png)

>[!NOTE]
> For Windows 10, versions 1803 and 1809, the property field in Device Manager uses a GUID {83da6326-97a6-4088-9453-a1923f573b29}[18]
