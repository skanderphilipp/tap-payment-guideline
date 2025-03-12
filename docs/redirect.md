## Overview   [Skip link to Overview](https://developers.tap.company/docs/redirect\#overview)

This page guides you to initiate a single payment method using APIs and redirect flow. You can use it with any payment method supported by Tap.

> ## 📘
>
> Redirect payment flow requires `redirect_url` in the API request. After payment is completed, the user will be redirected to this URL.

* * *

## Step 1: Choose the payment method source   [Skip link to Step 1: Choose the payment method source](https://developers.tap.company/docs/redirect\#step-1-choose-the-payment-method-source)

Each payment method has a specific `source_id` as follows:

- **src\_card**: Visa, MasterCard, AMEX, and mada
- **src\_sa.mada**: mada
- **src\_kw.knet**: KNET
- **src\_bh.benefit**: Benefit
- **src\_om.omannet**: Omannet
- **src\_eg.fawry**: Fawry
- **src\_apple\_pay**: Apple-Pay

Choose the `source_id` of the payment method you want to initiate.

* * *

## Step 2: Initiate a request   [Skip link to Step 2: Initiate a request](https://developers.tap.company/docs/redirect\#step-2-initiate-a-request)

Make a [`\charge`](https://developers.tap.company/docs/redirect) request, specifying the payment method source in the `source.id`.

JSON

```rdmd-code lang-json theme-light
"source": {
    "id": "src_kw.knet"
  },

```

Provide a redirect URL, where the user will be redirected after completing the transaction.

JSON

```rdmd-code lang-json theme-light
"redirect": {
    "url": "http://your_website.com/redirect_url"
  }

```

* * *

## Step 3: Redirect user to the payment page   [Skip link to Step 3: Redirect user to the payment page](https://developers.tap.company/docs/redirect\#step-3-redirect-user-to-the-payment-page)

In the response of the `\charge` request, you'll receive a `transaction.url` containing a URL for the payment page.

JSON

```rdmd-code lang-json theme-light
"transaction": {
    "authorization_id": "348683",
    "timezone": "UTC+03.00",
    "created": "1234343434",
    "url": "https://url.com/payment_url"
  }

```

The user should be redirected to this URL, provide the required payment information, and complete the transaction.

> ## 📘
>
> For KNET and Benefit, the URL will contains a direct link to KNET and Benefit page respectively.

* * *

## Step 4: Retrieve the transaction   [Skip link to Step 4: Retrieve the transaction](https://developers.tap.company/docs/redirect\#step-4-retrieve-the-transaction)

When the user is redirected to your `redirect_url`, you'll receive `tap_id`. Make a `\charge` request to retrieve the transaction details, specifying the `charge_id` contained in `tap_id`.

Retrieve a Charge

```rdmd-code lang-curl theme-light
curl --request GET \
  --url https://api.tap.company/v2/charges/chg_TS020420211019Ja242609987 \
  --header 'authorization: Bearer sk_test_XKokBfNWv6FIYuTMg5sLPjhJ' \
  --data '{}'

```

Response

```rdmd-code lang-json theme-light
{ "id": "chg_TS020420211019Ja242609987",
  "object": "charge",
  "live_mode": false,
  "api_version": "V2",
  "method": "GET",
  "status": "CANCELLED",
  "amount": 1.000,
  "currency": "BHD",
  "threeDSecure": true,
  "card_threeDSecure": false,
  "save_card": false,
  "merchant_id": "",
  "product": "",
  "statement_descriptor": "Sample",
  "description": "Test Description",
  "metadata": { "udf1": "test 1", "udf2": "test 2" },
  "transaction": {
      "timezone": "UTC+03:00",
      "created": "1632651545003",
      "expiry": { "period": 30, "type": "MINUTE" },
      "asynchronous": false,
      "amount": 1.000,
      "currency": "BHD"
  },
  "reference": {
      "id": "ref_BoajZCHlFDnLsUbyBygLkB",
      "track": "tck_TS030520211019Yx942609049",
      "payment": "5726211019090490134",
      "gateway": "00",
      "transaction": "txn_0001",
      "order": "ord_0001"
  },
  "response": {
      "code": "302",
      "message": "Cancelled"
  },
  "receipt": { "id": "205026211019099018", "email": false, "sms": true }, "customer": { "first_name": "test", "middle_name": "test", "last_name": "test", "email": "test@test.com", "phone": { "country_code": "965", "number": "50000000" } }, "source": { "object": "source", "type": "CARD_NOT_PRESENT", "payment_type": "DEBIT", "payment_method": "BENEFIT", "channel": "INTERNET", "id": "src_bh.benefit" }, "redirect": { "status": "SUCCESS", "url": "https://noonera.com/demo/redirect.php" }, "post": { "status": "SUCCESS", "url": "https://noonera.com/demo/post.php" } }

```

Updatedover 1 year ago

* * *