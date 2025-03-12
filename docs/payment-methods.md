Learn more about the different payment methods and mechanisms available through the Charges and Authorize API.

There is a production and sandbox mode for all Tap operations whether the JS library, Mobile SDKs or direct API transactions, the mode of payment is determined by the API key used. Tap provides two sets of keys for respective payment modes. The sandbox key is for staging and testing purposes, while production keys is to be used for LIVE operations.

## Redirect Payment Flow   [Skip link to Redirect Payment Flow](https://developers.tap.company/docs/payment-methods\#redirect-payment-flow)

Certain payment methods require your customer to complete a particular action (flow) before the source is made chargeable.

Your customer must be redirected to the Tap payment page to process the payment. Tap Payment url will be provided in the API Response (transaction.url). KNET, MADA, BENEFIT and 3D secure transactions work with the Redirect payment method.

Redirect payment flow requires merchant url (redirect.url) in the API request. After payment is completed, the customer will be redirected to this url (merchant url)

## Direct Payment Flow   [Skip link to Direct Payment Flow](https://developers.tap.company/docs/payment-methods\#direct-payment-flow)

Some payment methods are not required any additional authentication from your customer.

If the credit card is not enrolled for 3D secure, then Tap process the payment and will return the payment status in the API response. Payment url will not be provided in the API response.

Synchronous or asynchronous

Once you use a payment method to create a Charge object, that charge status can be confirmed either immediately (synchronously), or after a certain amount of time (asynchronously).

- With a synchronous payment method, the charge or authorize status can be immediately confirmed as either success or failed.

- For asynchronous payment methods, it can take up to several days to confirm whether the payment has been successful. During this time, the payment cannot be guaranteed. The status of the payment’s Charge object is initially set to IN\_PROGRESS, until the payment has been confirmed as successful or failed.


You can use the source as "src\_all" in the charge request to display all payment methods on Tap Payment page.

Updatedover 1 year ago

* * *