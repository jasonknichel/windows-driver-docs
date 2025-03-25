---
title: AllowTethering
description: AllowTethering
ms.date: 10/10/2023
ms.topic: concept-article
---

# AllowTethering

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

The AllowTethering element specifies whether the user is always allowed, never allowed, or allowed after an entitlement check to use Internet sharing.

> [!NOTE]
> If this element is configured to allow after an entitlement check, you must specify a [DeviceNotificationHandler](devicenotificationhandler.md) in your app that will handle the entitlement check.

## Usage

``` syntax
<AllowTethering>
  text
</AllowTethering>
```

## Attributes

There are no attributes.

## Text value

A string indicating whether Internet sharing is always allowed, never allowed, or allowed after an entitlement check.

## Child elements

There are no child elements.

## Parent elements

| Element | Description |
|---|---|
| [NetworkConfiguration](networkconfiguration.md) | Specifies the purchase and Internet mobile broadband profiles to be used or whether standard user can perform PIN unlock operations. |

## XSD

``` syntax
<xs:element name="name="AllowTethering" type="tns:TetheringAllowedType" minOccurs="0" />

<xs:simpleType name="TetheringAllowedType">  
  <xs:restriction base="xs:string">
    <xs:enumeration value="Never"/>
    <xs:enumeration value="Always"/>
    <xs:enumeration value="EntitlementCheckRequired"/>
  </xs:restriction>
</xs:simpleType>
```

## Remarks

This element is only applicable to Windows 8.1 and Windows 10.

The AllowTethering element is optional.
