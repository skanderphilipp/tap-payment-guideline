To streamline the creation of payment agreements, Tap Payments offers two methods:

**Charge API:** This method integrates the creation of a payment agreement directly into the charging process. When initiating an order or subscription, specifying the agreement type will prompt Tap Payments to automatically generate the agreement, providing an agreement ID (payment\_agreement.id) for the customer's card.

**Payment Agreement API:** Alternatively, merchants can employ a dedicated API for more granular control, allowing them to create a payment agreement and associate it with the customer's card independently. (This API is currently in beta, with a full launch anticipated shortly.)

## Payment Agreement Object   [Skip link to Payment Agreement Object](https://developers.tap.company/docs/creating-payment-agreement\#payment-agreement-object)

The payment agreement object details the terms of the agreement between the merchant and the customer regarding the use of a saved card.

json

```rdmd-code lang-json theme-light
"payment_agreement": {
		"id": "payment_agreement_TS05A0920230152Hj2e2105495",
		"total_payments_count": 2,
		"contract": {
			"id": "card_3NgY56232243uLD920sA4n697",
			"type": "UNSCHEDULED"
		},
		"variable_amount": {
			"id": "variable_amount_TS05A0920230152a0F22105495"
		}
	}

```

Here is an explanation of each attribute within the payment agreement object:

| Parameter | Description | Example |
| --- | --- | --- |
| id | Serves as a unique identifier for referencing and managing the payment agreement. | payment\_agreement\_TS05A0920230152Hj2e2105495 |
| total\_payments\_count | Tracks the total number of payments made under this agreement. | 2 |
| contract | Represents the unique identifier for the associated contract, helping in identification and referencing. |  |
| contract.id | Uniquely identifies the agreement between the merchant and the customer, using an invoice ID, subscription ID, card ID, or order ID. | card\_3NgY56232243uLD920sA4n697 |
| contract.type | Specifies the type of contract, such as "UNSCHEDULED" in this instance, indicating non-recurring payments. | UNSCHEDULED |
| variable\_amount | Provides information about the associated variable amount within the contract. |  |
| variable\_amount.id | Acts as a unique identifier for the specific variable amount. | variable\_amount\_TS05A0920230152a0F22105495 |
| maximum\_amount: | Indicates the maximum chargeable amount for this contract, with the example showcasing a maximum of 1.00 in the specified currency. |  |

This information helps merchants and payment gateway track the payment agreements and associated contracts with customers.

# Customer Initiated Transactions   [Skip link to Customer Initiated Transactions](https://developers.tap.company/docs/creating-payment-agreement\#customer-initiated-transactions)

The "customer\_initiated" boolean parameter distinguishes between customer-initiated and merchant-initiated transactions.

JSON

```rdmd-code lang-json theme-light
"customer_initiated":"false",

```

Here's how it works:

1. Transactions are considered customer-initiated by default, with the "customer\_initiated" parameter set to true, involving the customer's active participation and 3D Secure (3DS) authentication for enhanced security.
2. If a transaction is merchant-initiated, "customer\_initiated" is set to false, typically bypassing 3DS authentication. However, if a payment agreement is in place, the initial 3DS authorization serves as a reference for all subsequent transactions initiated by the merchant.
3. Depending on the "customer\_initiated" status, certain rules apply. For instance, mada transactions in Saudi Arabia mandate a payment agreement ID (PA\_ID) for all merchant-initiated transactions, reinforcing security protocols.
4. Tap Payments is progressively implementing clear distinctions between customer and merchant-initiated transactions across various card schemes, including VISA, MasterCard, and AMEX. From 2023 onwards, all new integrations are required to comply with this standard, while existing ones have until the end of 2023 to update their systems to continue using saved card features.

> ## 🚧  This phased approach mandates all merchants, both new and existing, to adapt to the "customer\_initiated" parameter by the end of 2023 to ensure compliance and the ongoing ability to process saved card transactions.

> ## 📘  Post-migration, transactions processed without a payment agreement will be unsupported. The "customer\_initiated" parameter will thus be instrumental in defining the transaction flow.

In essence, a false "customer\_initiated" value signals a transaction initiated by the merchant without 3DS, and a true value indicates a transaction initiated by the customer with 3DS authentication.

Updatedover 1 year ago

* * *