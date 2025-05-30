---
title: Create a new hardware submission
description: Create a new hardware submission
ms.date: 08/16/2024
ms.topic: how-to
---

# Create a new hardware submission

With the Partner Center hardware dashboard, you can submit your Windows tested drivers for certification. This article describes how to create a new hardware submission in the Partner Center hardware dashboard.

All hardware submissions to the dashboard are processed within five business days, depending on whether the submission requires manual review. Manual review might be required if your submission's tests fail, if it doesn't have a valid filter applied, or due to an internal business policy.

> [!NOTE]
> In order to make Windows 10 more secure without affecting performance, all binaries are now receiving embedded signatures. This applies to all submissions for certification, not only Windows 10 submissions.

## Prerequisites

1. Make sure your [dashboard account](https://partner.microsoft.com/dashboard) is registered for the Windows Hardware Developer Program. For information on how to register, see [How to register for the Windows Hardware Developer Program](hardware-program-register.md).

1. Use the following table to determine which signed file you need to create for your submission.

    | Operating system | Required signed file type | Guidance|
    |------------------|---------------------------|---------|
    | Windows 11, Windows 10, and Windows Server versions beginning with Windows Server 2016 | A Windows Hardware Lab kit *.hlk* file | [Find and download the correct version of the HLK](/windows-hardware/test/hlk/) based on the compatible system. You can then [merge all HLK test results](/windows-hardware/test/hlk/user/merge-packages) into a single dashboard submission.</br></br>**Note:** The Windows 10 version 22H2 release follows the same guidelines as Windows 10, version 2004. For more information, see [WHCP guidance for Windows 10, version 22H2](https://techcommunity.microsoft.com/t5/windows-hardware-certification/whcp-guidance-for-windows-10-version-22h2/ba-p/3586362). |
    | Windows 8/8.1 and older | A Windows Hardware Certification Kit.hckx* file | To learn how to create and digitally sign an *.hckx* file, see the [Windows HCK Getting Started Guide](/previous-versions/windows/hardware/hck/jj123537(v=vs.85)) |
    | Windows Server 2008 and older  | A WLK hardware submission package *.cab* file | To learn how to create a WLK submission package, see [Create a new WLK hardware submission](hardware-submission-wlk.md). |

## Submit your new hardware

1. Go to [Partner Center hardware dashboard](https://partner.microsoft.com/dashboard/hardware/Search) and sign in using your credentials.

1. Select **Submit new hardware**.

    :::image type="content" source="./images/hardware-submission-create/hardware-list.png" alt-text="Screenshot of the list of submitted hardware list.":::

1. In the **Packages and signing properties** section, enter a product name for your driver submission. This name can be used to search for and organize your driver submissions.

    > [!NOTE]
    > If you share your driver with another company, they will see this name.

1. Either drag or browse to the **.hlkx/.hckx** file that you want to submit. If you're submitting WLK hardware, you must submit a *.cab* file. To learn how to create a WLK *.cab* file submission, see [Create a WLK hardware submission package](hardware-submission-wlk.md).

   :::image type="content" source="./images/hardware-submission-create/hardware-submit.png" alt-text="Screenshot that shows the new hardware submission form.":::

1. If you want to test a driver before release, select **Perform test-signing**. Test-signed drivers are similar to drivers signed for public release, but don't require HLK testing. They're also not distributed through Windows Update, but can be downloaded from the hardware submission site. They can be installed on test machines only. For more information about test-signing driver packages, see [WHQL Test Signature Program](../install/whql-test-signature-program.md) and [How to test-sign a driver package](../install/how-to-test-sign-a-driver-package.md).

1. Complete any other any questionnaires that are presented. The portal presents any questionnaire required for the product type being submitted for Windows Server certification.

1. Under **Request Signatures**, select which operating system signatures (including allowable downlevel operating systems) should be included with your driver. Available certifications vary depending on your driver submission package, so there might not be any certifications listed.

    > [!NOTE]
    > If you're signing a driver package for a single architecture, only include logs for the intended architecture. For example, to sign for x64 only, submit only the x64 logs.

    :::image type="content" source="./images/hardware-submission-create/hardware-signatures.png" alt-text="Screenshot that shows possible signatures for a driver submission, and the finalize button.":::

1. In the **Certification** section, complete the following information:

   | Field | Description |
   |--|--|
   | Device type | Indicate if your device is:</br></br>**An internal component**, if your device is part of a system and connects inside the PC.</br></br> **An external component**, if your device is an external device (peripheral) that connects to a PC.</br></br> **Both**, if your device can be connected internally (inside a PC) and externally (peripheral). |
   | Device metadata category | Select an icon for your device from a list of default icons based on your device category. This selection determines which icon appears in Devices and Printers. If you don't want your device to appear, select "Internal device".</br></br> For information about delivering a rich experience with Windows Device Stage, see [Create a Device Metadata Experience](create-a-device-metadata-experience.md). |
   | Device metadata model ID | These GUIDs are used to validate your Device Metadata submissions to the legacy Sysdev dashboard. If provided, they must match the model IDs in your device metadata package. |
   | Announcement date | Enter the date when you want your product included on the Windows Server Catalog, the Windows Certified Product List, and the Universal Driver List. |
   | Marketing names | Enter one or more marketing names for your submission. Marketing names allow you to provide aliases for your product. You can provide as many names as you want.|

   :::image type="content" source="images/hardware-submission-create/hardware-certification.png" alt-text="Screenshot that shows the certification section.":::

    > [!IMPORTANT]
    > Check the announcement date. Once the announcement date has passed, you won't be able to add a new name.

1. Select **Submit** at the bottom of the page.

1. The **Distribution** section is used to publish your driver to Windows Update. For information about how to use the **Distribution** section, see [Manage driver distribution with shipping labels](manage-driver-distribution-by-submission.md).

1. You can monitor the progress of your submission with the progress tracker at the top of the page. Once all steps show a green check, the submission is complete and your organization receives a notification in the dashboard header.

   :::image type="content" source="images/hardware-submission-create/hardware-progress-tracker.png" alt-text="Screenshot that shows the progress tracker.":::

1. Review the results. If your submission failed, make any necessary changes and resubmit.

## Troubleshoot submission errors

### Files missing errors

Your error message is one of these:

- **There are files at the root of the cabinet.**
- **No .inf files found in driver directory/directories: XYZ.**

The failure is caused by an incorrect .cab file structure. The .CAB structure was created with driver files in the root folder of the .CAB file instead of having them in a subfolder. For instructions on how to create a proper .CAB file for your driver signing submissions, see [Attestation sign Windows 10+ drivers](code-signing-attestation.md).

### Zip64 error

Your error message is:

**File is using Zip64(4gb+file Size)**

This error is caused when the uploaded archive's filetype is .zip64 instead of .zip. This error is caused by a large file size. To fix this error, repackage the submission using the below steps.

1. Rename the current .hckx/hlkx file to .zip.
1. Extract to a folder.
1. Open the folder.
1. Select all items, then select and hold (or right-click) and select **Send to Compressed zip folder**.
1. Rename the new .zip folder as .hckx/.hlkx.
1. Upload the new .hckx/.hlkx file.

### Failed to open DUA package

Your error message is:

**Failed to open package: Not compatible with a version (3.2.0.0) with this instance package manager**

Use [HLK studio](/windows-hardware/test/hlk/user/install-standalone-hlk-studio) to open the downloaded DUA shell package and to create DUA submission.

**Other issues**

If you don't see your issue addressed here, go to [Get support for Partner Center dashboard issues](technical-support.md).

## Next Steps

> [!div class="nextstepaction"]
> [View hardware submissions](hardware-submissions-view.md)

> [!div class="nextstepaction"]
> [Update a hardware submission](hardware-submission-update.md)

> [!div class="nextstepaction"]
> [Validate a hardware submission signature](code-signing-validate.md)

> [!div class="nextstepaction"]
> [Windows HLK Getting Started Guide](/windows-hardware/test/hlk/getstarted/windows-hlk-getting-started)

> [!div class="nextstepaction"]
> [Distribute your driver with Driver flighting](driver-flighting.md)
