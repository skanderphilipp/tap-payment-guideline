Visa, Mastercard, American Express and Mada cards will be covered under the card payment method.

You can pass the token id to charge the above cards or you can pass the source as "src\_card" to collect the cards and processed them by Tap.

| Card | VISA | MasterCard | AMEX | mada |
| --- | --- | --- | --- | --- |
| **Payment Type** | DEBIT, CREDIT | DEBIT, CREDIT | CREDIT | DEBIT |
| **Payment Acceptance** | Local, Regional, Global | Local, Regional, Global | Local, Regional, Global | Local |

## Redirect Payment Flow   [Skip link to Redirect Payment Flow](https://developers.tap.company/docs/card-payments\#redirect-payment-flow)

Your customer must redirected to the 3D Secure page provided by issuer to authenticate the payment.

3D secure transactions work with Redirect payment flow. Charge or Authroze API will return the payment url (transaction.url) in the response object. Customer should be redirected to this payment url, to complete the payment process.

Merchant url (redirect.url) is required in the Charge request.

Initial charge or authorize status will be "PENDING". After payment completed, charge status will be confirmed immediately. So you can use the retrieve charge or authorize API to get the status.

## Direct Payment Flow   [Skip link to Direct Payment Flow](https://developers.tap.company/docs/card-payments\#direct-payment-flow)

If the credit card is not enrolled for 3D secure, then Tap process the payment and will return the confirmed payment status in the charge response. The payment url will not be available in the API response.

Updatedover 1 year ago

* * *