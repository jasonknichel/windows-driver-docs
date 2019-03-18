---
title: StorPortBuildIo rule (storport)
description: This rule verifies that if the StorPort miniport's StorPortBuildIo routine returns FALSE, the SRB in question is not passed to StartIo.
ms.assetid: C35954F9-9C59-408B-BF80-2B8DCD328F9C
ms.date: 05/21/2018
keywords: ["StorPortBuildIo rule (storport)"]
topic_type:
- apiref
api_name:
- StorPortBuildIo
api_type:
- NA
ms.localizationpriority: medium
---

# StorPortBuildIo rule (storport)


This rule verifies that if the StorPort miniport's **StorPortBuildIo** routine returns **FALSE**, the SRB in question is not passed to **StartIo**. (In such cases, the miniport driver must complete the SRB by calling [**StorPortNotification**](https://msdn.microsoft.com/library/windows/hardware/ff567433) with a notification type of **RequestComplete** from **StorPortBuildIo** or someplace else).

> [!NOTE]
> This rule is testing StorPort's correct operation, not the miniport's.

 

|              |          |
|--------------|----------|
| Driver model | Storport |

How to test
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">At compile time</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Run <a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a> and specify the <strong>StorPortBuildIo</strong> rule.</p>
Use the following steps to run an analysis of your code:
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">Prepare your code (use role type declarations).</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Run Static Driver Verifier.</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">View and analyze the results.</a></li>
</ol>
<p>For more information, see <a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">Using Static Driver Verifier to Find Defects in Drivers</a>.</p></td>
</tr>
</tbody>
</table>

 

 




