---
title: Example 5 Formatting Real-Time Trace Sessions
description: Example 5 Formatting Real-Time Trace Sessions
keywords:
- Tracefmt WDK , real-time trace sessions
- real-time trace sessions WDK
ms.date: 04/20/2017
ms.topic: concept-article
---

# Example 5: Formatting Real-Time Trace Sessions


You can use Tracefmt to format trace messages from real-time trace sessions in addition to trace log files.

The following sequence of commands uses [Tracelog](tracelog.md) and Tracefmt. The first command uses Tracelog to start a real-time trace session with the Tracedrv sample trace provider. [TraceDrv](https://github.com/Microsoft/Windows-driver-samples/tree/main/general/tracing/tracedriver), a sample driver that was designed for software tracing, is available in the [Windows driver samples](https://github.com/Microsoft/Windows-driver-samples) repository on GitHub.

```
tracelog -start MyTrace -guid tracedrv.ctl -flag 1 -rt
```

This command starts a trace session called MyTrace. It uses the -**guid** parameter to identify the trace provider, Tracedrv.sys, by using its control GUID file, tracedrv.ctl. It uses the **-flag** parameter to set the [trace flag](trace-flags.md) value to **1**. It uses the **-rt** parameter to start a trace session that delivers messages directly to a trace consumer, such as Tracefmt. Without the **-rt** parameter, the trace provider would send messages only to a log file.

The next command uses Tracefmt to format the messages generated by Tracedrv during the MyTrace trace session.

```
tracefmt -rt MyTrace -p c:\tracing -o mytrace.txt
```

This Tracefmt command uses the **-rt** parameter to identify the real-time trace session, MyTrace, and the **-p** parameter to specify the directory in which the TMF file for Tracedrv.sys is located. The **-o** parameter directs the output to the mytrace.txt file in the local directory.

In response to this command, Tracefmt prepares to format the trace messages in real time. It displays the following status messages, but does not return to the command prompt:

```
c:\tracetools>tracefmt -rt mytrace -display -o mytrace.txt
Setting RealTime mode for  mytrace
Getting guids from c:\tracetools\default.tmf
```

The following Tracelog command stops the MyTrace trace session. You must type the command in a different Command Prompt window.

```
tracelog -stop mytrace
```

When the trace session stops, Tracefmt reports that it wrote the trace messages to the output file, and then returns to the command prompt.

```
Event traces dumped to mytrace.txt
Event Summary dumped to mytrace.txt.sum
```

