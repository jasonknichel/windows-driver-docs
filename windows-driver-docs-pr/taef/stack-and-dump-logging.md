---
title: Stack and Dump Logging
description: Stack and Dump Logging
ms.date: 04/20/2017
ms.topic: concept-article
---

# Stack and Dump Logging


## <span id="Using__stacktraceonerror_and__minidumponerror_switches"></span><span id="using__stacktraceonerror_and__minidumponerror_switches"></span><span id="USING__STACKTRACEONERROR_AND__MINIDUMPONERROR_SWITCHES"></span>Using /stacktraceonerror and /minidumponerror switches


There are two ways you can capture stack trace and mini dumps from your tests. The easiest is 'onerror' mode. When you run your tests, supply te '/stacktraceonerror' and/or '/minidumponerror' switches. Then, if you hit a failure, Logger will capture the stack trace and/or mini dump for you in the default format.

The other method to capture stack trace and mini dumps is to use the APIs which are described below.

## <span id="using_wexdebug.h_functionality_to_capture_stack_traces_and_mini_dumps"></span><span id="USING_WEXDEBUG.H_FUNCTIONALITY_TO_CAPTURE_STACK_TRACES_AND_MINI_DUMPS"></span>Using WexDebug.h functionality to capture stack traces and mini dumps


WexDebug.h provides APIs for capturing call stack traces and mini dumps.

### <span id="Call_SaveDump_API_to_save_a_mini_dump."></span><span id="call_savedump_api_to_save_a_mini_dump."></span><span id="CALL_SAVEDUMP_API_TO_SAVE_A_MINI_DUMP."></span>Call SaveDump API to save a mini dump.

This API takes an optional DWORD parameter (which is a dump type flag or flag combination) and a string reference in which it returns you a string containing a file name and path to the saved dump file. The file name is automatically generated by the API and is based on the current date and time.

The optional dump type parameter specifies what the taken mini dump should contain. It also specifies whether the dump will be saved in a dmp or cab file, and, in the case of cab files, whether the symbols will be saved along with the dump. If the optional parameter is omitted, default settings are used.

Example (save dump into a cab along with its pdbs):

```cpp
NoThrowString savedDumpFilePath;
HRESULT hr = Debug::SaveDump(MiniDumpFormat::WriteCab | MiniDumpFormat::WriteCabSecondaryFiles, savedDumpFilePath);
```

Note, that saving a dump into a cab file takes longer than saving ordinary dump; attaching symbol files takes even longer.

### <span id="Call_GetStack_API_to_obtain_a_call_stack_trace."></span><span id="call_getstack_api_to_obtain_a_call_stack_trace."></span><span id="CALL_GETSTACK_API_TO_OBTAIN_A_CALL_STACK_TRACE."></span>Call GetStack API to obtain a call stack trace.

This API takes an optional DWORD parameter (which is a type flag or flag combination) and a string reference in which it returns you a string containing the call stack trace for the current context.

The optional stack type parameter specifies what the stack trace should contain. If the optional parameter is omitted, default settings are used.

Example:

```cpp
NoThrowString stackText;
HRESULT hr = Debug::GetStack(CallStackFormat::ColumnNames | CallStackFormat::FrameAddress |
                             CallStackFormat::SourceLine, stackText);
```

Correlation of stack option flags to debugger commands. If you use windbg family of debuggers the following approximate correlation list may come in handy:


| Debugger Syntax |          Corresponding Flags          |
|-----------------|---------------------------------------|
|        k        |     CallStackFormat::ColumnNames      |
|       kv        |   k + CallStackFormat::FunctionInfo   |
|     kp / kP     |    k + CallStackFormat::Parameters    |
|       kn        |   k + CallStackFormat::FrameNumbers   |
|       kf        | k + CallStackFormat::FrameMemoryUsage |

## <span id="Technical_Reference"></span><span id="technical_reference"></span><span id="TECHNICAL_REFERENCE"></span>Technical Reference


If you are interested in more information about the dump and stack optional parameters, please refer to the documentation provided with [Debugging Tools for Windows](../debugger/index.md). For documentation on the 'dump flags' see the [DEBUG\_FORMAT\_XXX](../debugger/debug-format-xxx.md). For documentation on the 'stack flags' please see the [OutputStackTrace](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol5-outputstacktraceex).
