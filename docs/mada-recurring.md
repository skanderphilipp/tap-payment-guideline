# Create a Charge Request with mada   [Skip link to Create a Charge Request with mada](https://developers.tap.company/docs/mada-recurring\#create-a-charge-request-with-mada)

Use the Tap Payments API to initiate a [charge](https://developers.tap.company/docs/create-a-charge) request, specifying the necessary parameters including the "save\_card" flag set to "true". This allows the card details to be securely stored for recurring payments.

Upon successful charge creation, you will receive a response containing the payment agreement ID, card ID, and customer ID. These details will be required for creating the recurring payment token.

Refer [saved card flow](https://developers.tap.company/docs/saved-cards) for payment agreement ID and related details

# Create a New Token   [Skip link to Create a New Token](https://developers.tap.company/docs/mada-recurring\#create-a-new-token)

To create a new token for recurring payments, utilize the [token endpoint](https://developers.tap.company/docs/create-a-token-from-saved-card) provided by Tap Payments.

# Create a recurring charge for mada   [Skip link to Create a recurring charge for mada](https://developers.tap.company/docs/mada-recurring\#create-a-recurring-charge-for-mada)

Make sure to include the following parameters while creating a recurring mada charge

Set "customer\_initiated" to "false" to indicate that the payment is not initiated by the customer but rather by the merchant.

Provide the payment agreement ID received while saving the card via charges API

# Process the Transaction   [Skip link to Process the Transaction](https://developers.tap.company/docs/mada-recurring\#process-the-transaction)

Once the recurring payment token is created, you can use it to process transactions on a recurring basis. Use the Tap Payments API to initiate the transaction, ensuring you include the necessary parameters such as the recurring payment token generated in the previous step.

Tap Payments will handle the payment processing based on the agreed-upon schedule, charging the customer automatically for the recurring service or subscription.

Updatedover 1 year ago

* * *