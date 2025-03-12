Benefit is a Bahrain-based payment method that allows customers to make online payments with their Benefit debit cards.

> ## ❗️  Benefit does not support authorization transactions

# Benefit Integration   [Skip link to Benefit Integration](https://developers.tap.company/docs/benefit\#benefit-integration)

You can integrate the Benefit payment method into your website and mobile app through Tap in two ways:

1. Utilizing our [Web Card SDK](https://developers.tap.company/docs/card-sdk-web-v2) for a smooth in-app payment flow.
2. Redirecting users to the Benefit payment page.

> ## 📘  In order to enable Benefit on your Tap account, please make sure to contact your account manager or contact us at [support@tap.company](mailto:support@tap.company)

## Accept Benefit Cards in the Embedded Web SDKs   [Skip link to Accept Benefit Cards in the Embedded Web SDKs](https://developers.tap.company/docs/benefit\#accept-benefit-cards-in-the-embedded-web-sdks)

The first option is mainly for adding Benefit in a web environment, by using one of our Web Card SDKs, either [V1](https://developers.tap.company/docs/card-sdk-web-v1) or [V2](https://developers.tap.company/docs/card-sdk-web-v2).

Once you enable the Web SDK to accept debit cards, your customers can enter their Benefit card details directly into the SDK, which securely tokenizes the card information.

To complete the payment and deduct the amount from the customer, make sure to pass the token generated (within 5 minutes of creating it), to the `source.id` field of our [create a charge API](https://developers.tap.company/reference/create-a-charge) endpoint, ensuring the currency is set to **BHD**. Upon calling the API, the payment will have a status of INITIATED. You will then need to open the `transaction.url` from the charge response in a browser, where the customer can enter their PIN to finalize the transaction, as demonstrated below.

> ## ❗️  Benefit only supports payments in BHD

![](https://files.readme.io/dbaa47a-Screenshot_2024-07-01_at_12.44.55_PM.png)

## Redirect to Benefit Payment Page   [Skip link to Redirect to Benefit Payment Page](https://developers.tap.company/docs/benefit\#redirect-to-benefit-payment-page)

The most common integration method for Benefit is redirecting customers to the Benefit payment page. This approach works for both web and mobile integrations, allowing customers to enter their card details, verify the payment with a PIN sent to their phone, and complete the transaction entirely on the Benefit page.

This option can be done by calling our create a charge API and passing in the `source.id` field the value **src\_bh.benefit**. Similar to the first option, the payment after calling the charge API, will have a status of INITIATED in the response and you will then need to open the `transaction.url` from the charge response in a browser, where the customer can enter their PIN to finalize the transaction.

Below is a sample of the charge API request/response to follow in order to achieve the redirection to Benefit page.

### Charge API Request   [Skip link to Charge API Request](https://developers.tap.company/docs/benefit\#charge-api-request)

Make sure to call the [create a charge API](https://developers.tap.company/reference/create-a-charge) and pass the correct source as well as using currency **BHD** only.

JSON

```rdmd-code lang-json theme-light
{
...
	"currency": "BHD",
	"source": {
		"id": "src_bh.benefit"
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

### Charge API Response   [Skip link to Charge API Response](https://developers.tap.company/docs/benefit\#charge-api-response)

A transaction URL is expected in the API response details. This will redirect the customer to the Benefit Payment Page once you open it a browser/webview.

JSON

```rdmd-code lang-jsx theme-light
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

### Benefit Payment Page Sample   [Skip link to Benefit Payment Page Sample](https://developers.tap.company/docs/benefit\#benefit-payment-page-sample)

In the image below, you can see how the customer is redirected to the Benefit page to enter their card details and PIN.

![](https://files.readme.io/ef3df92-image_247.png)

# Webhook for Final Charge Response   [Skip link to Webhook for Final Charge Response](https://developers.tap.company/docs/benefit\#webhook-for-final-charge-response)

After the customer submits the card details and PIN, and proceeds to Pay with Benefit in either of the options mentioned above, the final charge response with the updated status of the payment, can be viewed using [webhook](https://developers.tap.company/docs/webhook) or using the [retrieve charge API](https://developers.tap.company/reference/retrieve-a-charges).

Please refer to the below expected charge response sample.

JSONHeaders

```rdmd-code lang-json theme-light
{
"id": "chg_TS05A1320231018Hy56070XXXX",
"object": "charge",
"live_mode": false,
"customer_initiated": true,
"api_version": "V2",
"method": "POST",
"status": "CAPTURED",
"amount": 100.0,
"currency": "BHD",
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
"authorization_id": "123456",
"timezone": "UTC+03:00",
"created": "1686133093034",
"expiry": {
"period": 30,
"type": "MINUTE"
},
"asynchronous": false,
"amount": 100.0,
"currency": "BHD"
},
"reference": {
"track": "tck_TS03A1320231018e5D80706659",
"payment": "1307231018066595165",
"gateway": "202315888830649",
"acquirer": "315810000083",
"transaction": "txn_0001",
"order": "iphoe_13"
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
"id": "201307231018065637",
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
"currency": "BHD",
"id": "18695485"
},
"source": {
"object": "source",
"type": "CARD_NOT_PRESENT",
"payment_type": "DEBIT",
"payment_method": "BENEFIT",
"channel": "INTERNET",
"id": "src_bh.benefit"
},
"redirect": {
"status": "PENDING",
"url": "checkout.com/website"
},
"post": {
"attempt": 1,
"status": "PENDING",
"url": "<https://webhook.site/fd8b0712-d70a-4280-8d6f-9f14407b3bbd>"
},
"activities": [\
{\
"id": "activity_TS02A1320231018Xe560706737",\
"object": "activity",\
"created": 1686133093034,\
"status": "INITIATED",\
"currency": "BHD",\
"amount": 100.0,\
"remarks": "charge - created"\
},\
{\
"id": "activity_TS06A0620231019Jw150706351",\
"object": "activity",\
"created": 1686133146351,\
"status": "CAPTURED",\
"currency": "BHD",\
"amount": 100.0,\
"remarks": "charge - captured"\
}\
],
"auto_reversed": false
}

```

```rdmd-code lang-text theme-light
hash	      13a541064cd5da7bb309132acf4a7b9913c26baa64f3de2bfd064fXXXXXXXXXX
hashstring	  66f72458a90ce13bda69da99cf2124a8384a2b99e812fcb2431995XXXXXXXXXX
content-typeapplication/json
accept	      text/plain, application/json, application/cbor, application/*+json, */*

```

# Benefit Card Saving   [Skip link to Benefit Card Saving](https://developers.tap.company/docs/benefit\#benefit-card-saving)

> ## 🚧  Saved Benefit cards can be used for future customer-initiated transactions, though a PIN will need to be entered each time.

Tap now supports tokenization and saving of Benefit Cards, improving both the payment experience and acceptance rates. After capturing the first payment with Benefit and setting `"save_card": true` in the charge request, you'll receive a customer ID (cus\_xxx) and card ID (card\_xxx) in the response. These can be used for future transactions with the saved card.

Instead of re-entering card details, you can [generate a token](https://developers.tap.company/reference/create-a-token-from-saved-card) for the saved card. Pass this token (tok\_xxx) to the `source.id` field of the charge API. The customer will only need to enter their PIN by accessing the `transaction.url` provided in the response to complete the payment.

Updated6 months ago

* * *