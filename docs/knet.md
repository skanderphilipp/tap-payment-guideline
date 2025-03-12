> ## 📘  It's a Redirection Payment Page Flow

Redirection on the KNET payment page is a must, to enter the card information and complete the processing.

Knet accepts KWD currency only. It supports authorization now.

**KFAST:** KNET also provides the save card functionality, called [KFAST](https://developers.tap.company/docs/kfast).

* * *

# API Call for KNET   [Skip link to API Call for KNET](https://developers.tap.company/docs/knet\#api-call-for-knet)

Sample to control the source object in the [charge API](https://developers.tap.company/reference/create-a-charge): "src\_kw.knet" with currency 'KWD' only

JSON

```rdmd-code lang-json theme-light
{
...
	"currency": "KWD",
	"source": {
		"id": "src_kw.knet"
}
"post": {
    "url": "https://webhook.site/fd8b0712-d70a-4280-8d6f-9f14407b3bbd"
 },
 "redirect": {
    "url": "https://customer.redirection_url"
  }
...
}

```

* * *

## API Response   [Skip link to API Response](https://developers.tap.company/docs/knet\#api-response)

A transaction URL is expected in the API response details. This will redirect the customer to the Benefit Payment Page

JSON

```rdmd-code lang-json theme-light
{
...
"id": "chg_TS05A1320231018Hy56070XXXX",
"status": "INITIATED",
"transaction": {
	 "timezone": "UTC+03:00",
	 "created": "1671563769240",
	 "url": "<https://sandbox.payments.tap.company/test_gosell/v2/payment/tap_process.aspx?chg=d6aPjTalvIV03hWrGnROvO3i8B2ED7hkBbPL8PY%2fzEY%3d">,
 "expiry": {
 	"period": 30,
	 "type": "MINUTE"
	  },
...
}

```

* * *

## KNET payment page   [Skip link to KNET payment page](https://developers.tap.company/docs/knet\#knet-payment-page)

Customer experience journey

![](https://files.readme.io/cf91e5e-image_256.png)

* * *

## Post payment details   [Skip link to Post payment details](https://developers.tap.company/docs/knet\#post-payment-details)

Sample [webhook](https://developers.tap.company/docs/webhook) response (post payment details)

SampleHeader

```rdmd-code lang-json theme-light
"id": "chg_TS05A1320231018Hy56070XXXX",
  "object": "charge",
  "live_mode": false,
  "api_version": "V2",
  "method": "POST",{
  "status": "CAPTURED",
  "amount": 0.5,
  "currency": "KWD",
  "threeDSecure": true,
  "card_threeDSecure": false,
  "save_card": false,
  "merchant_id": "",
  "product": "",
  "statement_descriptor": "Sample",
  "description": "Test Description",
  "metadata": {
    "udf1": "test 1",
    "udf2": "test 2"
  },
  "transaction": {
    "authorization_id": "B63465",
    "timezone": "UTC+03:00",
    "created": "1671563769240",
    "expiry": {
      "period": 30,
      "type": "MINUTE"
    },
    "asynchronous": false,
    "amount": 0.5,
    "currency": "KWD"
  },
  "reference": {
    "track": "tck_TS010920221916Hr112012834",
    "payment": "9720221916128348054",
    "gateway": "202235421476242",
    "acquirer": "235410001666",
    "transaction": "txn_0001",
    "order": "ord_0001"
  },
  "response": {
    "code": "000",
    "message": "Captured"
  },
  "gateway": {
    "response": {
      "code": "00",
      "message": "CAPTURED"
    }
  },
  "receipt": {
    "id": "209020221916128803",
    "email": true,
    "sms": false
  },
  "customer": {
    "id": "cus_TS020920221916q8YJ2012896",
    "first_name": "Waleed",
    "last_name": "Asghar",
    "email": "w.asghar@tap.company",
    "phone": {
      "country_code": "971",
      "number": "586275033"
    }
  },
  "merchant": {
    "country": "BH",
    "currency": "KWD",
    "id": "18778851"
  },
  "source": {
    "object": "source",
    "type": "CARD_NOT_PRESENT",
    "payment_type": "DEBIT",
    "payment_method": "KNET",
    "channel": "INTERNET",
    "id": "src_kw.knet"
  },
  "redirect": {
    "status": "PENDING",
    "url": "https://webhook.site/9819d5ef-506a-4d1e-a0c3-072ccfcd95a3"
  },
  "post": {
    "attempt": 1,
    "status": "PENDING",
    "url": "https://webhook.site/9819d5ef-506a-4d1e-a0c3-072ccfcd95a3"
  },
  "activities": [\
    {\
      "id": "activity_TS070920221916t8HK2012928",\
      "object": "activity",\
      "created": 1671563769240,\
      "status": "INITIATED",\
      "currency": "KWD",\
      "amount": 0.5,\
      "remarks": "charge - created"\
    },\
    {\
      "id": "activity_TS043920221936t3PX2012101",\
      "object": "activity",\
      "created": 1671564999101,\
      "status": "CAPTURED",\
      "currency": "KWD",\
      "amount": 0.5,\
      "remarks": "charge - captured"\
    }\
  ],
  "auto_reversed": false
}

```

```rdmd-code lang-Text theme-light
hash	        13a541064cd5da7bb309132acf4a7b9913c26baa64f3de2bfd064fXXXXXXXXXX
hashstring	  66f72458a90ce13bda69da99cf2124a8384a2b99e812fcb2431995XXXXXXXXXX
content-type	application/json
accept	      text/plain, application/json, application/cbor, application/*+json, */*

```

Updated8 months ago

* * *