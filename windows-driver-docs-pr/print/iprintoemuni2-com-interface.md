---
title: IPrintOemUni2 COM Interface
description: IPrintOemUni2 COM Interface
keywords:
- IPrintOemUni2
ms.date: 07/14/2023
ms.topic: reference
---

# IPrintOemUni2 COM Interface

[!include[Print Support Apps](../includes/print-support-apps.md)]

The `IPrintOemUni2` COM interface contains all the methods of, and extends the capabilities of, the [IPrintOemUni COM Interface](iprintoemuni-com-interface.md).

The following table lists and describes all of the methods provided by the `IPrintOemUni2` interface. Rendering plug-ins must define all the listed methods. If a method isn't needed, it can return E_NOTIMPL.

| Method | Description |
|--|--|
| [**IPrintOemUni2::WritePrinter**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni2-writeprinter) | Enables a plug-in to capture all output data generated by a Unidrv driver. |

For more information, see [Implementing Printer Driver COM Interfaces](implementing-printer-driver-com-interfaces.md).
