Here is the guide for platforms to initiate transactions. A charge request is the foundation for processing payments in your platform. This guide will help you understand how to create a charge request and the necessary parameters involved.

Here is the CURL

JSON

```rdmd-code lang-json theme-light
curl --location 'https://api.tap.company/v2/charges/' \
--header 'Authorization: Bearer sk_live_xxxx' \
--header 'Content-Type: application/json' \
--data-raw '{
	"amount": 1,
	"currency": "KWD",
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
	"merchant": {
		"id": "merchant_xxxx"
	},
	"source": {
		"id": "src_cards"
	},
	"post": {
		"url": "http://example.com/postUrl"
	},
	"redirect": {
		"url": "http://example.com/redirectUrl"
	},
	"platform": {
		"id": "commerce_platform_xxxx"
	}
}'

```

Updated7 months ago

* * *