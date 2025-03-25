---
title: Introduction to Windows Filtering Platform Callout Drivers
description: A callout driver creates callouts which extend the Windows Filtering Platform by processing TCP/IP network data in more advanced ways than basic filtering can handle.
ms.date: 09/27/2024
ms.topic: concept-article
---

# Introduction to Windows Filtering Platform (WFP) Callout Drivers


This section introduces WFP [callout drivers](callout-driver.md). 

For more information about the WFP, see the [Windows Filtering Platform](/windows/win32/fwp/windows-filtering-platform-start-page) documentation in the Microsoft Windows SDK.

For WFP reference information, see [Windows Filtering Platform Callout Drivers](/windows-hardware/drivers/ddi/_netvista/#windows-filtering-platform-callout-drivers).

### Purpose of Callout Drivers

A callout driver implements one or more [callouts](callout.md). Callouts extend the capabilities of the Windows Filtering Platform by processing TCP/IP-based network data in ways that are beyond the scope of the simple filtering functionality. Callouts are typically used to do the following tasks:

<a href="" id="deep-inspection-------"></a>**Deep Inspection**   
Perform complex inspection of the network data to determine which data should be blocked, which data should be permitted, and which data should be passed to another filter. An antivirus product, for example, could look for virus signatures.

<a href="" id="packet-modification-------"></a>**Packet Modification**   
Perform modification and reinjection of the network packet headers or data, or both. A network address translation (NAT) product, for example, could modify the headers on IPv4 packets.

<a href="" id="stream-modification-------"></a>**Stream Modification**   
Perform modification and reinjection of the network data in a stream. A parental control product, for example, could remove or replace specific words or phrases in a data stream.

<a href="" id="data-logging-------"></a>**Data Logging**   
Log of network traffic data. A network monitoring product, for example, could count the number of data packets that are discarded for a specific reason.

In addition to processing network data, callout drivers can perform other Windows Filtering Platform management tasks, such as adding filters to the base filtering engine. For more information about other tasks that a callout driver can perform, see [Calling Other Windows Filtering Platform Functions](calling-other-windows-filtering-platform-functions.md).

 

