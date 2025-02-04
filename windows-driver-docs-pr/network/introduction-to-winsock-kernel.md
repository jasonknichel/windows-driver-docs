---
title: Introduction to Winsock Kernel
description: Learn how to use Winsock Kernel to perform network I/O operations.
ms.date: 01/31/2025
---

# Introduction to Winsock Kernel

Winsock Kernel (WSK) is a kernel-mode [Network Programming Interface (NPI)](network-programming-interface.md). With WSK, kernel-mode software modules can perform network I/O operations using the same socket programming concepts that are supported by user-mode Winsock2. The WSK NPI supports familiar socket operations such as socket creation, binding, connection establishment, and data transfers (send and receive). However, while WSK NPI supports most of the same socket programming concepts as user-mode Winsock2, WSK NPI is a completely new and different interface with unique characteristics such as asynchronous I/O that uses IRPs and event callbacks to enhance performance.

Kernel-mode network modules targeted for Windows Vista and later versions of Microsoft Windows should use WSK instead of [TDI drivers](/previous-versions/windows/hardware/network/ff565094(v=vs.85)) because WSK provides improved performance and easier programming. Filter drivers should implement the [Windows Filtering Platform](introduction-to-windows-filtering-platform-callout-drivers.md) on Windows Vista, and TDI clients should implement WSK.

> [!NOTE]
> TDI isn't supported in Microsoft Windows versions after Windows Vista. Use [Windows Filtering Platform](introduction-to-windows-filtering-platform-callout-drivers.md) or [Winsock Kernel](/windows-hardware/drivers/ddi/_netvista/#winsock-kernel-wsk) instead.
