---
title: Manage Code Signing Certificates
description: This article describes how to get, add, and update code signing certificates to the hardware dashboard.
ms.date: 03/31/2025
ms.topic: how-to
---

# Manage code signing certificates

As a Partner Center administrator, you're responsible for adding, updating, and retiring driver certificates when they expire. This article describes how to get, add, and update code signing certificates to the hardware dashboard.

For more information on rules for driver signing, see [Driver Signing changes in Windows 10, version 1607](https://techcommunity.microsoft.com/t5/windows-hardware-certification/driver-signing-changes-in-windows-10-version-1607/ba-p/364894) in the [Windows Hardware Certification blog](https://techcommunity.microsoft.com/t5/windows-hardware-certification/bg-p/WindowsHardwareCertification).

## Prerequisites

Register for the Hardware Developer program. If you're not registered, follow the steps in [How to register for the Microsoft Windows Hardware Developer Program](hardware-program-register.md).

## Get or renew a code signing certificate

To get a new code signing certificate:

1. Determine which certificate you need. To help you choose a certificate, see [Driver signing requirements](code-signing-reqs.md).
1. If you're reusing a certificate, move on to step 5.
1. If your organization doesn't have a certificate, you need to [purchase an EV certificate from a trusted vendor](code-signing-reqs.md#where-to-get-ev-code-signing-certificates).
1. Once the certificate authority verifies your contact information and your certificate purchase is approved, follow their directions to retrieve the certificate.
1. Go to [Partner Center](https://partner.microsoft.com/dashboard) and sign in using administrator credentials.
1. Select the gear icon in the upper right, then select **Account Settings**, then **Manage Certificates** on the left side of the screen.
1. Select **Add a new certificate**, then select **Next**.
1. Download *Signablefile.bin* and sign it with the new digital certificate for your company using [SignTool](/windows/win32/seccrypto/signtool) with the `/fd sha256` switch and appropriate SHA-2 timestamp.
1. Upload the signed file to Partner Center.

## Retire a code signing certificate

1. Go to [Partner Center](https://partner.microsoft.com/dashboard) and sign in using administrator credentials.
1. Select the gear icon in the upper right, then select **Developer settings**, then **Manage Certificates** on the left pane.
1. Move through the page to find the certificate you wish to remove.
1. Under the **Action** column of the certificate, select **Remove**.
