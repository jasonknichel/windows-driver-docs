---
title: Download the Windows Driver Kit (WDK)
description: Download instructions for the latest released version of the Windows Driver Kit (WDK)
keywords:
- Windows Driver Kit
- WDK
- Download
- drivers
ms.date: 05/14/2025
ms.topic: how-to
---

# Download the Windows Driver Kit (WDK)

The WDK is used to develop, test, and deploy drivers for Windows. The most recent public release is WDK 10.0.26100.3323 (released March 14, 2025).

- You can install and run this WDK on Windows 7 and later.
- You can use this kit to build drivers for Windows 10, Windows Server 2016, and later client and server versions.

> [!IMPORTANT]
> Starting in May 2025, Microsoft no longer publishes older versions of Windows Drivers Kit. Use the latest release of the WDK for all driver development efforts. If you're targeting older versions of Windows, follow the guidance in the [Building Drivers for Previous OS Releases Using the Latest Windows Driver Kit (WDK)](https://techcommunity.microsoft.com/blog/windowsdriverdev/building-drivers-for-previous-os-releases-using-the-latest-windows-driver-kit-wd/4374910) blog post. If your development scenario is not supported by the latest WDK, contact [Microsoft WDK Feedback](mailto:wdkfeedback@microsoft.com) for assistance.

[Join the Windows Insider Program](https://insider.windows.com/) to get [WDK Insider Preview builds](https://aka.ms/wipwdk). For installation instructions for Windows Insider Preview builds, see [Installing preview versions of the Windows Driver Kit (WDK)](./installing-preview-versions-wdk.md).

## WDK NuGet package support

WDK is available as a NuGet package starting from version 10.0.26100.1. Users can access and use these packages directly from nuget.org within Visual Studio. WDK NuGet package provides a convenient way to acquire and update the WDK, it also manages dependencies such as the SDK, helping to keep the driver development toolchain current. For more information, see [Install the latest WDK using NuGet](install-the-wdk-using-nuget.md).

## ARM64 support

Beginning in WDK version 10.0.26100.1, the WDK now supports the development, testing, and deployment of drivers on ARM64 machines. The WDK/EWDK can be installed and run natively on ARM64 hardware. Additionally, the previously supported emulation of x86 KMDF/UMDF2 drivers on ARM64 hardware is still available. Also, debugging and deploying drivers to an ARM64 target machine is now supported from both ARM64 and x64 host machines. When you install the WDK/EWDK on ARM64 machines, the process automatically identifies and installs all necessary dependencies, including build tools, binaries, and libraries.

## ![download icon for Visual Studio](images/download-install.png) Step 1: Install Visual Studio 2022

The WDK requires Visual Studio. For more information about system requirements for Visual Studio, see [Visual Studio 2022 System Requirements](/visualstudio/releases/2022/system-requirements).

The following editions of Visual Studio 2022 support driver development for this release:

- [Download Visual Studio Community 2022](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=17)
- [Download Visual Studio Professional 2022](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Professional&rel=17)
- [Download Visual Studio Enterprise 2022](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Enterprise&rel=17)

When you install Visual Studio 2022, select the **Desktop development with C++** workload, then under Individual Components add:

- MSVC v143 - VS 2022 C++ ARM64/ARM64EC Spectre-mitigated libs (Latest)
- MSVC v143 - VS 2022 C++ x64/x86 Spectre-mitigated libs (Latest)
- C++ ATL for latest v143 build tools with Spectre Mitigations (ARM64/ARM64EC)
- C++ ATL for latest v143 build tools with Spectre Mitigations (x86 & x64)
- C++ MFC for latest v143 build tools with Spectre Mitigations (ARM64/ARM64EC)
- C++ MFC for latest v143 build tools with Spectre Mitigations (x86 & x64)
- Windows Driver Kit

> [!TIP]
> Use the Search box to look for "64 latest spectre" (in English installations) or "64 latest" (in non-English installations) to quickly see these components.

:::image type="content" source="images/installing-VS-components-64-latest-spectre.png" alt-text="Image showing the six components listed with checkboxes set.":::

> [!NOTE]
> The **Desktop development with C++** workload selected does not install the Windows SDK 10.0.26100.1.

## ![download icon for SDK](images/download-install.png) Step 2: Install SDK

Installing Visual Studio doesn't download the latest SDK version, use the following link to install

- [Download the latest Windows SDK](https://developer.microsoft.com/windows/downloads/windows-sdk/)

The provided links for the SDK and the WDK have matching build numbers, which is always required for the kits to work together. If you decide to install your own SDK/WDK pair, perhaps for a different Windows version, ensure that the build numbers match. For more information, see [Kit versioning](#kit-versioning).

## ![download icon for WDK](images/download-install.png) Step 3: Install WDK

- [Download WDK 10.0.26100.3323](https://go.microsoft.com/fwlink/?linkid=2307500)

Starting with version 17.11.0, the WDK VSIX is included as an individual component in Visual Studio. Before installing the WDK, the installer checks if a compatible version of the VSIX is already installed. If the WDK VSIX is not found, users will be prompted to install it. To install the WDK VSIX, launch the Visual Studio Installer, select **Modify**, navigate to the **Individual Components** tab, add **Windows Driver Kit**, and then select **Modify** again.

:::image type="content" source="images/install_wdk_vsix_msg.png" alt-text="Image asking the user to install WDK VSIX.":::

> [!TIP]
> If you can't find driver project templates in Visual Studio, the WDK Visual Studio extension didn't install properly. To resolve this, launch Visual Studio Installer, select **Modify**, add **Windows Driver Kit** in the **Individual Component** tab, and select **Modify**.

## ![download icon for EWDK](images/download-install.png) Enterprise WDK (EWDK)

As an alternative to downloading Visual Studio, the SDK, and the WDK, you can download the EWDK, which is a standalone, self-contained command-line environment for building drivers. It includes Visual Studio Build Tools, the SDK, and the WDK.

The latest public version of the EWDK contains Visual Studio 2022 Build Tools 17.11.4 and MSVC toolset v14.41

The EWDK also requires the .NET Framework version 4.7.2. For more information about other requirements for the .NET Framework, see [.NET Framework system requirements](/dotnet/framework/get-started/system-requirements).

- [Download EWDK 10.0.26100.3323 with Visual Studio Build Tools](/legal/windows/hardware/enterprise-wdk-license-2022)

After you download the ISO, use these steps to set up your build environment:

1. Mount the EWDK ISO from a drive volume. Network share paths aren't currently supported.
1. Run *LaunchBuildEnv.cmd*.
1. In the environment created in step 2, type **SetupVSEnv**, and then press **Enter**.
1. Launch devenv.exe from the same environment, using the full file path. For example: `"C:\Program Files\Microsoft Visual Studio\2022\%Community|Professional|Enterprise%\Common7\IDE\devenv.exe"`
1. When you're done with the build environment, you might want to eject the ISO.

You can optionally use the Visual Studio interface with the build tools provided in the EWDK. To use the Visual Studio interface, ensure that the Visual Studio major version matches the version of the Visual Studio Build Tools in the EWDK. For example, Visual Studio 2022 works with the EWDK that contains VS17.X build tools. For a list of Visual Studio 2022 version numbers, see [Visual Studio 2022 Releases](/visualstudio/releases/2022/release-history).

## Kit versioning

A full kit build string includes as its last two components, the build number and a QFE (Quick Fix Engineering) value. For example, 10.0.22621.2428 has a build number of 22621, and a QFE value of 2428.

To build a driver, the *build number* of your SDK installation must match the *build number* of your WDK installation. The QFE values don't need to match unless your driver uses functionality that is only available in the headers included with a later QFE.

A quick way to see the full build string for locally installed kits is to go to Windows settings (Win+I), navigate to **Apps**, then **Installed apps**, and in the **Search** box type `kit`. The full build string appears to the right of the kit name. If you navigate to `C:\Program Files (x86)\Windows Kits\10\Include`, the QFE shown is hardcoded to `.0`. So, the directory name isn't a reliable way to check your QFE identifier. When you install a kit, the new installation replaces any previously existing installation of the same build number. When you install Visual Studio with the **Desktop development with C++** workload, if the installation payload includes the Windows SDK, the right-hand Summary pane also shows a hardcoded `.0` for QFE.

## Driver samples for Windows

Download the driver samples in one of these ways:

- Go to the driver samples page on [GitHub](https://github.com/Microsoft/Windows-driver-samples), select **Clone or download**, and then select **Download ZIP**.
- Download the [GitHub Extension for Visual Studio](https://visualstudio.github.com/), and then connect to the GitHub repositories.
- Browse the driver samples on the [Microsoft Samples portal](/samples/browse/?products=windows-wdk).

## Related downloads

- [Download the WDK Insider Preview](https://www.microsoft.com/software-download/windowsinsiderpreviewWDK)
- [Download previous versions of the WDK](other-wdk-downloads.md)
- [Download the Windows Assessment and Deployment Kit (Windows ADK)](/windows-hardware/get-started/adk-install)
- [Download the Windows HLK](/windows-hardware/test/hlk/windows-hardware-lab-kit)
- [Download the Windows Debugging Tools (WinDbg)](./debugger/debugger-download-tools.md)
- [Download Windows Symbol Packages](./debugger/debugger-download-symbols.md)

## See also

- [Windows 11 hardware requirements](/windows/whats-new/windows-11-requirements)
- [Install the WDK using WinGet](./install-the-wdk-using-winget.md)
- [Learn what's new in driver development](./what-s-new-in-driver-development.md)
- [Review known issues](./wdk-known-issues.md)
