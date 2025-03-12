This document provides a simple guide for integrating Tap Payments into both web and mobile applications, specifically tailored for PCI compliant merchants. It includes detailed instructions for encrypting cardholder data and processing payments securely. Merchants who are PCI compliant can encrypt the raw card data on their end and pass it to the Tap API for seamless payment processing.

# Card Encryption   [Skip link to Card Encryption](https://developers.tap.company/docs/encrypted-card-flow-pci\#card-encryption)

To ensure security, card details must be encrypted using the RSA algorithm provided by Tap. Here is the tap [test encryption keys](https://developers.tap.company/reference/testing-keys). We highly recommend to use your own encryption keys from your merchant account.

Below are the steps to encrypt card information.

## Obtain the RSA Public Key from tap   [Skip link to Obtain the RSA Public Key from tap](https://developers.tap.company/docs/encrypted-card-flow-pci\#obtain-the-rsa-public-key-from-tap)

Upon you submit your PCI and AOC certificate, tap will issue an RSA public key to perform the encryption. You can get the RSA Public Key from the tap Team.

## Prepare Data for Encryption   [Skip link to Prepare Data for Encryption](https://developers.tap.company/docs/encrypted-card-flow-pci\#prepare-data-for-encryption)

Ensure the card information is in JSON format:

json

```rdmd-code lang-json theme-light
{
  "number": "5123450000000008",
  "exp_month": "01",
  "exp_year": "2039",
  "cvc": "100",
  "name": "test user"
}

```

## Encrypt Card Information using RSA public key   [Skip link to Encrypt Card Information using RSA public key](https://developers.tap.company/docs/encrypted-card-flow-pci\#encrypt-card-information-using-rsa-public-key)

Encrypt the JSON data using the RSA public key. The encrypted card is now ready to be sent in the API request.

Public key

```rdmd-code lang-text theme-light
-----BEGIN PUBLIC KEY-----
ABCDENBgkqhkiG9w0BAQEFAAOCAQ0AMIIBCAKCAQEAubKi7U7Zdi/57F5pHkfxkCTbOnfEh+RicLd9dJqa4yBjW+7Nf4LbUGnqHjlVfOHs1Y6CSSqTHdyGHcEfjnEFKJX1Hfj/ViXmSyvxKsew5UZ6iPy57+3GiMvMc5hNCPqwMrLvhg1dX4cQXDb7+EkrzyvUtzxivkhZ9rbbOcz/bjV4aVqT7UV0ZWQvG3/g5nuzKg38AcCjz4YnLS6YsxZJISWKmgnMuFJqBfNMGkKcqIIiQletNb6Vze2K4pT2NMGpzg8YJvBtsdfsdfsfsdfdfdxm9hUdPeQWzlBJVwIRST==
-----END PUBLIC KEY-----

```

### Example Of The Encryption Function   [Skip link to Example Of The Encryption Function](https://developers.tap.company/docs/encrypted-card-flow-pci\#example-of-the-encryption-function)

JavaScript

```rdmd-code lang-javascript theme-light
function encryptWithRSA(value, publicKey) {
  const valueString = JSON.stringify(value);
  const encrypted = crypto.publicEncrypt(
    {
      key: publicKey,
      padding: crypto.constants.RSA_PKCS1_PADDING
    },
    Buffer.from(valueString, 'utf-8')
  );

  return encrypted.toString('base64');
}

```

Encrypted card might look like below (note that this is just an example)

Text

```rdmd-code lang-text theme-light
cEXqtyq7jWYR3tbkM0C31bQWzO3pewrA3B/vHyO/PqITT0HWwc16u6jNMVznqLxBhFTgQRSdlMgukJqWfRah1dhD9kz7f5g0B9kgC4UFsqRAcmmhYg4yhTD60gFRE6GEtywg/Wbs3L3GCaqmtfJlDJQGIklgt4Hu9PTDAYlw4d3gZIKnXlXH/y82t59niCGdlmChSv3bsNyO8mSnV852ZzNM3DLYKZaIfdRcd8l706lIqUTpdeQS5Wuw/UdLpKUHm864lkTSowC5fx5HyPxBkO4s0ZuUi8svTx0ivPhSmSUSblP7Q8GkpmNh8o1bdRoMb083TGVrTRyFI3ahQIPFdQ==

```

# Making API Requests   [Skip link to Making API Requests](https://developers.tap.company/docs/encrypted-card-flow-pci\#making-api-requests)

When making API requests to process payments with Tap Payments, it's essential to understand the different approaches available for handling encrypted card data.

## Understanding Integration Options   [Skip link to Understanding Integration Options](https://developers.tap.company/docs/encrypted-card-flow-pci\#understanding-integration-options)

### Option 1: Create a Token First, Then Make a Charge/Authorize Request   [Skip link to Option 1: Create a Token First, Then Make a Charge/Authorize Request](https://developers.tap.company/docs/encrypted-card-flow-pci\#option-1-create-a-token-first-then-make-a-chargeauthorize-request)

With this approach, you first create a token representing the encrypted card data before making a charge or authorize request.

#### Create a Token:   [Skip link to Create a Token:](https://developers.tap.company/docs/encrypted-card-flow-pci\#create-a-token)

1. Encrypt the card information using the RSA public key.
2. Send the encrypted card data to the Tap API via the token endpoint.
3. Receive a token.id representing the encrypted card data.

#### Make a Charge/Authorize Request Using the Token:   [Skip link to Make a Charge/Authorize Request Using the Token:](https://developers.tap.company/docs/encrypted-card-flow-pci\#make-a-chargeauthorize-request-using-the-token)

1. Use the token.id as the source.id in the charge or authorize endpoint.

Advantages include the ability to validate and store the token information before making the payment request.

### Option 2: Directly Make a Charge/Authorize Request with Encrypted Card Data   [Skip link to Option 2: Directly Make a Charge/Authorize Request with Encrypted Card Data](https://developers.tap.company/docs/encrypted-card-flow-pci\#option-2-directly-make-a-chargeauthorize-request-with-encrypted-card-data)

Alternatively, you can directly pass encrypted card data in the charge or authorize request without creating a token first.

#### Make a Charge/Authorize Request with Encrypted Card Data:   [Skip link to Make a Charge/Authorize Request with Encrypted Card Data:](https://developers.tap.company/docs/encrypted-card-flow-pci\#make-a-chargeauthorize-request-with-encrypted-card-data)

1. Encrypt the card information using the RSA public key.
2. Pass the encrypted card data as source.card in the charge or authorize endpoint.

Advantages include reducing the number of API calls required and potentially speeding up the transaction process.

By understanding these integration options, you can choose the approach that best suits your application's needs and workflow. You can discuss with the [developer experience team](mailto:integrations@tap.company) for more guidance.

Ensure that the secret key used for these endpoints are from the same merchant account. You can get further guidance from the [Developer Experience](mailto:integrations@tap.company) team at tap.

## Option 1 : Create a token and Create a Charge/Authorize   [Skip link to Option 1 : Create a token and Create a Charge/Authorize](https://developers.tap.company/docs/encrypted-card-flow-pci\#option-1--create-a-token-and-create-a-chargeauthorize)

You can pass the encrypted card via [token](https://developers.tap.company/docs/create-a-token-encrypted-card) API to create a `token.id` and pass it to the `source.id` of the [charges](https://developers.tap.company/docs/create-a-charge) API or [Authorize](https://developers.tap.company/docs/create-an-authorize) API

### Create a token   [Skip link to Create a token](https://developers.tap.company/docs/encrypted-card-flow-pci\#create-a-token-1)

You can pass the encrypted card to the token API via the parameter `crypted_data`

cURL

```rdmd-code lang-curl theme-light
curl --request POST \
     --url https://api.tap.company/v2/tokens/ \
     --header 'Authorization: Bearer sk_test_XKokBfNWv6FIYuTMg5sLPjhJ' \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
  "card": {
    "address_city": "Some city",
    "address_country": "Some country",
    "address_line1": "First line",
    "address_line2": "Second line",
    "address_state": "Royal State",
    "address_zip": "007",
    "crypted_data": "cEXqtyq7jWYR3tbkM0C31bQWzO3pewrA3B/vHyO/PqITT0HWwc16u6jNMVznqLxBhFTgQRSdlMgukJqWfRah1dhD9kz7f5g0B9kgC4UFsqRAcmmhYg4yhTD60gFRE6GEtywg/Wbs3L3GCaqmtfJlDJQGIklgt4Hu9PTDAYlw4d3gZIKnXlXH/y82t59niCGdlmChSv3bsNyO8mSnV852ZzNM3DLYKZaIfdRcd8l706lIqUTpdeQS5Wuw/UdLpKUHm864lkTSowC5fx5HyPxBkO4s0ZuUi8svTx0ivPhSmSUSblP7Q8GkpmNh8o1bdRoMb083TGVrTRyFI3ahQIPFdQ=="
  }
}
'

```

You will get the `token.id` in the response

JSON

```rdmd-code lang-json theme-light
{
	"id": "tok_MGmI37241418FNsU5cl50843",
	"status": "ACTIVE",
	"created": 1717597117843,
	"object": "token",
	"live_mode": false,
	"type": "CARD",
	"purpose": "CHARGE",
	"used": false,
	"card": {
		"id": "card_5Sgt37241418Fen55cm5P847",
		"object": "card",
		"on_file": false,
		"address": {
			"country": "Saudi",
			"city": "Kuwait city",
			"avenue": "Gulf",
			"street": "Salim",
			"line1": "Salmiya, 21"
		},
		"funding": "DEBIT",
		"fingerprint": "S6598GK124LgquRVCL0Vgu0mJPpIzMAQ21laYvZ73EI%3D",
		"brand": "MASTERCARD",
		"scheme": "MASTERCARD",
		"category": "Proprietary ATM",
		"exp_month": 1,
		"exp_year": 25,
		"last_four": "0008",
		"first_six": "512345",
		"first_eight": "51234500",
		"issuer": {
			"bank": "",
			"country": "US",
			"id": "bnk_LV04C1020240745l3MB0206269"
		}
	},
	"payment": {
		"id": "card_5Sgt37241418Fen55cm5P847",
		"on_file": false,
		"card_data": {
			"exp_month": 1,
			"exp_year": 25,
			"last_four": "0008",
			"first_six": "512345",
			"first_eight": "51234500",
			"address": {
				"country": "Saudi",
				"city": "Kuwait city",
				"avenue": "Gulf",
				"street": "Salim",
				"line1": "Salmiya, 21"
			}
		},
		"fingerprint": "S6598GK124LgquRVCL0Vgu0mJPpIzMAQ21laYvZ73EI%3D",
		"scheme": "MASTERCARD",
		"category": "Proprietary ATM",
		"issuer": {
			"bank": "",
			"country": "US",
			"id": "bnk_LV04C1020240745l3MB0206269"
		}
	},
	"merchant": {
		"id": "599424"
	},
	"client_ip": "192.168.1.20"
}

```

### Create a Charges/Authorize   [Skip link to Create a Charges/Authorize](https://developers.tap.company/docs/encrypted-card-flow-pci\#create-a-chargesauthorize)

Now you can pass the `token.id` as a `source.id` within [Charges](https://developers.tap.company/docs/create-a-charge) or [Authorize](https://developers.tap.company/docs/create-an-authorize) endpoint

JSON

```rdmd-code lang-json theme-light
"source": {
    "id": "token.id"
  }

```

## Option 2: Create a Charge/Authorize with an encrypted card   [Skip link to Option 2: Create a Charge/Authorize with an encrypted card](https://developers.tap.company/docs/encrypted-card-flow-pci\#option-2-create-a-chargeauthorize-with-an-encrypted-card)

You can pass the `encrypted card` as a `source.card` within [charges](https://developers.tap.company/docs/create-a-charge) API or [Authorize](https://developers.tap.company/docs/create-an-authorize) API

JSON

```rdmd-code lang-json theme-light
"source": {
    "card": "ENCRYPTED_CARD_DATA"
  }

```

Note that if there are any card validation errors, they will be included in the response from the charges or authorize request.

# Payment Processing   [Skip link to Payment Processing](https://developers.tap.company/docs/encrypted-card-flow-pci\#payment-processing)

Once you create a charge or an authorize request, you will get the `transaction.url` for the customer to complete the 3DS process.

> ## 📘  For merchants who are using multiple merchant accounts linked under a master account, you can use the master encryption keys to encrypt the card, and process the payment under any linked merchant account, by passing the merchant ID in the charges/authorize endpoint

Here is a charge response sample (same for both options)

```rdmd-code lang- theme-light
{
    "id": "chg_TS01A5220241042q1ZX1006293",
    "object": "charge",
    "live_mode": false,
    "customer_initiated": true,
    "api_version": "V2",
    "method": "CREATE",
    "status": "INITIATED",
    "amount": 1.00,
    "currency": "SAR",
    "threeDSecure": true,
    "card_threeDSecure": false,
    "save_card": false,
    "product": "GOSELL",
    "metadata": {
        "udf1": "test_data_1",
        "udf2": "test_data_2",
        "udf3": "test_data_3"
    },
    "transaction": {
        "timezone": "UTC+03:00",
        "created": "1718016173107",
        "url": "https://sandbox.payments.tap.company/test_gosell/v2/payment/tap_process.aspx?chg=d6aPjTalvIX0FifFT%2bJQ%2fxZp7Ju0qg3hE%2fcQCz4oL14%3d",
        "expiry": {
            "period": 30,
            "type": "MINUTE"
        },
        "asynchronous": false,
        "amount": 1.00,
        "currency": "SAR"
    },
    "reference": {
        "transaction": "txn_0001",
        "order": "ord_0001",
        "idempotent": "ord_0001"
    },
    "response": {
        "code": "100",
        "message": "Initiated"
    },
    "card": {
        "object": "card",
        "first_six": "512345",
        "first_eight": "51234500",
        "last_four": "0008",
        "name": "test user",
        "expiry": {
            "month": "01",
            "year": "39"
        }
    },
    "receipt": {
        "email": true,
        "sms": true
    },
    "customer": {
        "id": "cus_TS07A5420232136o2K52709053",
        "first_name": "Majdi",
        "middle_name": "Abdullah",
        "last_name": "Al Khowaiter",
        "email": "m.ghgjhgj@tap.company",
        "phone": {
            "country_code": "966",
            "number": "51234567"
        }
    },
    "merchant": {
        "country": "SA",
        "currency": "SAR",
        "id": "12345"
    },
    "source": {
        "object": "token",
        "id": "tok_mOsV3247433Xp410F85Z303",
        "on_file": false
    },
    "redirect": {
        "status": "PENDING",
        "url": "http://your_website.com/redirecturl"
    },
    "post": {
        "status": "PENDING"
    },
    "activities": [\
        {\
            "id": "activity_TS07A5720241042Hw951006068",\
            "object": "activity",\
            "created": 1718016173107,\
            "status": "INITIATED",\
            "currency": "SAR",\
            "amount": 1.00,\
            "remarks": "charge - created",\
            "txn_id": "chg_TS01A5220241042q1ZX1006293"\
        }\
    ],
    "auto_reversed": false
}

```

Updated20 days ago

* * *

- [Webhook](https://developers.tap.company/docs/webhook)
- [Redirect](https://developers.tap.company/docs/redirect)