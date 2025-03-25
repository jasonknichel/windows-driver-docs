---
title: About GPUView
description: About GPUView
keywords:
- GPUView, driver development
- GPUView, performance analysis
- CPU activity, GPU activity, performance analysis
ms.date: 01/06/2025
ms.topic: concept-article
---

# About GPUView

GPUView (*GPUView.exe*) is a performance analysis tool that helps developers analyze GPU and CPU activity on Windows systems. It's useful for diagnosing performance issues in graphics-intensive applications, such as games or multimedia software. It's [installed with the Windows Performance Toolkit (WPT)](installing-gpuview.md).

* Video core developers can use GPUView to determine the performance of the GPU and CPU regarding DMA buffer processing, and all other video processing, on the video hardware.
* Developers and testers can use GPUView to show different kinds of events that might lead to unusual conditions like glitches, preparation delays, and poor synchronization.

GPUView reads logged video and kernel events from an [event trace log](/windows-hardware/drivers/devtest/trace-log) (.etl) file and presents the data graphically to the user.

## Quick start for using GPUView

To use GPUView, you first need to generate a trace. To do so:

1. Open a command prompt with administrative privilege:

   * Type "command prompt" in the Start menu search box.
   * Right-click the command prompt icon and select Run as Administrator.

1. In the elevated command prompt, navigate to the GPUView directory and type the following command:

   ``` Log.cmd ```

1. Reproduce the performance issue (no more than 30 seconds to 1 minute). Then retype the same command:

   ``` Log.cmd ```

   This command generates several Event Tracing for Windows (\*.ETL) files. These various streams are all merged together into a single file called *Merged.etl*, which is what GPUView reads.

1. Use GPUView to view the resulting *Merged.ETL* file.

Some examples of logged events are:

* All CPU context switches, including the stack trace and the reason for switching.
* All kernel mode enters and exits and the stack trace.
* All GPU events as recorded by the DirectX Graphics Kernel, including all command buffer submissions, and resource creation, destruction, lock, and bind events.
* Events reported by the graphics driver, such as command buffer start and end times, and vertical synchronization intervals for each adapter.
* Many other system events that can affect performance, such as page faults.

You can also read ETL files with [XPerf](/windows-hardware/test/wpt/xperf-command-line-reference); however, it doesn't understand any of the GPU-specific events. Because these log files can be relatively large, you can use the `Log m` command instead, which skips many of the high frequency events.

More information can be found on Matthew Fisher's site, [Matt's Webcorner](https://graphics.stanford.edu/~mdfisher/GPUView.html), where he talks about creating GPUView.
