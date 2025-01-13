---
title: Videos Debugging UMDF Drivers
description: This topic contains a series of videos by Abhishek Ram that demonstrate how to debug User-Mode Driver Framework (UMDF) drivers.
Search.SourceType: Video
ms.date: 04/20/2017
---

# Videos: Debugging UMDF Drivers


This topic contains a series of videos by Abhishek Ram that demonstrate how to debug User-Mode Driver Framework (UMDF) drivers.

After watching the videos, you'll be familiar with the UMDF debugger extensions and know how to use them in basic debugging scenarios.

While the videos demonstrate debugging a UMDF version 1 driver on older versions of Windows, you can still use the same techniques with a UMDF version 2 driver running on current versions of Windows.

**Note**  This video describes the debugger extension commands in Wudfext.dll, which you can use to debug UMDF version 1 drivers only. To debug UMDF drivers starting in UMDF version 2.0, you must instead use the Wdfkd.dll debugger extension library. There are equivalents in Wdfkd.dll for all of the extensions in Wudfext.dll. For more info, see [Summary of Debugger Extensions in Wudfext.dll](using-umdf-debugger-extensions.md) and [Summary of Debugger Extensions in Wdfkd.dll](debugger-extensions-for-kmdf-drivers.md).

 

For more information about debugging UMDF, see the topics listed in [Debugging WDF Drivers](accessing-umdf-metadata-in-wer-reports.md).

## Prerequisites


To get the most from this content you should have working knowledge of UMDF and the Debugging Tools for Windows. Because each session builds on the previous one, we recommend that you view these demonstrations in the order listed.

## Basics and setup


Discusses use of the WDK samples and the OSR USB-FX2 Learning Kit.

>[!VIDEO aa2cf126-82e5-4c61-9d15-b39fa201c9dd]

In this video, you'll learn about UMDF debugging basics, including preparing your test machine, using the Devcon tool to install the UMDF Echo sample driver, using WdfVerifier to identify the host process hosting a given UMDF driver, and using WdfVerifier to attach the host process to the debugger in time to debug initialization code. This video also shows how you can list running host processes in Task Manager, and view running drivers in Device Manager.

## Examining the object hierarchy with debugger extensions

> [!VIDEO 640387ac-4906-4508-87b7-3115e613065b]

In this part, you'll learn how to start debugging a UMDF driver. The video describes how to set up the OSR USB-FX2 driver sample and application sample so that three instances of the app send read, write, and device I/O control requests to the driver. You'll see how the requests flow first to the reflector, and then to the user mode driver host process. This video introduces the WDF object hierarchy for the FX2 driver sample, and discusses how to use the following UMDF debugger extensions to traverse the UMDF object hierarchy:

-   [**!wudfext.umdevstacks**](../debuggercmds/-wudfext-umdevstacks.md)
-   [**!wudfext.wudfdriverinfo**](../debuggercmds/-wudfext-wudfdriverinfo.md)
-   [**!wudfext.wudfdevice**](../debuggercmds/-wudfext-wudfdevice.md)
-   [**!wudfext.wudfdevicequeues**](../debuggercmds/-wudfext-wudfdevicequeues.md)

For UMDF 2, see [Summary of Debugger Extensions in Wdfkd.dll](debugger-extensions-for-kmdf-drivers.md), for example [**!wdfkd.wdfumdevstacks**](../debuggercmds/-wdfkd-wdfumdevstacks.md).

## Accessing framework USB objects

>[!VIDEO c1cc9214-53c1-44eb-abb9-9ec7d09c86aa]

Here, you'll learn how to examine the driver's framework USB objects. To do so, you'll navigate through the WDF object hiearchy to reach the USB pipe objects, USB interface objects, and USB I/O target objects.

##  I/O requests and queues

>[!VIDEO 39bf5762-4a67-48af-bc8d-e3a8d2622225]

In this video, you'll use the debugger to examine the driver's framework I/O request objects and framework queue objects.

## File objects and callback objects

>[!VIDEO ce0e1ede-2f67-4c1e-93b0-3ac508600d95]

In this part, you'll learn how to examine framework file objects as well as the driver's callback objects.

##  Tracking I/O requests sent by a UMDF driver

> [!VIDEO 1a5e90ce-29c4-45d9-8dd8-4254e56ba54f]

Here, you'll learn how to use the App Verifier tool to help you debug. You'll also learn how to debug driver initialization code, and how to track requests sent by a UMDF driver to the kernel stack below.

##  Driver does not complete an I/O request

> [!VIDEO df5f6cc5-4993-474e-b555-e98d1f9ccba9]

In the final video, you'll investigate a case when a UMDF driver does not complete a request it received, and you'll learn about the framework's object tracking and reference tracking capabilities.

 

