---
title: Design the Landing Page of a Mobile Broadband App
description: Design the landing page of a mobile broadband app
ms.date: 10/05/2023
ms.topic: concept-article
---

# Design the landing page of a mobile broadband app

The landing page is the first page that the user sees when they start the mobile broadband app, except for certain cases that are described in [Integrate a mobile broadband app with other Windows components](integrate-a-mobile-broadband-app-with-other-windows-components.md#launch-points).

:::image type="content" source="images/mb-fig1-landing-page-postpaid.png" alt-text="Screenshot of a postpaid mobile broadband app landing page.":::

The landing page should follow UWP app guidelines for app layout. To encourage simplicity and ease of navigation, we recommend that you fit all contents of the landing page into a single page. The landing page is the central hub of your app. Although it is not a primary navigation method or management page, it showcases your app and its major functionality.

The following sections describe some of the content that you can include in the landing page:

- [Usage – show an overview or link](#usage--show-an-overview-or-link)
- [Operator messages – show an overview or link](#operator-messages--show-an-overview-or-link)
- [Links to other key pages](#links-to-other-key-pages)
- [App navigation](#app-navigation)
- [Operator branding](#operator-branding)
- [Quick summary](#quick-summary)
- [Additional resources](#additional-resources)

## Usage – show an overview or link

### Postpaid plans

Because it is important user to be able to see information about their data usage, usage should be highlighted on the landing page if possible. Although an overview is encouraged, you can alternatively provide a link to a separate page in the app that contains more details. Some suggestions for additional details can be found in the data usage section. See [Design account balance and usage info in a mobile broadband app](design-account-balance-and-usage-info-in-a-mobile-broadband-app.md) for more info.

### Prepaid plans

Data usage display is simplified for prepaid plans. A user should also be offered an option to recharge or refill their plan. You can provide a link to a page that offers payment options. See [Design billing pages in a mobile broadband app](design-billing-pages-in-a-mobile-broadband-app.md) for more info. The following shows a typical overview page for a prepaid plan:

:::image type="content" source="images/mb-fig2-landing-page-prepaid.png" alt-text="Screenshot of a prepaid mobile broadband app landing page.":::

## Operator messages – show an overview or link

A list of operator text messages can be highlighted on the landing page. Because a number of operator messages are high priority, users prefer having easy access to these. For more information about functionality that should be included for text messages, see [Design messages in a mobile broadband app](design-messages-in-a-mobile-broadband-app.md).

## Links to other key pages

You can provide links to other key pages on the landing page. For example, you could include a tile for **Help and Support** and a tile for **Services**.

## App navigation

When describing the landing page, it is important to consider navigation within the app. Your app will have multiple pages that have various purposes. Windows 10 offers the following tools that can be used for navigation:

- **Back button** The Back button can be used to return to the previous page in the app. For more information about the Back button styling, see [Quickstart: styling controls](/previous-versions/windows/apps/hh465498(v=win.10)).

- **Drop-down affordance with header text** The header text can be used as a drop-down affordance for navigation between multiple pages in an app. In the previous figures, clicking **Account Overview** would result in a drop-down list of pages in the app that can be navigated to, as shown in the following figure:

    :::image type="content" source="images/mb-fig3-nav-between-apps.png" alt-text="Screenshot of a drop-down menu for navigating between app pages.":::

    For more information about designing app navigation, see [Quickstart: Using single-page navigation](/previous-versions/windows/apps/hh452768(v=win.10)) and [**select element | select object**](https://developer.mozilla.org/docs/Web/HTML/Element/select).

## Operator branding

You can customize your mobile broadband app to suit your individual branding style. By using numerous customizations, you can make your app unique and easily recognizable. For more info on how you can brand your app, see [Design branding in a mobile broadband app](design-branding-in-a-mobile-broadband-app.md).

## Quick summary

### Appropriate design for the landing page

- Show information at a glance that users will primarily look for in your app.

- Use a simple layout to improve readability.

- Follow UWP app guidelines.

- Disable the **Back** button if this is the first time that the user is visiting the app.

### Inappropriate design for the landing page

- Don’t have scrolling on the landing page. Try to restrict all content to a single page.

- Don’t have management functionality on the landing page.

## Additional resources

- [Index of UX guidelines for UWP apps](https://developer.microsoft.com/windows/apps/design)

- [Adding controls and content](/previous-versions/windows/apps/hh465393(v=win.10))

- [Make great UWP apps](/windows/uwp/get-started/create-uwp-apps)

- [Laying out your UI](/previous-versions/windows/apps/hh465304(v=win.10))

- [Integrate a mobile broadband app with other Windows components](integrate-a-mobile-broadband-app-with-other-windows-components.md#splash-screen)

- [Integrate a mobile broadband app with other Windows components](integrate-a-mobile-broadband-app-with-other-windows-components.md#tile-and-toast-notifications)

## Related topics

[Designing the user experience of a mobile broadband app](designing-the-user-experience-of-a-mobile-broadband-app.md)
