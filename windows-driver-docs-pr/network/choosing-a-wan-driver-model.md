---
title: WAN Driver Models
description: Learn about WAN driver models, and learn how to choose between NDIS WAN and CoNDIS WAN.
ms.date: 01/31/2025
---

# WAN driver models

Microsoft Windows 2000 and later operating systems support two WAN driver models: NDIS WAN and CoNDIS WAN.

## NDIS WAN

NDIS WAN miniport drivers are built on the NDIS model for connectionless miniport drivers. NDIS WAN miniport drivers aren't supported for NDIS version 5.0 and later drivers. New drivers should be based on the CoNDIS WAN driver architecture.

## CoNDIS WAN

CoNDIS WAN drivers are built on the connection-oriented NDIS (CoNDIS) driver model. CoNDIS WAN miniport drivers and miniport call managers (MCMs) can:

- Call the same NDIS functions that non-WAN connection-oriented miniport drivers call.

- Export the same set of *MiniportXxx* functions that non-WAN connection-oriented miniport drivers export.

- Provide additional WAN-specific capabilities.

For more information about CoNDIS drivers, see [Connection-Oriented NDIS](connection-oriented-ndis.md).

If you're writing a new WAN driver, we recommend that you use the CoNDIS WAN model.

Microsoft will continue to support existing NDIS WAN miniport drivers. You don't have to write CoNDIS drivers for old hardware.

The following articles describe the primary advantages of using the CoNDIS WAN model:

- [CoNDIS WAN Is More Flexible](condis-wan-is-more-flexible.md)

- [CoNDIS WAN Is Less Complex](condis-wan-is-less-complex.md)

- [Other Benefits of CoNDIS WAN](other-benefits-of-condis-wan.md)

- [Other NDIS Features Available to CoNDIS WAN Drivers](other-ndis-features-available-to-condis-wan-drivers.md)

