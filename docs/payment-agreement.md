Tap Payments provides a streamlined process for transactions using saved cards, allowing merchants to store customer cards under specific payment agreements. These agreements permit the storage of cards with 3D Secure enabled and later, to charge the customer without requiring 3D Secure, adhering to the agreed-upon terms. This guide offers a comprehensive overview of this process, detailing the types of agreements available and the implementation plan for this feature.

# Payment Agreement   [Skip link to Payment Agreement](https://developers.tap.company/docs/payment-agreement\#payment-agreement)

A payment agreement is a mutual arrangement between the merchant and the customer that authorizes the merchant to carry out transactions on the customer's card. This arrangement facilitates more flexible transactions with saved cards while maintaining security measures that protect against unauthorized use. The use of a saved card necessitates clear consent from the customer, defined within the payment agreement terms, thus authorizing the merchant to make charges per the agreed terms using the saved card.

There are five contract types available for establishing customer payment agreements:

## Card Contract - Payment Agreement   [Skip link to Card Contract - Payment Agreement](https://developers.tap.company/docs/payment-agreement\#card-contract---payment-agreement)

This agreement allows for flexibility and openness, enabling merchants to utilize the saved card for any purpose as defined by the merchant.

**Example:** A customer agrees to save their card details with a merchant to facilitate future purchases without completing the entire payment process. As per their agreement, the merchant can charge the customer for various goods or services.

## Subscription Contract - Payment Agreement   [Skip link to Subscription Contract - Payment Agreement](https://developers.tap.company/docs/payment-agreement\#subscription-contract---payment-agreement)

This agreement enables the merchant to save the card exclusively for use within a specific subscription. The charged amount remains fixed and tied to the subscription.

**Example:** A customer subscribes to a monthly plan for a streaming service. Under a subscription contract, the merchant saves the customer's card details and automatically charges the fixed subscription fee to the customer's card each month.

## Installment Contract - Payment Agreement   [Skip link to Installment Contract - Payment Agreement](https://developers.tap.company/docs/payment-agreement\#installment-contract---payment-agreement)

This agreement applies when customers choose to make payments in installments. The charged amount remains fixed and corresponds to the installment plan.

**Example:** A customer purchases a high-value item and opts to pay in installments. The merchant saves the customer's card details under an installment contract and charges the agreed-upon installment amount at regular intervals until the full payment is completed.

## Milestone Contract - Payment Agreement   [Skip link to Milestone Contract - Payment Agreement](https://developers.tap.company/docs/payment-agreement\#milestone-contract---payment-agreement)

This agreement links payments to the completion of specific milestones or services. The charged amount varies and depends on the achieved milestones.

**Example:** A customer hires a contractor for a home renovation project. The merchant saves the customer's card details under a milestone contract and charges the customer after the completion of each defined milestone.

## Order Contract - Payment Agreement   [Skip link to Order Contract - Payment Agreement](https://developers.tap.company/docs/payment-agreement\#order-contract---payment-agreement)

The order contract represents a unique type of payment agreement, allowing the merchant to charge the customer after delivering goods or services. Instead of the usual authorize-capture process, this agreement enables the merchant to charge the customer at any time based on dispatched items. The charged amount varies and aligns with the dispatched items.

**Example:** A customer places an order for various items from an online store. The merchant saves the customer's card details under an order contract. As the merchant ships the items, they charge the customer's card for the corresponding amount of the dispatched items.

Updatedover 1 year ago

* * *