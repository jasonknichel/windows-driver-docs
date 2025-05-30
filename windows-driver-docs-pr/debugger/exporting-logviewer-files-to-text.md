---
title: Exporting LogViewer Files to Text
description: Exporting LogViewer Files to Text
keywords: ["LogViewer, exporting files to text"]
ms.date: 05/23/2017
ms.topic: how-to
---

# Exporting LogViewer Files to Text


## <span id="ddk_exporting_logviewer_files_to_text_dtoolq"></span><span id="DDK_EXPORTING_LOGVIEWER_FILES_TO_TEXT_DTOOLQ"></span>


A powerful way to manipulate log files is to export them to text. This allows you to find specific parameter values by using the Find facility of any text editor. Although it is possible for a text file to be generated by Logger directly, you will have more flexibility if you use LogViewer to filter the function calls or add aliasing, and then export this information into a text file.

To create a text file from an .lgv file, open the file in LogViewer, and then select **File | Export to Text**. In the dialog box, choose a file name and location.

There are several options at the bottom of the dialog box:

<span id="Export_Diff_Information"></span><span id="export_diff_information"></span><span id="EXPORT_DIFF_INFORMATION"></span>**Export Diff Information**  
This option will alias all pointers, handle values, and other values that change from execution to execution. Instead of outputting the actual value of a pointer (for example, "0x00123FA2"), LogViewer will output "Pointer." Similarly, handles will be aliased as "HeapHandle1" or some other value that will not register as a *diff* when the two files are compared using a differencing tool.

<span id="Include_Non-Visible_Rows"></span><span id="include_non-visible_rows"></span><span id="INCLUDE_NON-VISIBLE_ROWS"></span>**Include Non-Visible Rows**  
This option disables whatever filters are currently applied to the view while exporting.

<span id="Create_a_Separate_File_For_Each_Thread"></span><span id="create_a_separate_file_for_each_thread"></span><span id="CREATE_A_SEPARATE_FILE_FOR_EACH_THREAD"></span>**Create a Separate File For Each Thread**  
This option splits up the text file by thread, making it easier to follow a thread of execution. This is useful if you intend to "diff" two instances of execution.

<span id="Export_Range"></span><span id="export_range"></span><span id="EXPORT_RANGE"></span>**Export Range**  
This option specifies the range of rows to export.

 

 
