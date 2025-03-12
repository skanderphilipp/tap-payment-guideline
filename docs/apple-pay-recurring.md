# Apple Pay and tap Integration   [Skip link to Apple Pay and tap Integration](https://developers.tap.company/docs/apple-pay-recurring\#apple-pay-and-tap-integration)

Ensure that you have integrated Apple Pay into your application or website. Follow Apple's documentation and [tap](https://developers.tap.company/docs/apple-pay-token) guidelines to set up Apple Pay on your platform.

Integrate Tap Payments into your application or website to enable payment processing. Refer to Tap Payments documentation for the necessary integration steps.

# Apple Pay Payload Availability   [Skip link to Apple Pay Payload Availability](https://developers.tap.company/docs/apple-pay-recurring\#apple-pay-payload-availability)

Confirm that Apple Pay payload is available and supported by Tap Payments. Check Tap Payments documentation or contact their support team for details on Apple Pay integration and recurring payment capabilities.

# Create a Charge Request with tap token   [Skip link to Create a Charge Request with tap token](https://developers.tap.company/docs/apple-pay-recurring\#create-a-charge-request-with-tap-token)

Once Apple Pay payload is available, follow these steps to create a Tap token:

Use the Tap Payments API to initiate a [charge](https://developers.tap.company/docs/create-a-charge) request, specifying the necessary parameters including the "save\_card" flag set to "true". This allows the card details to be securely stored for recurring payments.

Upon successful charge creation, you will receive a response containing the payment agreement ID, card ID, and customer ID. These details will be required for creating the recurring payment token.

Refer [saved card flow](https://developers.tap.company/docs/saved-cards) for payment agreement ID and related details

# Create a New Token   [Skip link to Create a New Token](https://developers.tap.company/docs/apple-pay-recurring\#create-a-new-token)

To create a new token for recurring payments, utilize the [token endpoint](https://developers.tap.company/docs/create-a-token-from-saved-card) provided by Tap Payments.

# Create a recurring charge for Apple Pay   [Skip link to Create a recurring charge for Apple Pay](https://developers.tap.company/docs/apple-pay-recurring\#create-a-recurring-charge-for-apple-pay)

Make sure to include the following parameters while creating a recurring apple pay charge

Set "customer\_initiated" to "false" to indicate that the payment is not initiated by the customer but rather by the merchant.

Provide the payment agreement ID received while saving the card via charges API

# Process the Transaction   [Skip link to Process the Transaction](https://developers.tap.company/docs/apple-pay-recurring\#process-the-transaction)

Once the recurring payment token is created, you can use it to process transactions on a recurring basis. Use the Tap Payments API to initiate the transaction, ensuring you include the necessary parameters such as the recurring payment token generated in the previous step.

Tap Payments will handle the payment processing based on the agreed-upon schedule, charging the customer automatically for the recurring service or subscription.

Updatedover 1 year ago

* * *