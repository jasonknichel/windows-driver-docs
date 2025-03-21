---
title: Hardware dashboard API
description: The Microsoft hardware dashboard APIs programmatically query and create submissions for hardware products within your organization's Partner Center account.
ms.date: 01/28/2025
---

# Hardware dashboard API

Use the *Microsoft Hardware APIs* to programmatically query and create submissions for hardware products within your organization's Partner Center account. These APIs are useful if your account manages many products, and you want to automate and optimize the submission process for these assets. These APIs use Microsoft Entra ID (Microsoft Entra ID) to authenticate the calls from your app or service.

Only accounts that belong to the [Hardware Partner Center program](./get-started-dashboard-submissions.md) can use the hardware dashboard APIs. Here's the end-to-end process of using the Microsoft Hardware API:

1. Complete the prerequisites in the next section.

1. Obtain a Microsoft Entra ID access token before you call a method in the Microsoft Hardware API. After you have a token, you have 60 minutes to use it in calls to the Microsoft Store submission API before the token expires. After the token expires, you can generate a new one.

1. Call the Microsoft Hardware API.

## Complete the prerequisites for using the Microsoft Hardware API

Before you start writing code to call the Microsoft Hardware API, you must complete these required prerequisites:

- You (or your organization) must have a Microsoft Entra ID directory and you must have [Global administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles)  permission for the directory. If you already use Microsoft 365 or other business services from Microsoft, you already have Microsoft Entra ID directory. Otherwise, you can [create a new Microsoft Entra ID in Partner Center](/windows/uwp/publish/associate-azure-ad-with-partner-center#create-a-brand-new-azure-ad-to-associate-with-your-partner-center-account) for no extra charge.

- If a Microsoft Entra ID application doesn't already exist, [you must create one](/windows/uwp/publish/add-users-groups-and-azure-ad-applications#create-a-new-azure-ad-application-account-in-your-organizations-directory-and-add-it-to-your-partner-center-account).

- You must [associate a Microsoft Entra ID application with your Partner Center account](/windows/uwp/publish/associate-azure-ad-with-partner-center) and assign it the **Manager** role.

- Gather your [Microsoft Entra ID application tenant ID, client ID, and key](/windows/uwp/publish/add-users-groups-and-azure-ad-applications#manage-keys-for-an-azure-ad-application). **Be sure to print or copy this key info, as you won't be able to access it again after you leave the key creation page.**

## Assigning the appropriate Hardware roles to your Microsoft Entra ID application

After [completing the prerequisites](#complete-the-prerequisites-for-using-the-microsoft-hardware-api), assign the appropriate roles so that the Microsoft Entra ID application can create and manage submissions and shipping labels.

1. From Partner Center, select the gear icon (near the upper right corner of the dashboard) and then select **Developer settings**. In the **Settings** menu, select **Users**.

1. On the **Users** page, select **Microsoft Entra ID applications** and the Microsoft Entra ID application that represents the app or service you use to access submissions for your Partner Center account.

1. On this page, under **Roles**, select **Hardware**.

    :::image type="content" source="images/hardware-tab-in-roles-section.png" alt-text="A screenshot showing the Hardware tab in the Roles section.":::

    Select **Driver Submitter**, **Shipping Label owner**, and if available, **Shipping Label promoter**.  [Learn more about these roles](./hardware-dashboard-users-manage.md)

## Obtain a Microsoft Entra ID access token

Before you call any of the methods in the Microsoft Hardware API, you must first obtain a Microsoft Entra ID access token that you pass to the **Authorization** header of each method in the API. After you obtain an access token, you have 60 minutes to use it before it expires. After the token expires, you can refresh the token, so you can continue to use it in further calls to the API. To obtain the access token, follow the instructions in [Service to Service Calls Using Client Credentials](/azure/active-directory/azuread-dev/v1-oauth2-client-creds-grant-flow) to send an HTTP POST to the `https://login.microsoftonline.com/<tenant_id>/oauth2/token` endpoint. Here's a sample request.

```http
POST https://login.microsoftonline.com/<tenant_id>/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded; charset=utf-8

grant_type=client_credentials
&client_id=<your_client_id>
&client_secret=<your_client_secret>
&resource=https://manage.devcenter.microsoft.com
```

For the *tenant_id* value in the POST URI and the *client_id* and *client_secret* parameters, specify the tenant ID, client ID, and the key for your application that you retrieved from Partner Center in the previous section. For the *resource* parameter, you must specify `https://manage.devcenter.microsoft.com`.

After your access token expires, you can refresh it by following the instructions in [Refreshing the access tokens](/azure/active-directory/azuread-dev/v1-protocols-oauth-code#refreshing-the-access-tokens).

## Use the Microsoft Hardware API

After you have a Microsoft Entra ID access token, you can call methods in the Microsoft Hardware API. The API includes many methods that are grouped into scenarios. To create or update submissions, you typically call multiple methods in the Microsoft Hardware API in a specific order. For information about each scenario and the syntax of each method, see the articles in the following table.

| Scenario | Description |
|:--|:--|
| Drivers | Get, create, and update drivers registered to your Partner Center Account. For more information about these methods, see the following articles:<ul><li>[Get product data](get-product-data.md)</li><li>[Manage product submissions](manage-product-submissions.md)</li><li>[Get shipping label data](get-shipping-labels.md)</li><li>[Manage shipping labels](manage-shipping-labels.md)</li></ul>|

## Code sample

The following code sample provides a complete end-to-end prebuilt solution created by the Microsoft Surface and Devices team:

- [Surface Dev Center Manager tool (GitHub)](https://github.com/Microsoft/SDCM)

## More help

If you have questions about the Microsoft Store submission API or need assistance managing your submissions with this API, visit the [support page](https://partner.microsoft.com/dashboard/account/help?returnUri=https://developer.microsoft.com/dashboard/hardware) and request help.

## Related topics

- [What is Microsoft Entra ID?](/azure/active-directory/fundamentals/active-directory-whatis)
