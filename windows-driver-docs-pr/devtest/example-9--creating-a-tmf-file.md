---
title: Example 9 Creating a TMF File
description: Example 9 Creating a TMF file
keywords:
- Tracefmt WDK , TMF files
- TMF files WDK , Tracefmt
ms.date: 04/20/2017
ms.topic: concept-article
---

# Example 9: Creating a TMF file


The following command directs Tracefmt to format and display the trace messages in Tracedrv.etl, a trace log generated by Tracedrv. [TraceDrv](https://github.com/Microsoft/Windows-driver-samples/tree/main/general/tracing/tracedriver), a sample driver that was designed for software tracing, is available in the [Windows driver samples](https://github.com/Microsoft/Windows-driver-samples) repository on GitHub.

The command includes the **-i** parameter, which directs Tracefmt to create a TMF file for Tracedrv.

```
tracefmt d:\tracedrv\tracedrv.etl -i d:\tracedrv\tracedrv.sys -r d:\tracedrv 
-p d:\tracedrv\tmfs -o d:\tracedrv\tracedrv1.txt -v
```

The command uses the **-i** parameter to indicate the fully qualified path to the image file for Tracedrv, Tracedrv.sys, in the WDK.

```
-i d:\tracedrv\tracedrv.sys
```

It uses the **-r** parameter to indicate the fully qualified path to the full version of the PDB symbol file for Tracedrv, Tracedrv.pdb. Notice that you specify a path with this parameter, but not a file name. Tracefmt finds the correct version of the symbol file based on the image file specified by **-i**.

```
-r d:\tracedrv
```

The command uses the **-p** parameter to direct Tracefmt to place the TMF file that it creates for Tracedrv in the **d:\\tracedrv\\tmfs** directory.

```
-p d:\tracedrv\tmfs
```

The command uses the **-o** parameter to direct Tracefmt to place the output file of formatted trace messages in the **d:\\tracedrv\\tracedrv1.txt** file. This parameter also places the summary file in the same directory with the Tracedrv.txt.sum file name.

```
-o d:\tracedrv\tracedrv1.txt
```

The **-v** parameter requests detailed (verbose) messages.

In response to this command, Tracefmt looks for and finds the PDB file for Tracedrv.sys in the d:\\tracedrv directory. It extracts the trace message formatting instructions from the PDB file and stores them in a TMF file, as shown in the statement in bold type in the output that follows. The name of the TMF file is the [message GUID](message-guid.md) of the trace provider in Tracedrv. Tracefmt also creates a trace message control (TMC) file and places it in the same directory.

After Tracefmt creates the TMF file, it reads the file to find the formatting instructions for the trace messages in the Tracedrv.etl trace log. It begins by looking in the Default.tmf file and finds the TMf file that it created in the d:\\tracedrv\\tmfs directory.

Before it formats the data, Tracefmt displays data about the trace log. The data begins with the **Logfile d:\\tracedrv\\tracedrv.etl** statement.

The final statements in the output show that Tracefmt successfully formatted the 13 events in the trace log and created the Tracedrv1.txt and Tracedrv1.txt.sum files.

```
Setting log file to: d:\tracedrv\tracedrv.etl

Searching for matching PDB to d:\tracedrv\tracedrv.sys
Current Symbol Search Path = d:\tracedrv

Extracting TMF files out of found PDB files
DBGHELP: d:\tracedrv\tracedrv.pdb - OK
tracefmt : info BNP0000: WPPFMT generating d:\tracedrv\tmfs\1606d1a7-1682-57d1-65f7-36693800e096.tmf for d:\tracedrv\tracedrv.pdb
tracefmt : info BNP0000: WPPFMT generating d:\tracedrv\tmfs\d58c126f-b309-11d1-969e-0000f875a5bc.tmc for d:\tracedrv\tracedrv.pdb
Examining C:\WinDDK\5066\tools\tracing\i386\default.tmf for message formats,  3 found.
Searching for TMF files on path: d:\tracedrv\tmfs
Logfile d:\tracedrv\tracedrv.etl:
        OS version              5.1.2600  (Currently running on 5.1.2600)
        Start Time              2005-06-10-14:25:30.827
        End Time                2005-06-10-14:26:14.371
        Timezone is             Pacific Standard Time (Bias is 480mins)
        BufferSize              8192 B
        Maximum File Size       0 MB
        Buffers  Written        2
        Logger Mode Settings    (0) Logfile Mode is not set
        ProcessorCount          1
06/10/2005-21:25:45.539 ::        1: Filled=     696, Lost=  0 TotalLost= 0

Processing completed   Buffers: 1, Events: 13, EventsLost: 0 :: Format Errors: 0, Unknowns: 0

Event traces dumped to d:\tracedrv\tracedrv1.txt
Event Summary dumped to d:\tracedrv\tracedrv1.txt.sum
```

The primary output of this Tracefmt run is Tracedrv.txt, a text file that contains the formatted version of the trace messages in Tracedrv.etl. The following text shows the contents of Tracedrv.txt .

```
EventTrace
[0]0338.0E40::06/10/2005-14:25:43.968 [tracedrv]IOCTL = 1
[0]0338.0E40::06/10/2005-14:25:43.968 [tracedrv]Hello, 1 Hi
[0]0338.0E40::06/10/2005-14:25:43.968 [tracedrv]Hello, 2 Hi
[0]0338.0E40::06/10/2005-14:25:43.968 [tracedrv]Hello, 3 Hi
[0]0338.0E40::06/10/2005-14:25:43.968 [tracedrv]Machine State :: Offline
[0]0338.0E40::06/10/2005-14:25:43.968 [tracedrv]Function Return=0x8000000f(STATUS_DEVICE_POWERED_OFF)
[0]0338.0E40::06/10/2005-14:25:45.539 [tracedrv]IOCTL = 2
[0]0338.0E40::06/10/2005-14:25:45.539 [tracedrv]Hello, 1 Hi
[0]0338.0E40::06/10/2005-14:25:45.539 [tracedrv]Hello, 2 Hi
[0]0338.0E40::06/10/2005-14:25:45.539 [tracedrv]Hello, 3 Hi
[0]0338.0E40::06/10/2005-14:25:45.539 [tracedrv]Machine State :: Offline
[0]0338.0E40::06/10/2005-14:25:45.539 [tracedrv]Function Return=0x8000000f(STATUS_DEVICE_POWERED_OFF)
```

