Payments webhook is a server-to-server call(also known as IPN "Instant Payment Notification"), that allows merchants to receive the post-payment details to automate and synchronize their internal ERPs by checking the actual payment status and other technical details, as per requirements.

It's supported with all our APIs, SDKs & Libraries where it is required to be.

Tap also triggers the webhooks for different payment events, such as when a payment is completed, when a customer views a bill, when a recurring payment occurred, etc.

* * *

## Webhook Requires   [Skip link to Webhook Requires](https://developers.tap.company/docs/webhook\#webhook-requires)

Following the steps below

1. Merchants need to create their own endpoint server page(usually with the post method) which can receive the webhooks.
2. Make sure your endpoint URL is active and working smoothly, and ready to accept webhooks.
3. Define the webhook endpoint URL in the API/SDK call (parameter POST:"url"), when required.

JSON

```rdmd-code lang-json theme-light

{
"post": {
    "url": "https://webhook.site/fd8b0712-d70a-4280-8d6f-9f14407b3bbd"
   },
}

```

* * *

## What are webhooks   [Skip link to What are webhooks](https://developers.tap.company/docs/webhook\#what-are-webhooks)

Webhooks refer to a combination of elements that collectively create a notification and reaction system within a larger integration.

Metaphorically, webhooks are like a phone number that Tap calls to notify you of activity in your payment transaction lifecycle. The activity could be the completion of payment or a successful charge within a Subscription. The webhook endpoint is the person answering that call who takes actions based on the specific information it receives.

Non-metaphorically, the webhook endpoint is just more code on your server, which could be written in Ruby, PHP, Node.js, or whatever. The webhook endpoint has an associated URL (e.g., [https://example.com/webhooks](https://example.com/webhooks)). The Tap notifications are Event objects. This Event object contains all the relevant parameters of the API response, including the amount, currency, transaction reference, and status of the transaction. The webhook endpoint uses the charge details to take any required actions, such as indicating that the payment is completed.

## When to use webhooks   [Skip link to When to use webhooks](https://developers.tap.company/docs/webhook\#when-to-use-webhooks)

Many events that occur within a Tap account have synchronous results–immediate and direct–to an executed request. For example, a successful request to create a customer immediately returns a Customer object. Such requests don’t require webhooks, as the key information is already available.

Other events that occur within a Tap Payment Ecosystem are asynchronous: happening at a later time and not directly in response to your code’s execution. Most commonly these involve:

The completion of a Charge Transaction

The payment of a due Invoice

Individual Charges within a Subscription

With these and similar APIs, Tap needs to notify your integration about changes to the status of an object so your integration can take subsequent steps.

The specific actions your webhook endpoint may take differs based upon the event. Some examples include:

Updating a customer’s payment record in your database when a subscription payment succeeds

Making adjustments to an invoice when it’s attempted (but before it’s been paid)

Logging an accounting entry when an invoice is paid

Webhooks can also be used to provide state and API responses to services or systems that use Tap data for things like replication, analytics, or alerting.

> ## 📘  Best Practice
>
> In case, after a successful payment capture, if the user closes the browser or if the internet connection is not available till the customer is redirected back to the Merchant Website/App, POST URL is a sure mechanism to get notified of the final payment status. Although POST URL is optional, we highly recommend implementing it.

> ## ❗️  Important notes
>
> 1- If the POST URL is not accessible, the posting of the response payload will be failed. There will be two more retry attempts before the status of the POST is updated as ERROR. You can find the POST status in the API Response
>
> 2- Only raw data will be posted, make sure to send raw data to the POST URL. The URL should accept post data for captured or failed transactions only , if the transaction status is INITIATED or ABANDONED no data will be posted and post status will be PENDING.
>
> 3- The post data cannot be posted to local host. If the data did not reach the URL it will show Error.
>
> 4- If the post data are not received on post URL , check the SSLS ,if you are using open source certificate, you will not be able to post the response on your website.

## Webhook Example for a Charges Response   [Skip link to Webhook Example for a Charges Response](https://developers.tap.company/docs/webhook\#webhook-example-for-a-charges-response)

JSON

```rdmd-code lang-json theme-light

{
    "method": "POST",
    "url": "https://webhook.site/25c5e885-216b-4d5f-bcbf-8e5d0d20b76f",
    "headers": [\
        {\
            "name": "connection",\
            "value": "close"\
        },\
        {\
            "name": "accept-encoding",\
            "value": "gzip,deflate"\
        },\
        {\
            "name": "user-agent",\
            "value": "Apache-HttpClient/4.5.13 (Java/18.0.2.1)"\
        },\
        {\
            "name": "host",\
            "value": "webhook.site"\
        },\
        {\
            "name": "content-length",\
            "value": "2480"\
        },\
        {\
            "name": "hash",\
            "value": "12dd1ed1008db28cfac344993564cc71da813a98b5c80d892744ee9bc3d8e76d"\
        },\
        {\
            "name": "hashstring",\
            "value": "356f77b65c5fc809ce5f1f6e2279932949ca86833867f6da5dbb92800df6238f"\
        },\
        {\
            "name": "content-type",\
            "value": "application/json"\
        },\
        {\
            "name": "accept",\
            "value": "text/plain, application/json, application/cbor, application/*+json, */*"\
        }\
    ],
    "bodySize": 2480,
    "postData": {
        "mimeType": "application/json",
        "text": "{\"id\":\"chg_TS05A4120230736x9K22710693\",\"object\":\"charge\",\"live_mode\":false,\"customer_initiated\":true,\"api_version\":\"V2\",\"method\":\"POST\",\"status\":\"CAPTURED\",\"amount\":1.0,\"currency\":\"SAR\",\"threeDSecure\":true,\"card_threeDSecure\":false,\"save_card\":true,\"merchant_id\":\"\",\"product\":\"\",\"description\":\"\",\"metadata\":{\"udf1\":\"test_data_1\",\"udf2\":\"test_data_2\",\"udf3\":\"test_data_3\"},\"transaction\":{\"timezone\":\"UTC+03:00\",\"created\":\"1698392202943\",\"expiry\":{\"period\":30,\"type\":\"MINUTE\"},\"asynchronous\":false,\"amount\":1.0,\"currency\":\"SAR\"},\"reference\":{\"track\":\"tck_TS04A4320230736To522710661\",\"payment\":\"4327230736106619650\",\"gateway\":\"mada_pg70983e7a-a686-40ba-83e2-c5e9f4074fe5\",\"acquirer\":\"230004002581\",\"transaction\":\"txn_0001\",\"order\":\"ord_0001\"},\"response\":{\"code\":\"000\",\"message\":\"Captured\"},\"security\":{\"threeDSecure\":{\"status\":\"Y\"}},\"gateway\":{\"response\":{\"code\":\"000\",\"message\":\"Approved\"}},\"card\":{\"id\":\"card_IIGi4523416sFHe27jJ9E589\",\"object\":\"card\",\"first_six\":\"446404\",\"first_eight\":\"44640400\",\"scheme\":\"MADA\",\"brand\":\"VISA\",\"last_four\":\"0007\"},\"receipt\":{\"id\":\"204327230736104914\",\"email\":true,\"sms\":true},\"customer\":{\"id\":\"cus_TS07A5420232136o2K52709053\",\"first_name\":\"Majdi\",\"middle_name\":\"Abdullah\",\"last_name\":\"Al Khowaiter\",\"email\":\"m.ghgjhgj@tap.company\",\"phone\":{\"country_code\":\"966\",\"number\":\"51234567\"}},\"merchant\":{\"country\":\"SA\",\"currency\":\"SAR\",\"id\":\"25145693\"},\"source\":{\"object\":\"token\",\"type\":\"CARD_NOT_PRESENT\",\"payment_type\":\"DEBIT\",\"payment_method\":\"MADA\",\"channel\":\"INTERNET\",\"id\":\"tok_nLKq4223436fVYL27Nj9P855\"},\"redirect\":{\"status\":\"PENDING\",\"url\":\"http://your_website.com/redirecturl\"},\"post\":{\"attempt\":1,\"status\":\"PENDING\",\"url\":\"https://webhook.site/25c5e885-216b-4d5f-bcbf-8e5d0d20b76f\"},\"activities\":[{\"id\":\"activity_TS03A4420230736Rb512710536\",\"object\":\"activity\",\"created\":1698392202943,\"status\":\"INITIATED\",\"currency\":\"SAR\",\"amount\":1.0,\"remarks\":\"charge - created\"},{\"id\":\"activity_TS07A1320230737j1H42710453\",\"object\":\"activity\",\"created\":1698392233453,\"status\":\"CAPTURED\",\"currency\":\"SAR\",\"amount\":1.0,\"remarks\":\"charge - captured\"}],\"auto_reversed\":false,\"payment_agreement\":{\"id\":\"payment_agreement_23Ah4423436I5R027SS9c330\",\"amount_variability\":\"VARIABLE\",\"type\":\"UNSCHEDULED\",\"total_payments_count\":1,\"contract\":{\"id\":\"card_IIGi4523416sFHe27jJ9E589\",\"customer_id\":\"cus_TS07A5420232136o2K52709053\",\"type\":\"SAVED_CARD\"},\"metadata\":{\"txn_type\":\"CHARGE\",\"txn_id\":\"chg_TS05A4120230736x9K22710693\",\"terminal_id\":\"ter_g6P51020221643Rj631205942\"}}}"
    }
}

```

## Webhook Example for an Authorize Response   [Skip link to Webhook Example for an Authorize Response](https://developers.tap.company/docs/webhook\#webhook-example-for-an-authorize-response)

JSON

```rdmd-code lang-json theme-light

{
    "method": "POST",
    "url": "https://webhook.site/25c5e885-216b-4d5f-bcbf-8e5d0d20b76f",
    "headers": [\
        {\
            "name": "connection",\
            "value": "close"\
        },\
        {\
            "name": "accept-encoding",\
            "value": "gzip,deflate"\
        },\
        {\
            "name": "user-agent",\
            "value": "Apache-HttpClient/4.5.13 (Java/18.0.2.1)"\
        },\
        {\
            "name": "host",\
            "value": "webhook.site"\
        },\
        {\
            "name": "content-length",\
            "value": "2188"\
        },\
        {\
            "name": "hashstring",\
            "value": "da91e16a4c840a3c9826e454b255d1980cb9d95e5b783ed3d2c0e69b1b774f29"\
        },\
        {\
            "name": "content-type",\
            "value": "application/json"\
        },\
        {\
            "name": "accept",\
            "value": "text/plain, application/json, application/cbor, application/*+json, */*"\
        }\
    ],
    "bodySize": 2188,
    "postData": {
        "mimeType": "application/json",
        "text": "{\"id\":\"auth_TS04A1720230745Rt2a2710607\",\"object\":\"authorize\",\"customer_initiated\":true,\"authorize_debit\":false,\"live_mode\":false,\"api_version\":\"V2\",\"status\":\"AUTHORIZED\",\"amount\":100.0,\"currency\":\"SAR\",\"threeDSecure\":true,\"save_card\":true,\"merchant_id\":\"\",\"product\":\"\",\"transaction\":{\"authorization_id\":\"125468\",\"timezone\":\"UTC+03:00\",\"created\":\"1698392719404\",\"expiry\":{\"period\":30,\"type\":\"MINUTE\"},\"asynchronous\":false,\"amount\":100.0,\"currency\":\"SAR\"},\"reference\":{\"track\":\"tck_TS02A2020230745q4MN2710966\",\"payment\":\"2027230745109668360\",\"gateway\":\"123456789\",\"acquirer\":\"330004125468\",\"transaction\":\"txn_0001\",\"order\":\"ord_0001\"},\"response\":{\"code\":\"001\",\"message\":\"Authorized\"},\"security\":{\"threeDSecure\":{\"id\":\"3ds_TS05A1920230745Tb452710404\",\"status\":\"Y\"}},\"acquirer\":{\"response\":{\"code\":\"00\",\"message\":\"Approved\"}},\"gateway\":{\"response\":{\"code\":\"0\",\"message\":\"Transaction Approved\"}},\"card\":{\"id\":\"card_2V741723717UcVF17Yh9O354\",\"object\":\"card\",\"first_six\":\"512345\",\"first_eight\":\"51234500\",\"scheme\":\"MASTERCARD\",\"brand\":\"MASTERCARD\",\"last_four\":\"0008\"},\"receipt\":{\"id\":\"202127230745103892\",\"email\":true,\"sms\":true},\"customer\":{\"id\":\"cus_TS02A4520230208p3P21710602\",\"first_name\":\"Majdi\",\"middle_name\":\"Alal\",\"last_name\":\"Alal\",\"email\":\"m.ghgjhgj@tap.company\",\"phone\":{\"country_code\":\"966\",\"number\":\"51234567\"}},\"source\":{\"object\":\"token\",\"type\":\"CARD_NOT_PRESENT\",\"payment_type\":\"CREDIT\",\"payment_method\":\"MASTERCARD\",\"channel\":\"INTERNET\",\"id\":\"tok_udpI1923445Jo1b27mi9I282\"},\"redirect\":{\"status\":\"PENDING\",\"url\":\"http://your_website.com/redirecturl\"},\"post\":{\"status\":\"PENDING\",\"url\":\"https://webhook.site/25c5e885-216b-4d5f-bcbf-8e5d0d20b76f\"},\"auto\":{\"status\":\"SCHEDULED\",\"type\":\"VOID\",\"time\":1},\"merchant\":{\"id\":\"25145693\"},\"description\":\"\",\"metadata\":{\"udf1\":\"test_data_1\",\"udf2\":\"test_data_2\",\"udf3\":\"test_data_3\"},\"payment_agreement\":{\"id\":\"payment_agreement_u6Xt2123445zy0z27yY9m684\",\"type\":\"UNSCHEDULED\",\"total_payments_count\":1,\"contract\":{\"id\":\"card_2V741723717UcVF17Yh9O354\",\"customer_id\":\"cus_TS02A4520230208p3P21710602\",\"type\":\"SAVED_CARD\"},\"metadata\":{\"txn_type\":\"AUTHORIZE\",\"txn_id\":\"auth_TS04A1720230745Rt2a2710607\",\"terminal_id\":\"ter_m1RM0420211322p4PH1002445\"}}}"
    }
}

```

## Validate the webhook (hashstring)   [Skip link to Validate the webhook (hashstring)](https://developers.tap.company/docs/webhook\#validate-the-webhook-hashstring)

You can ensure the secure webhook by calculating the "Hashstring" value received in the headers. If the 'hashstring' value match with the calculated value, means the post is secure and received by the Tap side.

**Calculating and validating a hashstring**

Collect the below values from the posted response (charge / authorize / invoice response)

| Variable | Object | Description |
| --- | --- | --- |
| id | charge/authorize/invoice | charge.id or authorize.id or invoice.id |
| amount | charge/authorize/invoice | charge.amount or authorize.amount or invoice.amount<br>Amount should be rounded with standard decimal value<br>(Ex: AED - 2.00, BHD - 3.000, KWD - 3.000, OMR - 3.000, QAR - 2.00, SAR - 2.00, USD - 2.00, EUR - 2.00, GBP - 2.00, EGP - 2.00) |
| currency | charge/authorize/invoice | charge.currency or authorize.currency or invoice.currency |
| gateway\_reference | charge/authorize | charge.reference.gateway or authorize.reference.gateway |
| payment\_reference | charge/authorize | charge.reference.payment or authorize.reference.payment |
| updated | invoice | invoice.updated |
| status | charge/authorize/invoice | charge.status or authorize.status or invoice.status |
| created | charge/authorize/invoice | charge.transaction.created or authorize.transaction.created or invoice.created |

PHP

```rdmd-code lang-php theme-light

<?php
// Get the passed data from the post response (charge / authorize / refund / invoice response)

$id = 'charge.id or authorize.id or refund.id or invoice.id';
$amount = 'charge.amount or authorize.amount or refund.amount or invoice.amount';
$currency = 'charge.currency or authorize.currency or refund.currency or invoice.currency';
$gateway_reference = 'charge.reference.gateway or authorize.reference.gateway or refund.reference.gateway';
$payment_reference = 'charge.reference.payment or authorize.reference.payment or refund.reference.payment';
$updated = 'invoice.updated';
$status = 'charge.status or authorize.status or refund.status or invoice.status';
$created = 'charge.transaction.created or authorize.transaction.created or refunud.created or invoice.created';

// Your Secret API Key Provided by Tap
$SecretAPIKey = "sk_test_XKokBfNWv6FIYuTMg5sLPjhJ";

// Charges - Create a hashstring from the posted response data + the data that are related to you.
$toBeHashedString = 'x_id' . $id . 'x_amount' . $amount . 'x_currency' . $currency . 'x_gateway_reference' . $gateway_reference . 'x_payment_reference' . $payment_reference . 'x_status' . $status . 'x_created' . $created . '';

// Authorize or Void - Create a hashstring from the posted response data + the data that are related to you.
$toBeHashedString = "x_id" . $id . "x_amount" . $amount . "x_currency" . $currency . "x_gateway_reference" . $gateway_reference . "x_payment_reference" . $payment_reference . "x_status" . $status . "x_created" . $created . '';

// Refund - Create a hashstring from the posted response data + the data that are related to you.
$toBeHashedString = "x_id" . $id . "x_amount" . $amount . "x_currency" . $currency . "x_gateway_reference" . $gateway_reference . "x_payment_reference" . $payment_reference . "x_status" . $status . "x_created" . $created . '';

// Invoice - Create a hashstring from the posted response data + the data that are related to you.
$toBeHashedString = 'x_id' . $id . 'x_amount' . $amount . 'x_currency' . $currency . 'x_updated' . $updated . 'x_status' . $status . 'x_created' . $created . '';

// Create your hashstring by passing concatinated string and your secret API Key
$myHashString = hash_hmac('sha256', $toBeHashedString, $SecretAPIKey);

// Legitimate the post request by comparing the hashstring you computed with the one posted in the header
if ($myHashString == $postedHashString) {
    echo "Secure Post";
} else {
    echo "Insecure Post";
}

```

> ## 👍  Best Practise
>
> While computing the hash string ensure that all parameters used are following the exact parameter specifications. The amount should be rounded with the standard decimal value (ISO Standard Currency Codes).

Updatedabout 1 month ago

* * *

Did this page help you?

Yes

No