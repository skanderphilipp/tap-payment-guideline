# Overview   [Skip link to Overview](https://developers.tap.company/docs/qpay\#overview)

NAPS provides multiple payment options for processing transactions in Qatar. One of these options is QPay, which can be used for online payments. This payment method can be utilized through our Tap hosted payment page or via a full redirection to the QPay page to complete the payment.

**Note:** NAPS/QPay currently supports transactions in Qatari Riyal (QAR) only.

> ## 📘  In order to enable this payment method on your Tap account, please make sure to contact your account manager or contact us at [support@tap.company](mailto:support@tap.company)

# QPay Integration   [Skip link to QPay Integration](https://developers.tap.company/docs/qpay\#qpay-integration)

To integration QPay in your website or mobile app, you need to redirect the customers to the QPay page in order for them to enter their card details and process the payment.

Here we will guide you through the integration.

## Call the Create a Charge API   [Skip link to Call the Create a Charge API](https://developers.tap.company/docs/qpay\#call-the-create-a-charge-api)

First, you need to call the create a charge API and pass the currency as **QAR** and specify the `source.id` to be `src_qa.qpay`

cURL

```rdmd-code lang-curl theme-light
curl --request POST \
     --url https://api.tap.company/v2/charges/ \
     --header 'Authorization: Bearer sk_test_XKokBfNWv6FIYuTMg5sLPjhJ' \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
  "amount": 1,
  "currency": "QAR",
  "customer_initiated": true,
  "threeDSecure": true,
  "save_card": false,
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
    }
  },
  "source": {
    "id": "src_qa.qpay"
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

## Redirect Customers to QPay Page   [Skip link to Redirect Customers to QPay Page](https://developers.tap.company/docs/qpay\#redirect-customers-to-qpay-page)

In the charge API response, you will receive the status as **INITIATED** and you will see a `transaction.url` that you need to open in a browser for the customer to be redirected to the QPay page and add his card details.

### Charge Response   [Skip link to Charge Response](https://developers.tap.company/docs/qpay\#charge-response)

JSON

```rdmd-code lang-json theme-light
{
  "id": "chg_TS07A0320241133g5RO1906000",
  "object": "charge",
  "live_mode": false,
  "customer_initiated": true,
  "api_version": "V2",
  "method": "CREATE",
  "status": "INITIATED",
  "amount": 1,
  "currency": "QAR",
  "threeDSecure": true,
  "card_threeDSecure": false,
  "save_card": false,
  "merchant_id": "599424",
  "product": "GOSELL",
  "description": "Test Description",
  "metadata": {
    "udf1": "Metadata 1"
  },
  "transaction": {
    "timezone": "UTC+03:00",
    "created": "1718796783000",
    "url": "https://sandbox.payments.tap.company/test_gosell/v2/payment/tap_process.aspx?chg=8D9e9fdEo5N4mrraH0U7ZJbK9Bb0fB0OM2WX34QIF%2bg%3d",
    "expiry": {
      "period": 30,
      "type": "MINUTE"
    },
    "asynchronous": false,
    "amount": 1,
    "currency": "QAR"
  },
  "reference": {
    "transaction": "txn_01",
    "order": "ord_01"
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
    "first_name": "test",
    "last_name": "test",
    "email": "test@test.com",
    "phone": {
      "country_code": "965",
      "number": "51234567"
    }
  },
  "merchant": {
    "country": "KW",
    "currency": "KWD",
    "id": "599424"
  },
  "source": {
    "object": "source",
    "id": "src_qa.qpay",
    "on_file": false
  },
  "redirect": {
    "status": "PENDING",
    "url": "http://your_website.com/redirect_url"
  },
  "post": {
    "status": "PENDING",
    "url": "http://your_website.com/post_url"
  },
  "activities": [\
    {\
      "id": "activity_TS06A0620241133c4HR1906047",\
      "object": "activity",\
      "created": 1718796783000,\
      "status": "INITIATED",\
      "currency": "QAR",\
      "amount": 1,\
      "remarks": "charge - created",\
      "txn_id": "chg_TS07A0320241133g5RO1906000"\
    }\
  ],
  "auto_reversed": false
}

```

> ## 🚧  Make sure to open the transaction.url as a full redirection to the URL itself and do not add it in an iframe for the payment to work as expected!

### Complete a Payment with QPay   [Skip link to Complete a Payment with QPay](https://developers.tap.company/docs/qpay\#complete-a-payment-with-qpay)

After opening the transaction.url in a browser, the customer will add his card details and then submit it. You can either use the [test card](https://developers.tap.company/reference/testing-cards) added in our documentation if the payment is in sandbox mode, or use a real QPay card to complete the payment.

The user will also be prompted to add an OTP to verify that he is the cardholder. In test mode the OTP can be anything, for example 1234.

![](https://files.readme.io/d24735b-image.png)

## Final Charge Response   [Skip link to Final Charge Response](https://developers.tap.company/docs/qpay\#final-charge-response)

Once the payment with QPay is done, you will receive the status of the charge either through [API](https://developers.tap.company/reference/retrieve-a-charges) or a [webhook notification](https://developers.tap.company/docs/webhook), here is how a CAPTURED QPay payment response looks like.

JSON

```rdmd-code lang-json theme-light
{
  "id": "chg_TS07A0320241133g5RO1906000",
  "object": "charge",
  "live_mode": false,
  "customer_initiated": true,
  "api_version": "V2",
  "method": "GET",
  "status": "CAPTURED",
  "amount": 1,
  "currency": "QAR",
  "threeDSecure": true,
  "card_threeDSecure": false,
  "save_card": false,
  "product": "GOSELL",
  "description": "Test Description",
  "metadata": {
    "udf1": "Metadata 1"
  },
  "transaction": {
    "timezone": "UTC+03:00",
    "created": "1718796783000",
    "expiry": {
      "period": 30,
      "type": "MINUTE"
    },
    "asynchronous": false,
    "amount": 1,
    "currency": "QAR"
  },
  "reference": {
    "track": "tck_TS03A0520241133Oh491906234",
    "payment": "0519241133062344298",
    "transaction": "txn_01",
    "order": "ord_01",
    "gateway": "00"
  },
  "response": {
    "code": "000",
    "message": "Captured"
  },
  "gateway": {
    "response": {
      "code": "0000",
      "message": "Payment Processed Successfully"
    }
  },
  "card": {
    "object": "card",
    "first_six": "531801",
    "first_eight": "",
    "scheme": "NAPS",
    "brand": "MASTERCARD",
    "type": "DEBIT",
    "last_four": "2742",
    "name": "",
    "expiry": {},
    "issuer_name": "",
    "issuer_country": ""
  },
  "receipt": {
    "id": "200519241133063627",
    "email": true,
    "sms": true
  },
  "customer": {
    "id": "cus_TS05A0520241133Hs491906640",
    "first_name": "test",
    "last_name": "test",
    "email": "test@test.com",
    "phone": {
      "country_code": "965",
      "number": "51234567"
    }
  },
  "merchant": {
    "country": "KW",
    "currency": "KWD",
    "id": "599424"
  },
  "source": {
    "object": "source",
    "type": "CARD_NOT_PRESENT",
    "payment_type": "DEBIT",
    "channel": "INTERNET",
    "id": "src_qa.qpay",
    "on_file": false,
    "payment_method": "QPAY"
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
      "id": "activity_TS06A0620241133c4HR1906047",\
      "object": "activity",\
      "created": 1718796783000,\
      "status": "INITIATED",\
      "currency": "QAR",\
      "amount": 1,\
      "remarks": "charge - created",\
      "txn_id": "chg_TS07A0320241133g5RO1906000"\
    },\
    {\
      "id": "activity_TS07A0420241138Fj4q1906156",\
      "object": "activity",\
      "created": 1718797084156,\
      "status": "CAPTURED",\
      "currency": "QAR",\
      "amount": 1,\
      "remarks": "charge - captured",\
      "txn_id": "chg_TS07A0320241133g5RO1906000"\
    }\
  ],
  "auto_reversed": false
}

```

Updated8 months ago

* * *