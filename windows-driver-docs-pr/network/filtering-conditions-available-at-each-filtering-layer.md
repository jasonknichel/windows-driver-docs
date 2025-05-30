---
title: Filtering conditions available at each filtering layer
description: This section describes filtering conditions available at each filtering layer.
keywords:
- Filtering conditions available at each filtering layer network drivers
ms.date: 11/08/2017
ms.topic: concept-article
---

# Filtering conditions available at each filtering layer

The filtering conditions that are available at each filtering layer are as follows.

> [!NOTE]
> The V4 and V6 suffixes at the end of the layer identifiers indicate whether the layer is located in the IPv4 network stack or in the IPv6 network stack.

<table>
<tr>
<th>Management filtering layer identifier</th>
<th>Available filtering conditions</th>
</tr>
<tr>
<td>
<p>FWPM_LAYER_INBOUND_IPPACKET_V4</p>
<p>FWPM_LAYER_INBOUND_IPPACKET_V4_DISCARD</p>
<p>FWPM_LAYER_INBOUND_IPPACKET_V6</p>
<p>FWPM_LAYER_INBOUND_IPPACKET_V6_DISCARD</p>
</td>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_IP_LOCAL_INTERFACE</p>
<p>FWPM_CONDITION_FLAGS</p>
<p>FWPM_CONDITION_INTERFACE_INDEX</p>
<p>FWPM_CONDITION_INTERFACE_TYPE</p>
<p>FWPM_CONDITION_SUB_INTERFACE_INDEX</p>
<p>FWPM_CONDITION_TUNNEL_TYPE</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_OUTBOUND_IPPACKET_V4</p>
<p>FWPM_LAYER_OUTBOUND_IPPACKET_V4_DISCARD</p>
<p>FWPM_LAYER_OUTBOUND_IPPACKET_V6</p>
<p>FWPM_LAYER_OUTBOUND_IPPACKET_V6_DISCARD</p>
</td>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_IP_LOCAL_INTERFACE</p>
<p>FWPM_CONDITION_FLAGS</p>
<p>FWPM_CONDITION_INTERFACE_INDEX</p>
<p>FWPM_CONDITION_INTERFACE_TYPE</p>
<p>FWPM_CONDITION_SUB_INTERFACE_INDEX</p>
<p>FWPM_CONDITION_TUNNEL_TYPE</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_IPFORWARD_V4</p>
<p>FWPM_LAYER_IPFORWARD_V4_DISCARD</p>
<p>FWPM_LAYER_IPFORWARD_V6</p>
<p>FWPM_LAYER_IPFORWARD_V6_DISCARD</p>
</td>
<td>
<p>FWPM_CONDITION_IP_SOURCE_ADDRESS</p>
<p>FWPM_CONDITION_IP_DESTINATION_ADDRESS</p>
<p>FWPM_CONDITION_IP_DESTINATION_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_IP_LOCAL_INTERFACE</p>
<p>FWPM_CONDITION_IP_FORWARD_INTERFACE</p>
<p>FWPM_CONDITION_FLAGS</p>
<p>FWPM_CONDITION_SOURCE_INTERFACE_INDEX</p>
<p>FWPM_CONDITION_SOURCE_SUB_INTERFACE_INDEX</p>
<p>FWPM_CONDITION_DESTINATION_INTERFACE_INDEX</p>
<p>FWPM_CONDITION_DESTINATION_SUB_INTERFACE_INDEX</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_INBOUND_TRANSPORT_V4</p>
<p>FWPM_LAYER_INBOUND_TRANSPORT_V4_DISCARD</p>
<p>FWPM_LAYER_INBOUND_TRANSPORT_V6</p>
<p>FWPM_LAYER_INBOUND_TRANSPORT_V6_DISCARD</p>
</td>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_IP_LOCAL_INTERFACE</p>
<p>FWPM_CONDITION_IP_PROTOCOL</p>
<p>FWPM_CONDITION_IP_LOCAL_PORT</p>
<p>FWPM_CONDITION_IP_REMOTE_PORT</p>
<p>FWPM_CONDITION_FLAGS</p>
<p>FWPM_CONDITION_INTERFACE_INDEX</p>
<p>FWPM_CONDITION_INTERFACE_TYPE</p>
<p>FWPM_CONDITION_SUB_INTERFACE_INDEX</p>
<p>FWPM_CONDITION_TUNNEL_TYPE</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_OUTBOUND_TRANSPORT_V4</p>
<p>FWPM_LAYER_OUTBOUND_TRANSPORT_V4_DISCARD</p>
<p>FWPM_LAYER_OUTBOUND_TRANSPORT_V6</p>
<p>FWPM_LAYER_OUTBOUND_TRANSPORT_V6_DISCARD</p>
</td>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_IP_DESTINATION_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_IP_LOCAL_INTERFACE</p>
<p>FWPM_CONDITION_IP_PROTOCOL</p>
<p>FWPM_CONDITION_IP_LOCAL_PORT</p>
<p>FWPM_CONDITION_IP_REMOTE_PORT</p>
<p>FWPM_CONDITION_FLAGS</p>
<p>FWPM_CONDITION_INTERFACE_INDEX</p>
<p>FWPM_CONDITION_INTERFACE_TYPE</p>
<p>FWPM_CONDITION_SUB_INTERFACE_INDEX</p>
<p>FWPM_CONDITION_TUNNEL_TYPE</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_STREAM_V4</p>
<p>FWPM_LAYER_STREAM_V4_DISCARD</p>
<p>FWPM_LAYER_STREAM_V6</p>
<p>FWPM_LAYER_STREAM_V6_DISCARD</p>
</td>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_IP_LOCAL_PORT</p>
<p>FWPM_CONDITION_IP_REMOTE_PORT</p>
<p>FWPM_CONDITION_FLAGS</p>
<p>FWPM_CONDITION_DIRECTION</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_DATAGRAM_DATA_V4</p>
<p>FWPM_LAYER_DATAGRAM_DATA_V4_DISCARD</p>
<p>FWPM_LAYER_DATAGRAM_DATA_V6</p>
<p>FWPM_LAYER_DATAGRAM_DATA_V6_DISCARD</p>
</td>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_IP_LOCAL_INTERFACE</p>
<p>FWPM_CONDITION_IP_PROTOCOL</p>
<p>FWPM_CONDITION_IP_LOCAL_PORT</p>
<p>FWPM_CONDITION_IP_REMOTE_PORT</p>
<p>FWPM_CONDITION_FLAGS</p>
<p>FWPM_CONDITION_DIRECTION</p>
<p>FWPM_CONDITION_INTERFACE_INDEX</p>
<p>FWPM_CONDITION_INTERFACE_TYPE</p>
<p>FWPM_CONDITION_SUB_INTERFACE_INDEX</p>
<p>FWPM_CONDITION_TUNNEL_TYPE</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_INBOUND_ICMP_ERROR_V4</p>
<p>FWPM_LAYER_INBOUND_ICMP_ERROR_V4_DISCARD</p>
<p>FWPM_LAYER_INBOUND_ICMP_ERROR_V6</p>
<p>FWPM_LAYER_INBOUND_ICMP_ERROR_V6_DISCARD</p>
</td>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS</p>
<p>FWPM_CONDITION_IP_LOCAL_INTERFACE</p>
<p>FWPM_CONDITION_IP_ARRIVAL_INTERFACE</p>
<p>FWPM_CONDITION_FLAGS</p>
<p>FWPM_CONDITION_ICMP_TYPE</p>
<p>FWPM_CONDITION_ICMP_CODE</p>
<p>FWPM_CONDITION_EMBEDDED_LOCAL_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_EMBEDDED_REMOTE_ADDRESS</p>
<p>FWPM_CONDITION_EMBEDDED_PROTOCOL</p>
<p>FWPM_CONDITION_EMBEDDED_LOCAL_PORT</p>
<p>FWPM_CONDITION_EMBEDDED_REMOTE_PORT</p>
<p>FWPM_CONDITION_ARRIVAL_INTERFACE_INDEX</p>
<p>FWPM_CONDITION_ARRIVAL_INTERFACE_TYPE</p>
<p>FWPM_CONDITION_SUB_INTERFACE_INDEX
       <p><b>Note</b>  In 
        Windows Vista, this flag was called FWPM_CONDITION_ARRIVAL_SUB_INTERFACE_INDEX. In Windows Vista with Service Pack 1 (SP1) and later, both names are valid.</p>
</p>
<p>FWPM_CONDITION_ARRIVAL_TUNNEL_TYPE</p>
<p>FWPM_CONDITION_INTERFACE_INDEX
       <p><b>Note</b>  In 
        Windows Vista, this flag was called FWPM_CONDITION_LOCAL_INTERFACE_INDEX. In Windows Vista with SP1 and later, both names are valid.</p>
</p>
<p>FWPM_CONDITION_INTERFACE_TYPE
       <p><b>Note</b>  In 
        Windows Vista, this flag was called FWPM_CONDITION_LOCAL_INTERFACE_TYPE. In Windows Vista with SP1 and later, both names are valid.</p>
</p>
<p>FWPM_CONDITION_TUNNEL_TYPE
       <p><b>Note</b>  In 
        Windows Vista, this flag was called FWPM_CONDITION_LOCAL_TUNNEL_TYPE. In Windows Vista with SP1 and later, both names are valid.</p>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_OUTBOUND_ICMP_ERROR_V4</p>
<p>FWPM_LAYER_OUTBOUND_ICMP_ERROR_V4_DISCARD</p>
<p>FWPM_LAYER_OUTBOUND_ICMP_ERROR_V6</p>
<p>FWPM_LAYER_OUTBOUND_ICMP_ERROR_V6_DISCARD</p>
</td>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_IP_LOCAL_INTERFACE</p>
<p>FWPM_CONDITION_FLAGS</p>
<p>FWPM_CONDITION_ICMP_TYPE</p>
<p>FWPM_CONDITION_ICMP_CODE</p>
<p>FWPM_CONDITION_INTERFACE_INDEX</p>
<p>FWPM_CONDITION_INTERFACE_TYPE</p>
<p>FWPM_CONDITION_SUB_INTERFACE_INDEX</p>
<p>FWPM_CONDITION_TUNNEL_TYPE</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V4</p>
<p>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V4_DISCARD</p>
<p>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V6</p>
<p>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V6_DISCARD</p>
</td>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_IP_LOCAL_INTERFACE</p>
<p>FWPM_CONDITION_IP_PROTOCOL</p>
<p>FWPM_CONDITION_IP_LOCAL_PORT</p>
<p>FWPM_CONDITION_FLAGS</p>
<p>FWPM_CONDITION_ALE_APP_ID</p>
<p>FWPM_CONDITION_ALE_USER_ID</p>
<p>FWPM_CONDITION_ALE_PROMISCUOUS_MODE</p>
<p>FWPM_CONDITION_INTERFACE_TYPE</p>
<p>FWPM_CONDITION_TUNNEL_TYPE</p>
<p>FWPM_CONDITION_ALE_PACKAGE_ID
</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_ALE_AUTH_LISTEN_V4</p>
<p>FWPM_LAYER_ALE_AUTH_LISTEN_V4_DISCARD</p>
<p>FWPM_LAYER_ALE_AUTH_LISTEN_V6</p>
<p>FWPM_LAYER_ALE_AUTH_LISTEN_V6_DISCARD</p>
</td>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_IP_LOCAL_INTERFACE</p>
<p>FWPM_CONDITION_IP_LOCAL_PORT</p>
<p>FWPM_CONDITION_FLAGS</p>
<p>FWPM_CONDITION_ALE_APP_ID</p>
<p>FWPM_CONDITION_ALE_USER_ID</p>
<p>FWPM_CONDITION_INTERFACE_TYPE</p>
<p>FWPM_CONDITION_TUNNEL_TYPE</p>
<p>FWPM_CONDITION_ALE_PACKAGE_ID
</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4</p>
<p>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</p>
<p>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6</p>
<p>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</p>
</td>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_IP_LOCAL_INTERFACE</p>
<p>FWPM_CONDITION_IP_PROTOCOL</p>
<p>FWPM_CONDITION_IP_LOCAL_PORT</p>
<p>FWPM_CONDITION_IP_REMOTE_PORT</p>
<p>FWPM_CONDITION_IP_ARRIVAL_INTERFACE</p>
<p>FWPM_CONDITION_FLAGS</p>
<p>FWPM_CONDITION_ALE_APP_ID</p>
<p>FWPM_CONDITION_ALE_USER_ID</p>
<p>FWPM_CONDITION_ALE_REMOTE_USER_ID</p>
<p>FWPM_CONDITION_ALE_REMOTE_MACHINE_ID</p>
<p>FWPM_CONDITION_ALE_SIO_FIREWALL_SYSTEM_PORT</p>
<p>FWPM_CONDITION_ALE_NAP_CONTEXT</p>
<p>FWPM_CONDITION_ARRIVAL_INTERFACE_INDEX</p>
<p>FWPM_CONDITION_ARRIVAL_INTERFACE_TYPE</p>
<p>FWPM_CONDITION_SUB_INTERFACE_INDEX
       <p><b>Note</b>  In 
        Windows Vista, this flag was called FWPM_CONDITION_ARRIVAL_SUB_INTERFACE_INDEX. In Windows Vista with SP1 and later, both names are valid.</p>
</p>
<p>FWPM_CONDITION_ARRIVAL_TUNNEL_TYPE</p>
<p>FWPM_CONDITION_INTERFACE_INDEX
       <p><b>Note</b>  In 
        Windows Vista, this flag was called FWPM_CONDITION_LOCAL_INTERFACE_INDEX. In Windows Vista with SP1 and later, both names are valid.</p>
</p>
<p>FWPM_CONDITION_INTERFACE_TYPE
       <p><b>Note</b>  In 
        Windows Vista, this flag was called FWPM_CONDITION_LOCAL_INTERFACE_TYPE. In Windows Vista with SP1 and later, both names are valid.</p>
</p>
<p>FWPM_CONDITION_TUNNEL_TYPE
       <p><b>Note</b>  In 
        Windows Vista, this flag was called FWPM_CONDITION_LOCAL_TUNNEL_TYPE. In Windows Vista with SP1 and later, both names are valid.</p>
</p>
<p>FWPM_CONDITION_ALE_PACKAGE_ID
</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_ALE_AUTH_CONNECT_V4</p>
<p>FWPM_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</p>
<p>FWPM_LAYER_ALE_AUTH_CONNECT_V6</p>
<p>FWPM_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</p>
</td>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_IP_DESTINATION_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_IP_LOCAL_INTERFACE</p>
<p>FWPM_CONDITION_IP_PROTOCOL</p>
<p>FWPM_CONDITION_IP_LOCAL_PORT</p>
<p>FWPM_CONDITION_IP_REMOTE_PORT</p>
<p>FWPM_CONDITION_FLAGS</p>
<p>FWPM_CONDITION_ALE_APP_ID</p>
<p>FWPM_CONDITION_ALE_USER_ID</p>
<p>FWPM_CONDITION_ALE_REMOTE_USER_ID</p>
<p>FWPM_CONDITION_ALE_REMOTE_MACHINE_ID</p>
<p>FWPM_CONDITION_INTERFACE_TYPE</p>
<p>FWPM_CONDITION_TUNNEL_TYPE</p>
<p>FWPM_CONDITION_ALE_PACKAGE_ID
</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4</p>
<p>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4_DISCARD</p>
<p>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6</p>
<p>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6_DISCARD</p>
</td>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_IP_DESTINATION_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_IP_LOCAL_INTERFACE</p>
<p>FWPM_CONDITION_IP_PROTOCOL</p>
<p>FWPM_CONDITION_IP_LOCAL_PORT</p>
<p>FWPM_CONDITION_IP_REMOTE_PORT</p>
<p>FWPM_CONDITION_FLAGS</p>
<p>FWPM_CONDITION_DIRECTION</p>
<p>FWPM_CONDITION_ALE_APP_ID</p>
<p>FWPM_CONDITION_ALE_USER_ID</p>
<p>FWPM_CONDITION_ALE_REMOTE_USER_ID</p>
<p>FWPM_CONDITION_ALE_REMOTE_MACHINE_ID</p>
<p>FWPM_CONDITION_INTERFACE_TYPE</p>
<p>FWPM_CONDITION_TUNNEL_TYPE</p>
<p>FWPM_CONDITION_ALE_PACKAGE_ID
</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_NAME_RESOLUTION_CACHE_V4</p>
<p>FWPM_LAYER_NAME_RESOLUTION_CACHE_V6</p>
</td>
<td>
<p>FWPM_CONDITION_ALE_USER_ID</p>
<p>FWPM_CONDITION_ALE_APP_ID</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS</p>
<p>FWPM_CONDITION_PEER_NAME</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_ALE_RESOURCE_RELEASE_V4</p>
<p>FWPM_LAYER_ALE_RESOURCE_RELEASE_V6</p>
</td>
<td>
<p>FWPM_CONDITION_ALE_APP_ID</p>
<p>FWPM_CONDITION_ALE_USER_ID</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_IP_LOCAL_PORT</p>
<p>FWPM_CONDITION_IP_PROTOCOL</p>
<p>FWPM_CONDITION_IP_LOCAL_INTERFACE</p>
<p>FWPM_CONDITION_FLAGS</p>
<p>FWPM_CONDITION_ALE_PACKAGE_ID</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_ALE_ENDPOINT_CLOSURE_V4</p>
<p>FWPM_LAYER_ALE_ENDPOINT_CLOSURE_V6</p>
</td>
<td>
<p>FWPM_CONDITION_ALE_APP_ID</p>
<p>FWPM_CONDITION_ALE_USER_ID</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_IP_LOCAL_PORT</p>
<p>FWPM_CONDITION_IP_PROTOCOL</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS</p>
<p>FWPM_CONDITION_IP_REMOTE_PORT</p>
<p>FWPM_CONDITION_IP_LOCAL_INTERFACE</p>
<p>FWPM_CONDITION_FLAGS</p>
<p>FWPM_CONDITION_ALE_PACKAGE_ID</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_ALE_CONNECT_REDIRECT_V4</p>
<p>FWPM_LAYER_ALE_CONNECT_REDIRECT_V6</p>
</td>
<td>
<p>FWPM_CONDITION_ALE_APP_ID</p>
<p>FWPM_CONDITION_ALE_USER_ID</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_IP_LOCAL_PORT</p>
<p>FWPM_CONDITION_IP_PROTOCOL</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS</p>
<p>FWPM_CONDITION_IP_DESTINATION_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_IP_REMOTE_PORT</p>
<p>FWPM_CONDITION_FLAGS</p>
<p>FWPM_CONDITION_ALE_ORIGINAL_APP_ID</p>
<p>FWPM_CONDITION_ALE_PACKAGE_ID</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_ALE_BIND_REDIRECT_V4</p>
<p>FWPM_LAYER_ALE_BIND_REDIRECT_V6</p>
</td>
<td>
<p>FWPM_CONDITION_ALE_APP_ID</p>
<p>FWPM_CONDITION_ALE_USER_ID</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_TYPE</p>
<p>FWPM_CONDITION_IP_LOCAL_PORT</p>
<p>FWPM_CONDITION_IP_PROTOCOL</p>
<p>FWPM_CONDITION_FLAGS</p>
<p>FWPM_CONDITION_ALE_PACKAGE_ID</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_STREAM_PACKET_V4</p>
<p>FWPM_LAYER_STREAM_PACKET_V6</p>
</td>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS</p>
<p>FWPM_CONDITION_IP_LOCAL_PORT</p>
<p>FWPM_CONDITION_IP_REMOTE_PORT</p>
<p>FWPM_CONDITION_IP_LOCAL_INTERFACE</p>
<p>FWPM_CONDITION_INTERFACE_INDEX</p>
<p>FWPM_CONDITION_SUB_INTERFACE_INDEX</p>
<p>FWPM_CONDITION_DIRECTION</p>
<p>FWPM_CONDITION_FLAGS</p>
<p>FWPM_CONDITION_INTERFACE_TYPE</p>
<p>FWPM_CONDITION_TUNNEL_TYPE</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_INBOUND_MAC_FRAME_ETHERNET</p>
<p>FWPM_LAYER_OUTBOUND_MAC_FRAME_ETHERNET</p>
</td>
<td>
<p>
FWPM_CONDITION_INTERFACE_MAC_ADDRESS
</p>
<p>
FWPM_CONDITION_MAC_LOCAL_ADDRESS
</p>
<p>
FWPM_CONDITION_MAC_REMOTE_ADDRESS
</p>
<p>
FWPM_CONDITION_MAC_LOCAL_ADDRESS_TYPE
</p>
<p>
FWPM_CONDITION_MAC_REMOTE_ADDRESS_TYPE
</p>
<p>
FWPM_CONDITION_ETHER_TYPE
</p>
<p>
FWPM_CONDITION_VLAN_ID
</p>
<p>
FWPM_CONDITION_INTERFACE
</p>
<p>
FWPM_CONDITION_INTERFACE_INDEX
</p>
<p>
FWPM_CONDITION_NDIS_PORT
</p>
<p>
FWPM_CONDITION_L2_FLAGS
</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE</p>
<p>FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE </p>
</td>
<td>
<p>
FWPM_CONDITION_NDIS_MEDIA_TYPE
</p>
<p>
FWPM_CONDITION_NDIS_PHYSICAL_MEDIA_TYPE
</p>
<p>
FWPM_CONDITION_INTERFACE
</p>
<p>
FWPM_CONDITION_INTERFACE_TYPE
</p>
<p>
FWPM_CONDITION_INTERFACE_INDEX
</p>
<p>
FWPM_CONDITION_NDIS_PORT
</p>
<p>
FWPM_CONDITION_L2_FLAGS
</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_INGRESS_VSWITCH_ETHERNET</p>
</td>
<td>
<p>
FWPM_CONDITION_MAC_SOURCE_ADDRESS
</p>
<p>
FWPM_CONDITION_MAC_SOURCE_ADDRESS_TYPE
</p>
<p>
FWPM_CONDITION_MAC_DESTINATION_ADDRESS
</p>
<p>
FWPM_CONDITION_MAC_DESTINATION_ADDRESS_TYPE
</p>
<p>
FWPM_CONDITION_ETHER_TYPE
</p>
<p>
FWPM_CONDITION_VLAN_ID
</p>
<p>FWPM_CONDITION_VSWITCH_TENANT_NETWORK_ID</p>
<p>
FWPM_CONDITION_VSWITCH_ID
</p>
<p>
FWPM_CONDITION_VSWITCH_NETWORK_TYPE
</p>
<p>
FWPM_CONDITION_VSWITCH_SOURCE_INTERFACE_ID
</p>
<p>
FWPM_CONDITION_VSWITCH_SOURCE_INTERFACE_TYPE
</p>
<p>FWPM_CONDITION_VSWITCH_SOURCE_VM_ID</p>
<p>
FWPM_CONDITION_L2_FLAGS
</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_EGRESS_VSWITCH_ETHERNET</p>
</td>
<td>
<p>
FWPM_CONDITION_MAC_SOURCE_ADDRESS
</p>
<p>
FWPM_CONDITION_MAC_SOURCE_ADDRESS_TYPE
</p>
<p>
FWPM_CONDITION_MAC_DESTINATION_ADDRESS
</p>
<p>
FWPM_CONDITION_MAC_DESTINATION_ADDRESS_TYPE
</p>
<p>
FWPM_CONDITION_ETHER_TYPE
</p>
<p>
FWPM_CONDITION_VLAN_ID
</p>
<p>FWPM_CONDITION_VSWITCH_TENANT_NETWORK_ID</p>
<p>
FWPM_CONDITION_VSWITCH_ID
</p>
<p>
FWPM_CONDITION_VSWITCH_NETWORK_TYPE
</p>
<p>
FWPM_CONDITION_VSWITCH_SOURCE_INTERFACE_ID
</p>
<p>
FWPM_CONDITION_VSWITCH_SOURCE_INTERFACE_TYPE
</p>
<p>FWPM_CONDITION_VSWITCH_SOURCE_VM_ID</p>
<p>
FWPM_CONDITION_VSWITCH_DESTINATION_INTERFACE_ID
</p>
<p>
FWPM_CONDITION_VSWITCH_DESTINATION_INTERFACE_TYPE
</p>
<p>FWPM_CONDITION_VSWITCH_DESTINATION_VM_ID</p>
<p>
FWPM_CONDITION_L2_FLAGS
</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_INGRESS_VSWITCH_TRANSPORT_V4</p>
<p>FWPM_LAYER_INGRESS_VSWITCH_TRANSPORT_V6</p>
</td>
<td>
<p>
FWPM_CONDITION_IP_SOURCE_ADDRESS
</p>
<p>
FWPM_CONDITION_IP_DESTINATION_ADDRESS
</p>
<p>
FWPM_CONDITION_P_PROTOCOL
</p>
<p>
FWPM_CONDITION_IP_SOURCE_PORT
</p>
<p>
FWPM_CONDITION_IP_DESTINATION_PORT
</p>
<p>
FWPM_CONDITION_VLAN_ID
</p>
<p>FWPM_CONDITION_VSWITCH_TENANT_NETWORK_ID</p>
<p>
FWPM_CONDITION_VSWITCH_ID
</p>
<p>
FWPM_CONDITION_VSWITCH_NETWORK_TYPE
</p>
<p>
FWPM_CONDITION_VSWITCH_SOURCE_INTERFACE_ID
</p>
<p>
FWPM_CONDITION_VSWITCH_SOURCE_INTERFACE_TYPE
</p>
<p>FWPM_CONDITION_VSWITCH_SOURCE_VM_ID</p>
<p>
FWPM_CONDITION_L2_FLAGS
</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_EGRESS_VSWITCH_TRANSPORT_V4</p>
<p>FWPM_LAYER_EGRESS_VSWITCH_TRANSPORT_V6</p>
</td>
<td>
<p>
FWPM_CONDITION_IP_SOURCE_ADDRESS
</p>
<p>
FWPM_CONDITION_IP_DESTINATION_ADDRESS
</p>
<p>
FWPM_CONDITION_IP_PROTOCOL
</p>
<p>
FWPM_CONDITION_IP_SOURCE_PORT
</p>
<p>
FWPM_CONDITION_IP_DESTINATION_PORT
</p>
<p>
FWPM_CONDITION_VLAN_ID
</p>
<p>FWPM_CONDITION_VSWITCH_TENANT_NETWORK_ID</p>
<p>
FWPM_CONDITION_VSWITCH_ID
</p>
<p>
FWPM_CONDITION_VSWITCH_NETWORK_TYPE
</p>
<p>
FWPM_CONDITION_VSWITCH_SOURCE_INTERFACE_ID
</p>
<p>
FWPM_CONDITION_VSWITCH_SOURCE_INTERFACE_TYPE
</p>
<p>FWPM_CONDITION_VSWITCH_SOURCE_VM_ID</p>
<p>
FWPM_CONDITION_VSWITCH_DESTINATION_INTERFACE_ID
</p>
<p>
FWPM_CONDITION_VSWITCH_DESTINATION_INTERFACE_TYPE
</p>
<p>FWPM_CONDITION_VSWITCH_DESTINATION_VM_ID</p>
<p>
FWPM_CONDITION_L2_FLAGS
</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_IPSEC_KM_DEMUX_V4</p>
<p>FWPM_LAYER_IPSEC_KM_DEMUX_V6</p>
</td>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_IPSEC_V4</p>
<p>FWPM_LAYER_IPSEC_V6</p>
</td>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS</p>
<p>FWPM_CONDITION_IP_PROTOCOL</p>
<p>FWPM_CONDITION_IP_LOCAL_PORT</p>
<p>FWPM_CONDITION_IP_REMOTE_PORT</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_IKEEXT_V4</p>
<p>FWPM_LAYER_IKEEXT_V6</p>
</td>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_RPC_UM</p>
</td>
<td>
<p>FWPM_CONDITION_IP_LOCAL_PORT</p>
<p>FWPM_CONDITION_REMOTE_USER_TOKEN</p>
<p>FWPM_CONDITION_RPC_IF_UUID</p>
<p>FWPM_CONDITION_RPC_IF_VERSION</p>
<p>FWPM_CONDITION_RPC_PROTOCOL</p>
<p>FWPM_CONDITION_RPC_IF_FLAG</p>
<p>FWPM_CONDITION_DCOM_APP_ID</p>
<p>FWPM_CONDITION_IMAGE_NAME</p>
<p>FWPM_CONDITION_RPC_AUTH_TYPE</p>
<p>FWPM_CONDITION_RPC_AUTH_LEVEL</p>
<p>FWPM_CONDITION_SEC_ENCRYPT_ALGORITHM</p>
<p>FWPM_CONDITION_SEC_KEY_SIZE</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_V4</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_V6</p>
<p>FWPM_CONDITION_PIPE</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS_V4</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS_V6</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_RPC_EPMAP</p>
</td>
<td>
<p>FWPM_CONDITION_IP_LOCAL_PORT</p>
<p>FWPM_CONDITION_REMOTE_USER_TOKEN</p>
<p>FWPM_CONDITION_RPC_IF_UUID</p>
<p>FWPM_CONDITION_RPC_IF_VERSION</p>
<p>FWPM_CONDITION_RPC_PROTOCOL</p>
<p>FWPM_CONDITION_RPC_AUTH_TYPE</p>
<p>FWPM_CONDITION_RPC_AUTH_LEVEL</p>
<p>FWPM_CONDITION_SEC_ENCRYPT_ALGORITHM</p>
<p>FWPM_CONDITION_SEC_KEY_SIZE</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_V4</p>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_V6</p>
<p>FWPM_CONDITION_PIPE</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS_V4</p>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS_V6</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_RPC_EP_ADD</p>
</td>
<td>
<p>FWPM_CONDITION_RPC_PROTOCOL</p>
<p>FWPM_CONDITION_PROCESS_WITH_RPC_IF_UUID</p>
<p>FWPM_CONDITION_RPC_EP_VALUE</p>
<p>FWPM_CONDITION_RPC_EP_FLAGS</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_RPC_PROXY_CONN</p>
</td>
<td>
<p>FWPM_CONDITION_CLIENT_TOKEN</p>
<p>FWPM_CONDITION_RPC_SERVER_NAME</p>
<p>FWPM_CONDITION_RPC_SERVER_PORT</p>
<p>FWPM_CONDITION_RPC_PROXY_AUTH_TYPE</p>
<p>FWPM_CONDITION_CLIENT_CERT_KEY_LENGTH</p>
<p>FWPM_CONDITION_CLIENT_CERT_OID</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_RPC_PROXY_IF</p>
</td>
<td>
<p>FWPM_CONDITION_RPC_IF_UUID</p>
<p>FWPM_CONDITION_RPC_IF_VERSION</p>
<p>FWPM_CONDITION_CLIENT_TOKEN</p>
<p>FWPM_CONDITION_RPC_SERVER_NAME</p>
<p>FWPM_CONDITION_RPC_SERVER_PORT</p>
<p>FWPM_CONDITION_RPC_PROXY_AUTH_TYPE</p>
<p>FWPM_CONDITION_CLIENT_CERT_KEY_LENGTH</p>
<p>FWPM_CONDITION_CLIENT_CERT_OID</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_LAYER_KM_AUTHORIZATION</p>
</td>
<td>
<p>FWPM_CONDITION_REMOTE_ID</p>
<p>FWPM_CONDITION_AUTHENTICATION_TYPE</p>
<p>FWPM_CONDITION_KM_TYPE</p>
<p>FWPM_CONDITION_DIRECTION</p>
<p>FWPM_CONDITION_KM_MODE</p>
<p>FWPM_CONDITION_IPSEC_POLICY_KEY</p>
<p>FWPM_CONDITION_KM_AUTH_NAP_CONTEXT</p>
</td>
</tr>
</table>

