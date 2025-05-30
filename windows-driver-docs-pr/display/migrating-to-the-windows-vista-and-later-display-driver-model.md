---
title: Migrating to WDDM
description: Migrating to the Windows Display Driver Model (WDDM)
keywords:
- display driver model WDK Windows Vista , migrating
- Windows Vista display driver model WDK , migrating
- migrating display driver model WDK Windows Vista
ms.date: 08/21/2024
ms.topic: concept-article
---

# Migrating to WDDM

> [!NOTE]
> XDDM and VGA drivers will not compile on Windows 8 and later operating systems. If display hardware is attached to a Windows 8 computer without a driver that is certified to support WDDM 1.2 or later, the system defaults to running the Basic Display Driver.
>
> New drivers should be written as WDDM drivers.

To migrate to the Windows Display Driver Model (WDDM), driver developers need to write completely different display and video miniport drivers. Similar to the [Windows 2000 display driver model (XDDM)](windows-2000-display-driver-model-design-guide.md), WDDM requires a paired display driver and display miniport driver. However, in WDDM:

* The display driver runs in user mode, and is hence referred to as the user-mode display driver (UMD).

* The video miniport driver is known as the kernel-mode display miniport driver (KMD).

* The model doesn't use services of the Windows Graphics Device Interface (GDI) engine. Instead, it uses services of the Direct3D runtime and DirectX graphics kernel subsystem (*Dxgkrnl.sys*).

Although driver writers can reuse low-level hardware-dependent code in their WDDM drivers, they should rewrite new device driver interface (DDI)-related code. When writing WDDM drivers, consider these points:

* The KMD must implement a revised set of entry-point functions to interact with the operating system and the DirectX graphics kernel subsystem (*Dxgkrnl.sys*). For more information, see [DriverEntry of Display Miniport Driver](driverentry-of-display-miniport-driver.md). The KMD can call any documented kernel-mode function.

* The KMD dynamically loads the appropriate *Dxgkrnl.sys*. KMD and *Dxgkrnl* call each other through interfaces.

* The KMD is no longer required to process *most* video I/O control codes (IOCTLs). In XDDM, the kernel-mode display driver uses these codes to communicate with the video miniport driver. In WDDM, the UMD communicates with the Direct3D runtime. In turn, *Dxgkrnl* communicates with KMD.

  WDDM still uses the following IOCTLs, and the KMD must process them:
  * [**IOCTL_VIDEO_QUERY_COLOR_CAPABILITIES**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_color_capabilities)
  * [**IOCTL_VIDEO_HANDLE_VIDEOPARAMETERS**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters)

* The UMD must implement and export an [**OpenAdapter**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openadapter) function, which opens an instance of the graphics adapter. The UMD must also implement a [**CreateDevice**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice) function, which creates representations of display devices that handle collections of rendering state.

* The UMD's [**CreateResource**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource) function, along with the KMD's [**DxgkDdiCreateAllocation**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation) function, replace the [*DdCanCreateSurface*](/previous-versions/windows/hardware/drivers/ff549213(v=vs.85)), [*DdCreateSurface*](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85)), and [**D3dCreateSurfaceEx**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) functions in XDDM.

* Most of the remaining UMD functions implement the same functionality that the kernel-mode XDDM display driver implemented in the following functions:

  * The [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) function and [**DP2**](/windows-hardware/drivers/ddi/d3dhal/ne-d3dhal-_d3dhal_dp2operation) operation codes
  * The [motion compensation callback functions](/windows-hardware/drivers/ddi/_display/#functions) and [DirectX Video Acceleration structures](/windows-hardware/drivers/ddi/_display/#structures)
