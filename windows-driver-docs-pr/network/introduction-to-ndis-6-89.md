---
title: Introduction to NDIS 6.89
description: This section introduces NDIS 6.89 and describes changes from NDIS 6.88. NDIS 6.89 is included in Windows 11, version 24H2.
ms.date: 01/31/2025
---

# Introduction to NDIS 6.89

This topic introduces Network Driver Interface Specification (NDIS) 6.89 and describes its major design additions. NDIS 6.89 is included in Windows 11, version 24H2 and Windows Server 2022 and later.

NDIS 6.89 is a minor version update to NDIS 6.88. For more information about porting NDIS 6.x drivers to NDIS 6.89, see [Porting NDIS 6.x drivers to NDIS 6.89](porting-ndis-6-x-drivers-to-ndis-6-89.md).

## Feature updates

NDIS 6.89 adds support for [UDP Receive Segment Coalescing Offload (URO)](udp-rsc-offload.md). This hardware offload enables NICs to coalesce UDP receive segments. NICs can combine UDP datagrams from the same flow that match a set of rules into a logically contiguous buffer. These combined datagrams are then indicated to the Windows networking stack as a single large packet. Coalescing UDP datagrams reduces the CPU cost to process packets in high-bandwidth flows, resulting in higher throughput and fewer cycles per byte.

## Implementing an NDIS 6.89 driver

An NDIS 6.89 driver must follow the requirements that are defined in [Implementing an NDIS 6.30 driver](implementing-an-ndis-6-30-driver.md).

In addition, an NDIS 6.89 driver must be compliant with the following requirements:

* An NDIS 6.89 driver must report the correct NDIS version when it registers with NDIS.
   
  * You must update the major and minor NDIS version number in the NDIS_Xxx_DRIVER_CHARACTERISTICS structure to support NDIS 6.89. The MajorNdisVersion member must contain 6 and the MinorNdisVersion member must contain 89. This requirement applies to miniport, protocol, and filter drivers. You must also update the version information for the compiler (see [Compiling an NDIS 6.89 driver](#compiling-an-ndis-689-driver)).

  * Miniport drivers must set the **Header** member of [**NDIS_MINIPORT_DRIVER_CHARACTERISTICS**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics): Set **Revision** to NDIS_MINIPORT_DRIVER_CHARACTERISTICS_REVISION_3 and **Size** to NDIS_SIZEOF_MINIPORT_DRIVER_CHARACTERISTICS_REVISION_3. 

  * Filter drivers must set the **Header** member of [**NDIS_FILTER_DRIVER_CHARACTERISTICS**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_driver_characteristics): Set **Revision** to NDIS_FILTER_CHARACTERISTICS_REVISION_3 and **Size** to NDIS_SIZEOF_FILTER_DRIVER_CHARACTERISTICS_REVISION_3. 

  * Protocol drivers must set the **Header** member of [**NDIS_PROTOCOL_DRIVER_CHARACTERISTICS**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_driver_characteristics): Set **Revision** to NDIS_PROTOCOL_CHARACTERISTICS_REVISION_2 and **Size** to NDIS_SIZEOF_PROTOCOL _DRIVER_CHARACTERISTICS_REVISION_2.

- NDIS 6.89 miniport drivers for Windows 11, version 24H2 and Windows Server 2022 and later must use the NDIS 6.89 versions of data structures.

## Compiling an NDIS 6.89 driver

The WDK for Windows Server 2022 supports header versioning. Header versioning makes sure that NDIS 6.89 drivers use the appropriate NDIS 6.89 data structures at compile time.

Add the following compiler settings to the Visual Studio project for your driver:

- For a miniport driver, add `NDIS689_MINIPORT=1`.
- For a filter or protocol driver, add `NDIS689=1`.

For information on building a driver with the Windows Server 2022 release of the WDK, see [Building a Driver](../develop/building-a-driver.md).
