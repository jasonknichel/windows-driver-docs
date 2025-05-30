---
title: What Happens when you Provision a Computer (WDK 8.1)
description: Here we show what happens when you use version 8.1 of the Windows Driver Kit (WDK) to provision a target computer.
ms.date: 04/20/2017
ms.topic: concept-article
---

# What happens when you provision a computer (WDK 8.1)

Using Microsoft Visual Studio to configure and set up driver deployment and driver testing is called *provisioning a target computer* or *provisioning a test computer*. For information about provisioning, see [Provision a computer for driver deployment and testing (WDK 8.1)](../gettingstarted/provision-a-target-computer-wdk-8-1.md). Here we show what happens when you use version 8.1 of the Windows Driver Kit (WDK) to provision a target computer.

## When you provision a computer (WDK 8.1)

Provisioning a computer performs the following tasks:

-   Copies installation files to %SystemDrive%\\DriverTest
-   Creates a user named WDKRemoteUser and switches to that user
-   Installs .NET 4.0 if it is not already installed
-   Installs Microsoft Visual C++ Redistributable
-   Installs [Test Authoring and Execution Framework (TAEF)](../taef/index.md) (WDK Client)
-   Installs debuggers
-   Installs [Windows Device Testing Framework](../wdtf/index.md) (WDTF)
-   Turns off AutoReboot
-   Enables kernel memory crash dumps
-   Disables Screen Saver
-   Disables workstation lock policy
-   Disables ForceGuest
-   Sets the power policy to a high power configuration, which prevents the system from entering Standby or Hibernate Mode when idle
-   Enables the RTC Wake timer
-   Enables and configures kernel debugging
-   Enables test signing of drivers
-   Reboots the target computer if necessary
-   Creates a system restore point

## Removing provisioning from the target computer

Once you have provisioned a target computer, you cannot completely remove the provisioning. However, you can remove most of the provisioning from the target computer by using Visual Studio on the host computer. Here are the steps.

1.  On the host computer, in Visual Studio, on the **Driver** menu, choose **Test &gt; Configure Computers**.
2.  Select the name of the target computer, and select **Delete computer**.
3.  Select **Remove provisioning and delete computer**. Select **Next**.
4.  When the removal process is complete, select **Finish**.
5.  Uninstall WDK Test Target Setup from the target computer.

## When you remove provisioning (WDK 8.1)

When you remove provisioning from the target computer, these items are removed:

-   Test Automation Framework
-   Debuggers
-   Windows Driver Testing Framework
-   %SystemDrive%\\DriverTest folder and contents
-   WDKRemoteUser account
-   Workstation lock policy

Removing provisioning does not change these items:

-   Visual C++ Redistributable
-   AutoReboot setting
-   Kernel memory crash dump setting
-   Screen saver setting
-   ForceGuest setting
-   Power policy
-   RTC Wake timer setting
-   Kernel debugging settings
-   Test signing setting

 

