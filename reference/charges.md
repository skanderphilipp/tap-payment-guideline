## Overview   [Skip link to Overview](https://developers.tap.company/reference/charges\#overview)

To directly charge a credit or debit card, submit a request to create a charge using the [Create a Charge](https://developers.tap.company/reference/create-a-charge) endpoint. All charges are identified by unique charge\_ids. You can also retrieve a charge, refund a charge or retrieve a list of charges.

You can also use this charges endpoint to Capture an authorized transaction.

* * *

## The Payment Source Object   [Skip link to The Payment Source Object](https://developers.tap.company/reference/charges\#the-payment-source-object)

In the charge request, include `source.id` to indicate the payment source at the time of the transaction.

The possible values are below based on your choice.

| Source ID | Description |
| --- | --- |
| `src_sa.mada` | **mada** (local payment switch in **KSA**). For this payment method, a `transaction.url` is always returned. Hence the user has to be redirected to this page after the Charge is `INITIATED`. |
| `src_kw.knet` | **KNET** (local payment switch in **Kuwait**). For this payment method, a `transaction.url` is always returned. Hence the user has to be redirected to this page after the Charge is `INITIATED`. |
| `src_eg.fawry` | **FAWRY** (local payment switch in **Egypt**). For this payment method, a `transaction.url` is always returned with the Fawry order details. Hence the user has to be redirected to this page after the Charge is `IN PROGRESS` so that the user can complete the payment at the Fawry Store. |
| `src_bh.benefit` | **Benefit** (local payment switch in **Bahrain**). For this payment method, a `transaction.url` is always returned. Hence the user has to be redirected to this page after the Charge is `INITIATED`. |
| src\_benefitpay | **Benefit** (local payment switch in **Bahrain**). For this payment method, a `transaction.url` is always returned. Hence the user has to be redirected to this page after the Charge is `INITIATED` with two option to pay with QR code or pay by benefit pay app directly. |
| src\_qa.qpay | **NAPS/QPAY** (local payment switch in **Qatar**) . For this payment method, a `transaction.url` is always returned in the response, hence the user has to be redirected to this page after the Charge is `INITIATED`. |
| `src_tabby.installement` | With **Tabby**, you can split your purchases into 4 interest-free payments, online or in-store. Here is the integration [guide](https://developers.tap.company/reference/tabby). |
| src\_apple\_pay | With **Apple pay**, you can pay with your apple device and by using safari browser easily. |
| src\_google\_pay | With **Google pay**, allow you to pay with your google account wallet. |
| src\_sa.stcpay | **STC Pay** allows the customers in KSA to pay with their phone numbers registred in STC Pay |
| src\_omannet | **Omannet** (local payment switch in **Oman**) . For this payment method, a `transaction.url` is always returned in the response, hence the user has to be redirected to this page after the Charge is `INITIATED`. |
| `token_id` | To capture the amount using the `token.id` generated from [Create a Token](https://developers.tap.company/reference/create-a-token) or [Card SDK](https://developers.tap.company/docs/card-js-library) or [Checkout SDK](https://developers.tap.company/docs/checkout-js-library). |
| `authorize_id` | To capture the amount using the `authorize.id` generated from [Create an Authorize](https://developers.tap.company/reference/create-an-authorize). |
| `src_card` | To display ONLY the Card payment methods on a Tap hosted page. The [Create a Charge](https://developers.tap.company/reference/create-a-charge) will return the `transaction.url` for redirecting the user to the Tap hosted page. |
| `src_all` | To display all the payment methods enabled for the Merchant ID on a Tap hosted Page. The [Create a Charge](https://developers.tap.company/reference/create-a-charge) will return the `transaction.url` to redirect the user to the Tap hosted page. |

> ## 📘  Redirect Payment Flow
>
> For **KNET, mada, Benefit** and 3D Secure transactions, `redirect.url` should be passed in the Charges Request.

* * *

## Charge Payment Request   [Skip link to Charge Payment Request](https://developers.tap.company/reference/charges\#charge-payment-request)

Sample

JSON

```rdmd-code lang-json theme-light
{
  "amount": 10,
  "currency": "AED",
  "threeDSecure": true,
  "save_card": false/true,    //based on your choice
  "customer_initiated":true,
  "description": "Test Description",
  "statement_descriptor": "Sample",
  "metadata": {
    "udf1": "test 1",
    "udf2": "test 2"
  },
  "reference": {
    "transaction": "txn_0001",
    "order": "ord_0001"
  },
  "receipt": {
    "email": true,
    "sms": false
  },
"customer":{
      "first_name":"Waleed",
      "last_name":"Asghar",
      "email":"w.asghar@tap.company",
      "phone":{
         "country_code":"971",
         "number":"586275033"
      }
   },
   "merchant":{
       "id": ""
   },
   "source": {
    "id": "src_all"
  },
  "post": {
    "url": "http://your_website.com/post_url"
  },
  "redirect": {
    "url": "http://your_website.com/redirect_url"
  }
}

```

## To Split The Payments (for Marketplace)   [Skip link to To Split The Payments (for Marketplace)](https://developers.tap.company/reference/charges\#to-split-the-payments-for-marketplace)

To split the amount, you can pass this optional Destinations Object in the charge request. And define the destination ID/s, desired amount, and currency. It will allow splitting the amount with sub-merchants(destinations), and the remaining amount will stay in the master account/wallet.

JSON

```rdmd-code lang-json theme-light
"destinations": {
    "destination": [\
      {\
        "id": "480593",\
        "amount": 2,\
        "currency": "AED"\
      },\
      {\
        "id": "486374",\
        "amount": 3,\
        "currency": "AED"\
      }\
    ]
  },

```

* * *

## To Set an Expiry period   [Skip link to To Set an Expiry period](https://developers.tap.company/reference/charges\#to-set-an-expiry-period)

The default transaction expiry period is 30 minutes, but it can be adjusted. You can set it to a minimum of 5 minutes and a maximum of 60 minutes by including the optional `transaction` object and specifying the desired period as shown below.

JSON

```rdmd-code lang-json theme-light
  "transaction": {
        "expiry": {
            "period": 60,
            "type": "MINUTE"
        }
    },

```

## Post Payment Response Details   [Skip link to Post Payment Response Details](https://developers.tap.company/reference/charges\#post-payment-response-details)

If the charge request is valid, then Tap will return the charge response which includes the "status" field defining the status of the charge. The possible values are below

`INITIATED, ABANDONED, CANCELLED, FAILED, DECLINED, RESTRICTED, CAPTURED, VOID, TIMEDOUT, UNKNOWN`

`INITIATED` \- Tap will provide the payment URL ( `transaction.url`) to process the payment.

The customer should be redirected to this URL in order to complete the payment.

`CAPTURED` \- Amount was successfully charged.

`ABANDONED, CANCELLED, FAILED, DECLINED, RESTRICTED, VOID, TIMEDOUT, UNKNOWN` \- Payment failed. Use the charge response code and message to identify the reason for failure.

`customer.id`

If you did not provide a customer ID in the charge request, Tap will create a customer ID for each successful transaction and share it within the charge response. You can store this customer ID for future charges, and authorizations, or for getting the list of charges or authorized transactions. You can also create a customer using [Create a Customer](https://developers.tap.company/reference/create-a-customer)

`card.id`

If you requested to save the card in the charge request, Tap will save the card and provide a card ID in the charge response if the transaction is successful. You can save this card ID and use it for future charges or authorizations. However, the card ID cannot be used directly in the charge or authorization request. You must first create a token ID using the saved card's ID and then pass the token ID along with the customer ID in the charge or authorization request.

### Expected Response   [Skip link to Expected Response](https://developers.tap.company/reference/charges\#expected-response)

Sample

JSON

```rdmd-code lang-json theme-light
{
    "id": "chg_TS03A2220231551Ha3j1408926",
    "object": "charge",
    "live_mode": false,
    "customer_initiated": true,
    "api_version": "V2",
    "method": "GET",
    "status": "CAPTURED",
    "amount": 10.00,
    "currency": "AED",
    "threeDSecure": true,
    "card_threeDSecure": false,
    "save_card": true,
    "merchant_id": "",
    "product": "GOSELL",
    "statement_descriptor": "Sample",
    "description": "Test Description",
    "metadata": {
        "udf1": "test 1",
        "udf2": "test 2"
    },
    "order": {
        "id": "ord_lWdQ29231251p2pQ14NO7c311"
    },
    "transaction": {
        "authorization_id": "030982",
        "timezone": "UTC+03:00",
        "created": "1692028310505",
        "expiry": {
            "period": 30,
            "type": "MINUTE"
        },
        "asynchronous": false,
        "amount": 10.00,
        "currency": "AED"
    },
    "reference": {
        "track": "tck_TS01A2220231551t1K31408958",
        "payment": "2214231551089588145",
        "gateway": "123456789012345",
        "acquirer": "322612030982",
        "transaction": "txn_0001",
        "order": "ord_0001"
    },
    "response": {
        "code": "000",
        "message": "Captured"
    },
    "security": {
        "threeDSecure": {
            "id": "3ds_TS06A5020231551j5JH1408505",
            "status": "Y"
        }
    },
    "acquirer": {
        "response": {
            "code": "00",
            "message": "Approved"
        }
    },
    "gateway": {
        "response": {
            "code": "0",
            "message": "Transaction Approved"
        }
    },
    "card": {
        "id": "card_NOSc48231251fiLc14rl7u285",
        "object": "card",
        "first_six": "411111",
        "scheme": "VISA",
        "brand": "VISA",
        "last_four": "1111"
    },
    "receipt": {
        "id": "202314231551081692",
        "email": true,
        "sms": false
    },
    "customer": {
        "id": "cus_TS06A5220231551Rl7y1408020",
        "first_name": "Waleed",
        "last_name": "Asghar",
        "email": "w.asghar@tap.company",
        "phone": {
            "country_code": "971",
            "number": "586275033"
        }
    },
    "merchant": {
        "country": "AE",
        "currency": "AED",
        "id": "14583257"
    },
    "source": {
        "object": "token",
        "type": "CARD_NOT_PRESENT",
        "payment_type": "CREDIT",
        "payment_method": "VISA",
        "channel": "INTERNET",
        "id": "tok_mgtn48231251SX3414YZ7l282"
    },
    "redirect": {
        "status": "SUCCESS",
        "url": "http://your_website.com/redirect_url"
    },
    "post": {
        "status": "ERROR",
        "url": "http://your_website.com/post_url"
    },
    "activities": [\
        {\
            "id": "activity_TS07A5220231551Mj841408864",\
            "object": "activity",\
            "created": 1692028310505,\
            "status": "INITIATED",\
            "currency": "AED",\
            "amount": 10.00,\
            "remarks": "charge - created"\
        },\
        {\
            "id": "activity_TS05A1020231552Oe1m1408270",\
            "object": "activity",\
            "created": 1692028330270,\
            "status": "CAPTURED",\
            "currency": "AED",\
            "amount": 10.00,\
            "remarks": "charge - captured"\
        }\
    ],
    "auto_reversed": false,
    "payment_agreement": {
        "id": "payment_agreement_h5Rp522312517fHg14Vg7a661",
        "type": "UNSCHEDULED",
        "total_payments_count": 1,
        "contract": {
            "id": "card_NOSc48231251fiLc14rl7u285",
            "customer_id": "cus_TS06A5220231551Rl7y1408020",
            "type": "SAVED_CARD"
        },
        "metadata": {
            "txn_type": "CHARGE",
            "txn_id": "chg_TS03A2220231551Ha3j1408926",
            "terminal_id": "ter_p3F64020211320j6XQ1002702"
        }
    }
}

```