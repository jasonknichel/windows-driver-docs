---
title: Understanding Static Driver Verifier
description: Understanding Static Driver Verifier
keywords:
- Static Driver Verifier WDK , about Static Driver Verifier
- StaticDV WDK , about Static Driver Verifier
- SDV WDK , about Static Driver Verifier
ms.date: 07/02/2024
ms.topic: concept-article
---

# Understanding Static Driver Verifier

To write a robust driver that complies with the Windows Driver Model (WDM) or the Kernel Mode Driver Framework (KMDF), NDIS, or Storport, you must have expertise and understand how the driver interacts with the I/O manager. Testing these drivers is equally tricky.

Developing solid drivers can be challenging for the following reasons:

- Drivers are asynchronous, even on single-processor machines.

- Drivers are massively reentrant.

- Drivers use many obscure rules.

- Driver models are evolutionary and age over time.

Testing device drivers is limited by the following reasons:

- *Observation*. You cannot observe an error in the interaction between the driver and the operating system. Drivers can violate implicit usage rules, resulting in a crash or improper behavior, but it is difficult to detect the root cause of an error when developing and testing drivers.

- *Control*. Drivers that work correctly under normal circumstances can have subtle errors that occur only in exceptional situations, such as when a driver below it in the stack fails an IRP. Such situations are hard to exercise, so traditional testing does not adequately detect the error paths through the driver code.

SDV enhances both the observation and control that you have when you test drivers. By defining rules for the proper use of WDM, KMDF, NDIS, and Storport functions and monitoring the driver's compliance with those rules, SDV improves your ability to observe errors. For example, the WDM rule [LowerDriverReturn](./wdm-lowerdriverreturn.md) specifies that, under certain circumstances, a driver's dispatch routine should always return the value that was returned by the lower driver in the stack.

SDV also increases control by providing:

- A hostile model of the driver's environment, where several worst-case scenarios (such as operating system calls continually failing) can happen.

- Powerful static analysis (called *model checking*) that systematically explores all possible execution paths in the driver.

SDV is an essential unit-testing tool for device drivers. It places a driver in a hostile environment and systematically tests code paths through the driver by looking for violations of driver model usage rules.

> [!IMPORTANT]
> SDV is no longer supported and SDV is not available in Windows 24H2 WDK or EWDK releases. It is not available in WDKs newer than build 26017, and is not included in the Windows 24H2 RTM WDK.
> SDV can still be used by downloading the Windows 11, version 22H2 EWDK (released October 24, 2023) with Visual Studio build tools 17.1.5 from [Download the Windows Driver Kit (WDK)](../download-the-wdk.md). Only the use of the Enterprise WDK to run SDV is recommended. Using older versions of the standard WDK in conjunction with recent releases of Visual Studio is not recommended, as this will likely result in analysis failures. <br>
> Going forward, CodeQL will be the primary static analysis tool for drivers. CodeQL provides a powerful query language that treats code as a database to be queried, making it simple to write queries for specific behaviors, patterns, and more.
> For more information about using CodeQL, see [CodeQL and the Static Tools Logo Test](static-tools-and-codeql.md).
