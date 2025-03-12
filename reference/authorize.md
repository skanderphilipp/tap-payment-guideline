## Overview   [Skip link to Overview](https://developers.tap.company/reference/authorize\#overview)

To Authorize a credit card, an authorization request has to be created using the "Create an Authorize" endpoint. You can retrieve information on individual authorizations or a list of all authorizations using the appropriate endpoints. An authorization is identified by a unique, randomly generated ID that starts with "auth\_".

> ## 📘
>
> Authorize works only with Credit Cards.

To authorize a credit card, you need to create an authorization request with a Source ID.

| Source ID | Description |
| --- | --- |
| `token_id` | To capture the amount using the `token.id` generated from [Create a Token](https://developers.tap.company/reference/create-a-token) or [Card SDK](https://developers.tap.company/docs/card-js-library) or [Checkout SDK](https://developers.tap.company/docs/checkout-js-library). |
| `authorize_id` | To capture the amount using the `authorize.id` generated from [Create an Authorize](https://developers.tap.company/reference/create-an-authorize). |
| `src_card` | To display ONLY the Card payment methods on a Tap hosted page. The [Create an Authorize](https://developers.tap.company/reference/create-an-authorize) will return the `transaction.url` for redirecting the user to the Tap hosted page. |
| `src_all` | To display all the payment methods enabled for the Merchant ID on a Tap hosted Page. The [Create an Authorize](https://developers.tap.company/reference/create-an-authorize) will return the `transaction.url` to redirect the user to the Tap hosted page. |

If the source is saved under a Card Token ID, you must provide the linked Customer ID in the authorization request, otherwise the API will return an error.

**Auto Capture or Void with Updated Authorization Periods**

You can use the auto-object in the authorization request to automatically capture or void authorized transactions after a specified time period. Time should be defined in hours, with a minimum of 1 hour and a maximum of 168 hours. For Visa/MasterCard (V/MC), the authorization period is up to 30 days, for MADA and AMEX it is 14 days, and for others (e.g., PayPal), it is 7 days. Ensure that source.id is always provided as a token, as this extension is not applicable for src\_all and src\_cards.

For 3D secure transactions, you must pass the redirect.URL in the authorization API request. After the payment is completed, we will redirect the user to this URL.

## Authorize Request Example   [Skip link to Authorize Request Example](https://developers.tap.company/reference/authorize\#authorize-request-example)

JSON

```rdmd-code lang-json theme-light
{
  "amount": 1,
  "currency": "KWD",
  "threeDSecure": true,
  "save_card": false,
  "description": "test description",
  "statement_descriptor": "sample",
  "metadata": {
    "udf1": "test"
  },
  "reference": {
    "transaction": "txn_0001",
    "order": "ord_0001"
  },
  "receipt": {
    "email": false,
    "sms": true
  },
  "customer": {
    "first_name": "test",
    "middle_name": "test",
    "last_name": "test",
    "email": "test@test.com",
    "phone": {
      "country_code": "965",
      "number": "50000000"
    }
  },
  "source": {
    "id": "tok_34nmhg7nbvh45d7g"
  },
  "auto": {
    "type": "VOID",
    "time": 100
  },
  "post": {
    "url": "http://your_website.com/posturl"
  },
  "redirect": {
    "url": "http://your_website.com/returnurl"
  }
}

```

## Authorize Response Example   [Skip link to Authorize Response Example](https://developers.tap.company/reference/authorize\#authorize-response-example)

If the authorization request is valid, Tap will return an authorization response containing a "status" field which defines the status of the authorization. The possible values for this field are:

**INITIATED, ABANDONED, CANCELLED, FAILED, DECLINED, RESTRICTED, AUTHORIZED, CAPTURED, VOID, TIMEDOUT, UNKNOWN**

**"INITIATED"** \- Tap will provide the payment URL(transaction.url) to process the payment. The customer should be redirected to this URL to complete the payment.

**"AUTHORIZED"** \- The amount is successfully authorized.

**"CAPTURED"** \- The authorized amount is successfully captured.

**"VOID"** \- The authorized amount is successfully voided.

**ABANDONED, CANCELLED, FAILED, DECLINED, RESTRICTED, TIMEDOUT, UNKNOWN** -If the payment fails, you can use the authorization response code and message to get more information about the reasons for the failure.

**Customer ID** If you did not pass the customer ID in the authorization request, Tap will create a customer ID for each successful transaction and share it in the authorization response. You can store the customer ID for this customer and use it in the future for charges or authorizations, or to get the list of charges or authorizations.

**Card ID** If you have requested to save the card in the authorization request, the card will be saved and the Card ID will be provided in the authorization response if the transaction is successful. You can save this Card ID and use it for future charges or authorizations. However, the Card ID cannot be directly used in the charge or authorization request. You must first create a Token ID using this saved Card ID and pass the Token ID along with the Customer ID in the charge or authorization request.

> ## 📘
>
> To capture authorized funds, use the Charges API and include Authorize ID in the source object and Customer ID in the customer object.

JSON

```rdmd-code lang-json theme-light
"id": "auth_TS015320221616g5FJ0906442",
  "object": "authorize",
  "live_mode": false,
  "api_version": "V2",
  "method": "CREATE",
  "status": "INITIATED",
  "amount": 1,
  "currency": "KWD",
  "threeDSecure": true,
  "save_card": false,
  "merchant_id": "",
  "product": "",
  "statement_descriptor": "sample",
  "transaction": {
    "timezone": "UTC+03:00",
    "created": "1654791413442",
    "url": "https://sandbox.payments.tap.company/test_gosell/v2/payment/response.aspx?tap_auth=qU%2fYHoOr4bnJIZ4JWH429ltx3zTaguu3niIplmXFZ2A%3d&sess=a692rUwq%2bPk%3d&token=qU%2fYHoOr4bnJIZ4JWH429ltx3zTaguu3v8z9CyXELe3K%2b85WW7N5BA%3d%3d",
    "expiry": {
      "period": 30,
      "type": "MINUTE"
    },
    "asynchronous": false,
    "amount": 1,
    "currency": "KWD"
  },
  "reference": {
    "transaction": "txn_0001",
    "order": "ord_0001"
  },
  "response": {
    "code": "100",
    "message": "Initiated"
  },
  "receipt": {
    "email": true,
    "sms": true
  },
  "customer": {
    "first_name": "Test",
    "last_name": "Test",
    "email": "test@test.com",
    "phone": {
      "country_code": "965",
      "number": "50000000"
    }
  },
  "source": {
    "object": "source",
    "id": "src_card"
  },
  "redirect": {
    "status": "PENDING",
    "url": "http://your_website.com/redirecturl"
  },
  "post": {
    "status": "PENDING",
    "url": "http://your_website.com/posturl"
  },
  "auto": {
    "status": "PENDING",
    "type": "VOID",
    "time": 100
  },

```