# Overview   [Skip link to Overview](https://developers.tap.company/docs/stcpay\#overview)

STC Pay enables the customers who has account in their system to pay with phone number with entering the cards details, it is most preferable to the customers who don't know how to enter the card details or don't like to hold bank cards.

**Note:** STC Pay currently supports transactions in Saudi Riyal (SAR) only. And currently it does not support Authorize transactions and does not support recurring payments.

> ## 📘  In order to enable this payment method on your Tap account, please make sure to contact your account manager or contact us at [support@tap.company](mailto:support@tap.company)

# STC Pay Integration   [Skip link to STC Pay Integration](https://developers.tap.company/docs/stcpay\#stc-pay-integration)

To integrate STC Pay in your website or mobile app, at first you need to add this value `src_sa.stcpay` inside the source object as it is always in all the requests but with additional object in the source named **phone**, the source object will be like below

### The source object when create STC Pay transaction   [Skip link to The source object when create STC Pay transaction](https://developers.tap.company/docs/stcpay\#the-source-object-when-create-stc-pay-transaction)

JSON

```rdmd-code lang-json theme-light
...........,
"source": {
        "id": "src_sa.stcpay",
         "phone": {  // the phone number registerd in STC Pay
            "country_code": "966",
            "number": "557877988"
        }
    },
............

```

### Test Phone numbers for STC Pay   [Skip link to Test Phone numbers for STC Pay](https://developers.tap.company/docs/stcpay\#test-phone-numbers-for-stc-pay)

| Country Code | Phone Number | OTP(any) |
| --- | --- | --- |
| 966 | 557877988 | 123456 |
| 966 | 506027231 | 123456 |
| 966 | 537974429 | 123456 |
| 966 | 558646150 | 123456 |

Here we will guide you through the integration.

## Call Create Charge Request   [Skip link to Call Create Charge Request](https://developers.tap.company/docs/stcpay\#call-create-charge-request)

First, you need to call the create charge API and pass the currency as **SAR** and specify the `source.id` to be `src_sa.stcpay` and the registered phone number in STC Pay to pay with as shown above.

cURL

```rdmd-code lang-curl theme-light
curl --request POST \
     --url https://api.tap.company/v2/charges/ \
     --header 'Authorization: Bearer sk_test_XKokBfNWv6FIYuTMg5sLPjhJ' \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
  "amount": 10,
  "currency": "SAR",
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
      "country_code": 966,
      "number": 51234567
    }
  },
 "source": {
        "id": "src_sa.stcpay",
         "phone": { // the phone number here does not required to be the similar to the customer phone number.
            "country_code": "966",
            "number": "557877988"
        }
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

### Charge Response   [Skip link to Charge Response](https://developers.tap.company/docs/stcpay\#charge-response)

JSON

```rdmd-code lang-json theme-light
{
    "id": "chg_TS05A3120241229h3JR0508210",
    "object": "charge",
    "live_mode": false,
    "customer_initiated": true,
    "api_version": "V2",
    "method": "CREATE",
    "status": "INITIATED",
    "amount": 10.00,
    "currency": "SAR",
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
        "created": "1722860971210",
        "url": "",
        "expiry": {
            "period": 3,
            "type": "MINUTE"
        },
        "asynchronous": false,
        "amount": 10.00,
        "currency": "SAR"
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
            "country_code": "966",
            "number": "51234567"
        }
    },
    "merchant": {
        "country": "SA",
        "currency": "SAR",
        "id": ""
    },
    "source": {
        "object": "source",
        "id": "src_sa.stcpay",
        "phone": {
            "country_code": "966",
            "number": "557877988"
        },
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
            "id": "activity_TS05A3520241229Th4b0508590",\
            "object": "activity",\
            "created": 1722860971210,\
            "status": "INITIATED",\
            "currency": "SAR",\
            "amount": 10.00,\
            "remarks": "charge - created",\
            "txn_id": "chg_TS05A3120241229h3JR0508210"\
        }\
    ],
    "auto_reversed": false,
    "gateway_response": {
        "name": "STC_PAY",
        "request": {
            "amount": "10.00",
            "currency": "SAR",
            "reference": {
                "transaction": "chg_TS05A3120241229h3JR0508210",
                "invoice": ""
            },
            "configuration": {
                "show_result": "0",
                "hide_mobile_qr": "0",
                "frequency": {
                    "start": 30,
                    "interval": 30,
                    "count": 10,
                    "type": "SECOND"
                }
            }
        }
    }
}

```

## Update The Charge With The OTP   [Skip link to Update The Charge With The OTP](https://developers.tap.company/docs/stcpay\#update-the-charge-with-the-otp)

After you create the charge request the customer will receive an OTP from STC Pay then you have to get that OTP and update the charge request like bellow.

JSON

```rdmd-code lang-json theme-light
curl --location --request PUT 'https://api.tap.company/v2/charges/chg_TS05A3120241229h3JR0508210' \
--header 'Authorization: Bearer sk_test_XKokBfNWv6FIYuTMg5sLPjhJ' \
--header 'Content-Type: application/json' \
--data '{
    "gateway_response": {
       "name": "STC_PAY",
        "response": {
            "reference": {
                "otp":"123453"
            }
        }
    }
}
'

```

## Congratulations: You Captured The Payment!   [Skip link to Congratulations: You Captured The Payment!](https://developers.tap.company/docs/stcpay\#congratulations-you-captured-the-payment)

If the OTP is correct you will get a success response with status CAPTURED for this transaction.

JSON

```rdmd-code lang-json theme-light
{
    "id": "chg_TS05A3120241229h3JR0508210",
    "object": "charge",
    "live_mode": true,
    "customer_initiated": true,
    "api_version": "V2",
    "method": "UPDATE",
    "status": "CAPTURED",
    "amount": 10.00,
    "currency": "SAR",
    "threeDSecure": false,
    "card_threeDSecure": false,
    "save_card": false,
    "product": "GOSELL",
    "description": "Test Description",
    "metadata": {
        "udf1": "Metadata 1"
    },
    "transaction": {
        "timezone": "UTC+03:00",
        "created": "1723028016778",
        "expiry": {
            "period": 3,
            "type": "MINUTE"
        },
        "asynchronous": false,
        "amount": 10.00,
        "currency": "SAR"
    },
    "reference": {
        "track": "tck_TS03I3720241053y9TM0708517",
        "payment": "3707241053085173025",
        "transaction": "txn_01",
        "order": "ord_01",
        "gateway": "FT24220SQGXB"
    },
    "response": {
        "code": "000",
        "message": "Captured"
    },
    "gateway": {
        "response": {
            "code": "2",
            "message": "Paid"
        }
    },
    "receipt": {
        "id": "203807241053085072",
        "email": true,
        "sms": true
    },
    "customer": {
        "id": "cus_TS02I3820241053x0D10708841",
        "first_name": "test",
        "last_name": "test",
        "email": "test@test.com",
        "phone": {
            "country_code": "966",
            "number": "51234567"
        }
    },
    "merchant": {
        "country": "SA",
        "currency": "SAR",
        "id": ""
    },
    "source": {
        "object": "source",
        "type": "CARD_NOT_PRESENT",
        "channel": "INTERNET",
        "id": "src_sa.stcpay",
        "phone": {
            "country_code": "966",
            "number": "557877988"
        },
        "on_file": false,
        "payment_method": "STC_PAY"
    },
    "redirect": {
        "status": "SUCCESS",
        "url": "http://your_website.com/redirect_url"
    },
    "post": {
        "status": "SUCCESS",
        "url": "http://your_website.com/post_url"
    },
    "activities": [\
        {\
            "id": "activity_TS03I3820241053Rc9a0708872",\
            "object": "activity",\
            "created": 1723028016778,\
            "status": "INITIATED",\
            "currency": "SAR",\
            "amount": 10.00,\
            "remarks": "charge - created",\
            "txn_id": "chg_TS07I3620241053r2ML0708778"\
        },\
        {\
            "id": "activity_TS05I2220241054Mw2r0708036",\
            "object": "activity",\
            "created": 1723028062036,\
            "status": "CAPTURED",\
            "currency": "SAR",\
            "amount": 10.00,\
            "remarks": "charge - captured",\
            "txn_id": "chg_TS05A3120241229h3JR0508210"\
        }\
    ],
    "auto_reversed": false,
    "gateway_response": {
        "name": "STC_PAY",
        "request": {
            "amount": "10.00",
            "currency": "SAR",
            "reference": {
                "transaction": "chg_TS05A3120241229h3JR0508210",
                "invoice": ""
            },
            "configuration": {
                "show_result": "0",
                "hide_mobile_qr": "0",
                "frequency": {
                    "start": 30,
                    "interval": 30,
                    "count": 10,
                    "type": "SECOND"
                }
            }
        }
    }
}

```

Updated7 months ago

* * *