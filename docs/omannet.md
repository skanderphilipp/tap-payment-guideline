OmanNet allows customers to perform online payments using a OmanNet debit card.

# OmanNet Integration   [Skip link to OmanNet Integration](https://developers.tap.company/docs/omannet\#omannet-integration)

You can integrate the OmanNet payment method into your website and mobile app through Tap in two ways:

1. Utilizing our [Web Card SDK](https://developers.tap.company/docs/card-sdk-web-v2) and Mobile SDKs for a smooth in-app payment flow.
2. Redirecting users to the Tap hosted payment page.

> ## 📘  In order to enable OmanNet on your Tap account, please make sure to contact your account manager or contact us at [support@tap.company](mailto:support@tap.company)

## Accept OmanNet Cards in Embedded SDKs   [Skip link to Accept OmanNet Cards in Embedded SDKs](https://developers.tap.company/docs/omannet\#accept-omannet-cards-in-embedded-sdks)

The recommended option is usually using our SDKs for both web and mobile to accept OmanNet Debit cards. The Tap SDKs, will tokenize the OmanNet card submitted.

For example you can use our Web Card SDKs, either [V1](https://developers.tap.company/docs/card-sdk-web-v1) or [V2](https://developers.tap.company/docs/card-sdk-web-v2) for this integration.

Once you enable the SDK to accept debit cards, your customers can enter their OmanNet card details directly into the SDK, which securely tokenizes the card information.

To complete the payment and deduct the amount from the customer, make sure to pass the token generated (within 5 minutes of creating it), to the `source.id` field of our [create a charge API](https://developers.tap.company/reference/create-a-charge) endpoint, ensuring the currency is set to **OMR**. Upon calling the API, the payment will have a status of INITIATED. You will then need to open the `transaction.url` from the charge response in a browser, where the customer can enter the OTP sent to their phone number to complete the payment.

![](https://files.readme.io/d1caaba44aebf6515ac0728189adacc28d6c8d4d40457d327f135054e0bf7dec-image.png)

> ## ❗️  OmanNet only supports payments in OMR

## Redirect to Tap Hosted Payment Page   [Skip link to Redirect to Tap Hosted Payment Page](https://developers.tap.company/docs/omannet\#redirect-to-tap-hosted-payment-page)

If you are not using our SDKs but rather completing the integration solely with APIs, you can use the Tap Hosted payment page and only allow the OmanNet payment method to be available for the customer to complete his transaction. This approach works for both web and mobile integrations as well, allowing customers to enter their OmanNet card details in the Tap Hosted page, verify the payment with a OTP sent to their phone, and complete the transaction.

This option can be done by calling our create a charge API and passing in the `source.id` field the value **src\_omannet**. Similar to the first option, the payment after calling the charge API, will have a status of INITIATED in the response and you will then need to open the `transaction.url` from the charge response in a browser, where the customer can enter their OTP to finalize the transaction.

Below is a sample of the charge API request/response to follow in order to achieve the redirection to Tap hosted page with only OmanNet as the available payment method.

### Charge API Request   [Skip link to Charge API Request](https://developers.tap.company/docs/omannet\#charge-api-request)

Make sure to call the [create a charge API](https://developers.tap.company/reference/create-a-charge) and pass the correct source as well as using currency **OMR** only.

JSON

```rdmd-code lang-json theme-light
{
...
	"currency": "OMR",
	"source": {
		"id": "src_omannet"
}
"post": {
    "url": "https://webhook.site/fd8b0712-d70a-9f14407b3bbd"
 },
 "redirect": {
    "url": "https://customer.redirection_url"
  }
...
}

```

### Charge API Response   [Skip link to Charge API Response](https://developers.tap.company/docs/omannet\#charge-api-response)

A transaction URL is expected in the API response details. This will redirect the customer to the Tap Hosted Payment Page once you open it a browser/webview.

JSON

```rdmd-code lang-jsx theme-light
{
...
"id": "chg_TS05A1320231018Hy56070XXXX",
"status": "INITIATED",
"transaction": {
	 "timezone": "UTC+03:00",
	 "created": "1671563769240",
	 "url": "<https://sandbox.payments.tap.company/test_gosell/v2/payment/tap_process.aspx?chg=d6aPjTalvIV0O3i8B2ED7hkBbPL8PY%2fzEY%3d">,

 "expiry": {
 	"period": 30,
	 "type": "MINUTE"
	  },
...
}

```

### Accept OmanNet in Tap Hosted Payment Page Sample   [Skip link to Accept OmanNet in Tap Hosted Payment Page Sample](https://developers.tap.company/docs/omannet\#accept-omannet-in-tap-hosted-payment-page-sample)

In the image below, you can see how the customer can accept OmanNet cards in the Tap Hosted Payment page.

![](https://files.readme.io/65df37c407cfb807e954aa46a6052d738613387292c009a985b1695e60499eec-image.png)

# Webhook for Final Charge Response   [Skip link to Webhook for Final Charge Response](https://developers.tap.company/docs/omannet\#webhook-for-final-charge-response)

After the customer completes his payment with OmanNet in either of the options mentioned above, the final charge response with the updated status of the payment, can be viewed using [webhook](https://developers.tap.company/docs/webhook) or using the [retrieve charge API](https://developers.tap.company/reference/retrieve-a-charges).

Please refer to the below expected charge response sample.

JSON

```rdmd-code lang-json theme-light
{
    "id": "chg_TS07A2520241510KgXXXX",
    "object": "charge",
    "live_mode": false,
    "customer_initiated": true,
    "api_version": "V2",
    "method": "GET",
    "status": "CAPTURED",
    "amount": 4.123,
    "currency": "OMR",
    "threeDSecure": false,
    "card_threeDSecure": false,
    "save_card": false,
    "order_id": "7210055701315195",
    "product": "GOSELL",
    "description": "",
    "transaction": {
        "authorization_id": "052279",
        "timezone": "UTC+03:00",
        "created": "1723821025023",
        "expiry": {
            "period": 30,
            "type": "MINUTE"
        },
        "asynchronous": false,
        "amount": 4.13,
        "currency": "OMR"
    },
    "reference": {
        "track": "tck_TS05A4520241509Pp2XXXX",
        "payment": "2616241510085XXXX",
        "trace_id": "123456789XXXX",
        "transaction": "298079370500",
        "order": "7210055701315195",
        "acquirer": "422912052279",
        "gateway": "123456789012345"
    },
    "response": {
        "code": "000",
        "message": "Captured"
    },
    "security": {
        "threeDSecure": {
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
        "object": "card",
        "first_six": "422823",
        "first_eight": "42282300",
        "scheme": "OMANNET",
        "brand": "OMANNET",
        "last_four": "0001"
    },
    "receipt": {
        "id": "202616241510088210",
        "email": true,
        "sms": true
    },
    "customer": {
        "id": "cus_TS04A4520241509Jp2XXXX",
        "first_name": "Test Payer",
        "email": "testPayer@payment.com",
        "phone": {
            "country_code": "965",
            "number": "50000000"
        }
    },
    "merchant": {
        "country": "OM",
        "currency": "OMR",
        "id": "2777XXXX"
    },
    "source": {
        "object": "token",
        "type": "CARD_NOT_PRESENT",
        "payment_type": "DEBIT",
        "channel": "INTERNET",
        "id": "tok_jFc3724911eOGu12XXXX",
        "on_file": false,
        "payment_method": "OMANNET"
    },
    "activities": [\
        {\
            "id": "activity_TS04A2720241510m2R21608572",\
            "object": "activity",\
            "created": 1723821025023,\
            "status": "INITIATED",\
            "currency": "OMR",\
            "amount": 4.123,\
            "remarks": "charge - created",\
            "txn_id": "chg_TS07A2520241510KgXXXX"\
        },\
        {\
            "id": "activity_TS02A2820241510n2H31608853",\
            "object": "activity",\
            "created": 1723821028853,\
            "status": "CAPTURED",\
            "currency": "OMR",\
            "amount": 4.13,\
            "remarks": "charge - captured",\
            "txn_id": "chg_TS07A2520241510KgXXXX"\
        }\
    ],
    "auto_reversed": false
}

```

Updated6 months ago

* * *