---
title: Reporting a NIC's LSOV2 TCP-Packet-Segmentation Capabilities
description: Reporting a NIC's LSOV2 TCP-Packet-Segmentation Capabilities
keywords:
- LSOV2 WDK networking
- large TCP packet segmentation WDK networking
- segmentation of large TCP packets WDK networking
- task offload WDK TCP/IP transport , LSOV1 and LSOV2
ms.date: 04/20/2017
ms.topic: concept-article
---

# Reporting a NIC's LSOV2 TCP-Packet-Segmentation Capabilities





An NDIS miniport driver specifies the current large send offload version 2 (LSOV2) TCP-packet-segmentation configuration of a NIC in an [**NDIS\_TCP\_LARGE\_SEND\_OFFLOAD\_V2**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2) structure.Miniport drivers must include the current LSOV2 configuration in the [**NDIS\_MINIPORT\_ADAPTER\_OFFLOAD\_ATTRIBUTES**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes) structure. Miniport drivers call the [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) function from the [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) function and pass in the information in NDIS\_MINIPORT\_ADAPTER\_OFFLOAD\_ATTRIBUTES.

Miniport drivers must report changes in the LSOV2 configuration, if any, in the [**NDIS\_STATUS\_TASK\_OFFLOAD\_CURRENT\_CONFIG**](./ndis-status-task-offload-current-config.md) status indication.

In response to a query of [OID\_TCP\_OFFLOAD\_CURRENT\_CONFIG](./oid-tcp-offload-current-config.md), NDIS includes the NDIS\_TCP\_LARGE\_SEND\_OFFLOAD\_V2 structure in the [**NDIS\_OFFLOAD**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload) structure that NDIS returns in the **InformationBuffer** member of the [**NDIS\_OID\_REQUEST**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request) structure. NDIS uses the information that the miniport driver provided.

We recommend that a miniport driver that supports LSOV2 hardware should also support LSOV1. This support will enable the TCP/IP transport to use LSOV1 if an NDIS 5.*x* intermediate driver is installed over a miniport adapter. For more information about LSOV1 capabilities, see [Reporting a NIC's LSOV1 TCP-Packet-Segmentation Capabilities](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md).

LSOV2 supports IPv4 and IPv6 packets. The miniport driver must specify the following information for both IPv4 and IPv6 in the [**NDIS\_TCP\_LARGE\_SEND\_OFFLOAD\_V2**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2) structure:

-   Encapsulation settings, in the **Encapsulation** member. For more information about this member, see the Remarks section in [**NDIS\_TCP\_LARGE\_SEND\_OFFLOAD\_V2**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2).

-   The maximum bytes of user data that the TCP/IP transport can pass to the miniport driver in a large TCP packet, in the **MaxOffLoadSize** member.

-   The minimum number of segments that a large TCP packet must be divisible by before the TCP/IP transport can offload it to a NIC for segmentation, in the **MinSegmentCount** member.

## Related topics


[Determining Task Offload Capabilities](determining-task-offload-capabilities.md)

 

