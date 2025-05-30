---
title: Dashboard submission product and shipping label IDs
description: Dashboard submission product and shipping label IDs
ms.date: 09/19/2024
---

# Dashboard submission product and shipping label IDs

This article defines the identification numbers associated with Partner Center submissions.

Within the Windows Hardware Dev Center, each driver submission is associated with three IDs: A private, shared, and submission ID. The following screenshot shows the relationship between these three IDs:

:::image type="content" source="images/id_relationship.png" alt-text="Screenshot that shows the relationship of the private, shared, and submission ID types.":::

The Partner Center lists each of these IDs on the driver details page of your products:

:::image type="content" source="images/id_driver_details.png" alt-text="Screenshot that shows that the three ID types and values are listed in the Partner Center.":::

## ID definitions

| ID Name | Description |
|--|--|
| Shared product ID | This identifier is shared across all accounts who have access to a driver. The Shared product ID allows you to easily communicate about specific submissions and track submission updates across multiple organizations. Share and track this ID with others, in most cases. |
| Private Product ID | The private product ID is the top level identifier that is generated with each new product creation. This ID is most useful for personal reference of specific products, and predicting their URLs. |

> [!NOTE]
> When you share a driver with someone else, they will be assigned a new private product ID. If you want to communicate about a product, use the Shared Product ID.
|Submission ID|This identifier represents the individual packages you upload to a Product. The initial submission, and all submission updates each have a unique identifier. This ID is most useful for tracking updates using the Driver Update Acceptable (DUA) process within a product.

Shipping labels also contain two more IDs:

| ID Name | Description |
|--|--|
| Shipping Label ID | This identifier is used for internal tracking, and is assigned to any shipping labels that are assigned to a product. In most cases, you don't need to know the Shipping Label ID. |
| Promotion Request ID | If your shipping label requires a manual review, Microsoft gives it a Promotion Request ID. The Promotion Request ID represents your unique shipping label in the driver ship room. You should include this ID in any support inquiry. |

## Next Steps

> [!div class="nextstepaction"]
> [View hardware submissions](hardware-submissions-view.md)

> [!div class="nextstepaction"]
> [Update a hardware submission](hardware-submission-update.md)

> [!div class="nextstepaction"]
> [Manage driver distribution with shipping labels](./manage-driver-distribution-by-submission.md)
