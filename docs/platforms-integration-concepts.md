Welcome to the Simplified Onboarding and Transaction Management Guide for Platforms. In this documentation, we'll make the technical aspects of merchant onboarding and transaction processing easy to grasp. Whether you're a platform or a developer, understanding Merchant IDs, Terminal IDs, and the steps involved in the onboarding process is crucial. We'll also explore how to initiate and process transactions accurately. Let's simplify the technical jargon and streamline your experience with Tap.

## Merchant ID and Terminal IDs:   [Skip link to Merchant ID and Terminal IDs:](https://developers.tap.company/docs/platforms-integration-concepts\#merchant-id-and-terminal-ids)

A single Merchant ID can be used across all four platform types. A unique Terminal ID is assigned per sales channel (per platform) to differentiate transactions. The combination of Merchant ID and Platform ID determines the appropriate terminal for processing a transaction.

Merchant ID starts with "merchant _\*\*\*\*" and Terminal ID starts with "terminal_\*\*\*"

> ## 📘  Terminal ID is for internal use only. The platform need not use Terminal ID while initiating a transaction.

In simple terms, think of the "Merchant ID" as a unique code representing a business, like KFC. Now, consider the "Terminal ID" as a specific code assigned to different ways KFC takes orders, such as in-person dining or online delivery. The "Platform ID" acts like a tag that tells us how KFC is receiving these orders. So, while KFC has one main ID for their business (Merchant ID), they have two Terminal IDs because they take orders in two different ways. When someone pays KFC, we use the combination of the Merchant ID and Platform ID to determine which Terminal ID to use. This ensures that the right pricing is applied for the type of order – whether it's for in-person dining or online delivery, keeping everything organized and accurate.

## Onboarding Flow:   [Skip link to Onboarding Flow:](https://developers.tap.company/docs/platforms-integration-concepts\#onboarding-flow)

A platform can onboard a merchant as both a retail and commerce platform. They can also onboard merchants as payment technology operators to gain additional benefits, such as setting fees per payment method.

### Lead Creation:   [Skip link to Lead Creation:](https://developers.tap.company/docs/platforms-integration-concepts\#lead-creation)

The first step to onboard a merchant is to create a lead. A lead is a business account with minimal info which can then be converted to an actual merchant account. Lead can be created using an API and lead ID starts with `led_***` When creating a lead for a merchant, include a `platforms` object specifying the platform IDs (e.g., commerce and retail) assigned to the merchant.

Retail Platform ID starts with `retail_platform_***` Commerce Platform ID starts with `commerce_platform_**** ` and so on.

Refer [lead API reference](https://developers.tap.company/reference/lead) for more information

### Account Creation:   [Skip link to Account Creation:](https://developers.tap.company/docs/platforms-integration-concepts\#account-creation)

After a lead is successfully created, the next step is to convert a lead to an actual merchant account. After converting a lead into an account, the response includes a single Merchant ID with Terminal IDs associated with it.

### Transaction Processing:   [Skip link to Transaction Processing:](https://developers.tap.company/docs/platforms-integration-concepts\#transaction-processing)

When platform initiates a transaction (e.g., creating a charge or authorize), the platform must specify the Merchant ID and Platform ID. The combination of these two IDs directs the transaction to the appropriate terminal for processing.

Refer [create a charge](https://developers.tap.company/reference/charges) for more information

Updatedover 1 year ago

* * *