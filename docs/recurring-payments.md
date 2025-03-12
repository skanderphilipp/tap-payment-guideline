Recurring payments allow merchants to charge customers on a regular basis, such as for subscriptions or installment plans. This guide provides a detailed guide on setting up and processing recurring payments using Tap APIs. Please note that this guide assumes you have already familiarized yourself with the API reference documentation for Tap Payments, specifically the [Charges](https://developers.tap.company/docs/charges) API and [Authorize](https://developers.tap.company/docs/authorize) API.

# Step 1: Enable the Save Card Feature   [Skip link to Step 1: Enable the Save Card Feature](https://developers.tap.company/docs/recurring-payments\#step-1-enable-the-save-card-feature)

First, ensure the Save Card feature is active on your account by contacting your Tap account manager. Activation allows you to store customer card details securely on Tap's system, providing you with Card ID, Customer ID, and Payment Agreement ID. Note: Full card details are not disclosed for security reasons.

To begin accepting recurring payments, the Save Card feature must be enabled on your merchant account. Contact your Tap account manager to request the activation of this feature. Once enabled, you will gain the ability to save customer card details on the Tap Payments platform. You will receive three important parameters: `Card ID,` `Customer ID`, and `Payment Agreement ID`. It's worth noting that the full raw card details will not be provided, as Tap ensures secure storage of card information.

# Step 2: Saving Cards   [Skip link to Step 2: Saving Cards](https://developers.tap.company/docs/recurring-payments\#step-2-saving-cards)

There are two methods to save cards: during the first transaction or during the authorization process. Follow the instructions below:

## a) Saving Cards During First Transaction:   [Skip link to a) Saving Cards During First Transaction:](https://developers.tap.company/docs/recurring-payments\#a-saving-cards-during-first-transaction)

When a customer makes their first transaction, you can save their card details by passing the `save_card ` parameter as `true` in the [Charges](https://developers.tap.company/docs/charges) API. Refer to the Charges API documentation for further details on implementing this.

## b) Saving Cards During Authorization:   [Skip link to b) Saving Cards During Authorization:](https://developers.tap.company/docs/recurring-payments\#b-saving-cards-during-authorization)

Alternatively, you can authorize the card for a small amount and save the card during the authorization process. To achieve this, include the `save_card=true` parameter in the authorization request. Subsequently, you can release the authorized amount using the [void authorize](https://developers.tap.company/docs/void-an-authorize) endpoint or set auto-void/auto-capture for a maximum period of `168` hours. For comprehensive instructions, consult the [Authorize API](https://developers.tap.company/docs/create-an-authorize) reference documentation.

# Step 3: Retrieving Card Details   [Skip link to Step 3: Retrieving Card Details](https://developers.tap.company/docs/recurring-payments\#step-3-retrieving-card-details)

Once a card is saved successfully, you can retrieve important card details for future reference. The card details retrieved will include:

Card ID

Creation timestamp

Live mode status

Customer ID

Funding type (e.g., CREDIT)

Card fingerprint

Card brand (e.g., VISA)

Card scheme (e.g., VISA)

Cardholder name

Expiration month

Expiration year

Last four digits of the card number

First six digits of the card number

**Example Response**

JSON

```rdmd-code lang-json theme-light

{
	"id": "card_CBLn1723121vxiX249U4R752",
	"created": 1684918877751,
	"object": "card",
	"live_mode": true,
	"address": {},
	"customer": "cus_LV02H3420231157Rw4e2405654",
	"funding": "CREDIT",
	"fingerprint": "H%2BB%2BTuqbTaggPAbfml9CDDJzLQUzActOhf1BnVF22TI%3D",
	"brand": "VISA",
	"scheme": "VISA",
	"name": "MIKITA",
	"exp_month": 1,
	"exp_year": 27,
	"last_four": "5925",
	"first_six": "418887"
}

```

> ## 📘  Note: It's essential to highlight that saving cards does not require PCI compliance on your end. All card details are securely stored in Tap Payments' PCI environment. Tap provides card SDKs for both web and mobile platforms, ensuring the secure collection of cardholder data during integration. The card data is encrypted, and a secure token is generated for authorization.

# Step 4: First Transaction and 3D Secure Process   [Skip link to Step 4: First Transaction and 3D Secure Process](https://developers.tap.company/docs/recurring-payments\#step-4-first-transaction-and-3d-secure-process)

When cards are saved, the first transaction performed using the saved card will undergo a 3D Secure process. This process enhances the security of the transaction and protects against fraudulent activity.

# Step 5: Starting Recurring Payments   [Skip link to Step 5: Starting Recurring Payments](https://developers.tap.company/docs/recurring-payments\#step-5-starting-recurring-payments)

To initiate recurring payments, you need to store three essential parameters in your database: Customer ID, Card ID, and Payment Agreement ID. These parameters will be used in subsequent transactions for recurring charges. Here's how to generate a fresh token for recurring payments:

Utilize the Token API to generate a token from the saved card. This token will serve as a reference for future charges.

> ## 🚧  Note: Tokens are one-time use and expire after 5 minutes. It's crucial to generate a new token for each recurring payment.

## Step 6: Initiating Recurring Payments - Non-3DS Transaction   [Skip link to Step 6: Initiating Recurring Payments - Non-3DS Transaction](https://developers.tap.company/docs/recurring-payments\#step-6-initiating-recurring-payments---non-3ds-transaction)

Perform the following steps to initiate a recurring payment as a non-3DS transaction:

1. Use the generated token within the source.id field of the Charges API.
2. Set `customer_initiated` to `false` to indicate a merchant-initiated transaction.
3. Include the Payment Agreement ID generated during the card-saving process in the Charges/Authorize API.

> ## 🚧  Note: A non-3DS transaction cannot be initiated without a valid Payment Agreement ID.

## Step 7: Complete Charge Request Example   [Skip link to Step 7: Complete Charge Request Example](https://developers.tap.company/docs/recurring-payments\#step-7-complete-charge-request-example)

Below is an example of a complete Charge Request for a recurring payment, including all the necessary parameters:

cURL

```rdmd-code lang-curl theme-light

curl --request POST \
     --url https://api.tap.company/v2/charges \
     --header 'Authorization: Bearer sk_test_WTcOpytQHIS1kdhw24avuG3C' \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
  "amount": 1,
  "currency": "KWD",
  "customer_initiated": false,
  "save_card": false,
  "payment_agreement": {
    "id": "payment_agreement_TS07A4620230032t4K21406294"
  },
  "description": "Test Description",
  "metadata": {
    "udf1": "Metadata 1"
  },
  "reference": {
    "transaction": "txn_01",
    "order": "ord_01"
  },
  "receipt": {
    "email": true,
    "sms": true
  },
  "customer": {
    "first_name": "test",
    "middle_name": "test",
    "last_name": "test",
    "email": "test@test.com",
    "phone": {
      "country_code": 965,
      "number": 51234567
    },
    "id": "cus_TS01A4620230032p4KP1406279"
  },
  "source": {
    "id": "tok_2uKe58232153ZmxV138r5c637"
  },
  "post": {
    "url": "http://your_website.com/post_url"
  },
  "redirect": {
    "url": "http://your_website.com/redirect_url"
  }
}
'

```

> ## 🚧  Note: Remember that for merchant-initiated transactions, the liability lies with the merchant, while for customer-initiated transactions, the liability rests with the payer.

# Best Practices:   [Skip link to Best Practices:](https://developers.tap.company/docs/recurring-payments\#best-practices)

To ensure a seamless experience and accurate tracking of recurring payments, consider the following best practices:

> ## 👍  Use a consistent Customer ID for each customer.
>
> Tap generates a unique Customer ID when customer information is passed through the Charges/Authorize API. Save this ID for future use. If required, utilize the Tap Customer API to create a Customer ID proactively.

> ## 📘  Note: Recurring payments are not supported for certain local payment methods, such as KNET or benefit. Refer to the respective payment method documentation for further information.

This comprehensive guide has provided you with step-by-step instructions on setting up and processing recurring payments using Tap Payments. By following these guidelines, you can seamlessly integrate recurring payments into your business operations and enhance the customer experience. If you require further assistance or have specific inquiries, please consult the Tap Payments support team for personalized support.

Updated9 months ago

* * *

Did this page help you?

Yes

No