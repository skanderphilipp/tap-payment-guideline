# Introduction to Samsung Pay   [Skip link to Introduction to Samsung Pay](https://developers.tap.company/docs/samsung-pay-token\#introduction-to-samsung-pay)

Samsung Pay is a mobile payment and digital wallet service by Samsung that lets users make payments using compatible phones and other Samsung-produced devices. Here is a step by step guide to integrate Samsung pay using Tap APIs.

# Streamlining Secure Payments with Samsung Pay Direct Integration   [Skip link to Streamlining Secure Payments with Samsung Pay Direct Integration](https://developers.tap.company/docs/samsung-pay-token\#streamlining-secure-payments-with-samsung-pay-direct-integration)

## Setup Samsung Pay Developer Account   [Skip link to Setup Samsung Pay Developer Account](https://developers.tap.company/docs/samsung-pay-token\#setup-samsung-pay-developer-account)

- Navigate to [Samsung Pay Developers](https://pay.samsung.com/developers)
- Click on Sign In on the upper right corner
- Login with your Samsung Account
- Click on **Dashboard**
- Fill out the business details; ensure the correct country is selected. KSA is


listed with the code name GCC.
- Samsung team will approve the account within 2 business days.

## Getting Samsung Pay CSR   [Skip link to Getting Samsung Pay CSR](https://developers.tap.company/docs/samsung-pay-token\#getting-samsung-pay-csr)

Please contact [integrations@tap.company](mailto:integrations@tap.company) to obtain the Samsung Pay CSR

## Web and InApp Online Payment   [Skip link to Web and InApp Online Payment](https://developers.tap.company/docs/samsung-pay-token\#web-and-inapp-online-payment)

The Samsung JS SDK verifies it is loaded on an approved domain name as configured by the merchant. Follow these steps to create the service:

- From Samsung Pay Developers portal, click on **Go and create** inside the

**Create new service** box
- Alternatively, hover on **My projects** then Click **Go and Create** within the **Create New Service** box

  - Select **Web Online Payment** or Select **InApp Online Payment** based on your need
  - Enter the service information
- **Service Name**: an identifier for the merchant
- **Service Location**: Ensure the correct country is selected (SA is listed under GCC in the country options).
- **Payment Gateway**: you have to selected **tappayments** as payment gateway
- **CSR**: The file shared with you from Tap's Integration team.

## Creating a Samsung Pay Token   [Skip link to Creating a Samsung Pay Token](https://developers.tap.company/docs/samsung-pay-token\#creating-a-samsung-pay-token)

To integrate Samsung Pay into your payment system, you'll need to create and handle Samsung Pay tokens. Below is a step-by-step guide to creating a Samsung Pay token.

### Initialize Samsung Pay   [Skip link to Initialize Samsung Pay](https://developers.tap.company/docs/samsung-pay-token\#initialize-samsung-pay)

Ensure that Samsung Pay is properly set up on the user's device.

### Generate Token Request   [Skip link to Generate Token Request](https://developers.tap.company/docs/samsung-pay-token\#generate-token-request)

Create a token request payload in the specified format.

JSON

```rdmd-code lang-json theme-light

{
    "type": "samsungpay",
    "token_data": {
        "data": "your_payload_from_samsung"
    }
}

```

### Send Token Request   [Skip link to Send Token Request](https://developers.tap.company/docs/samsung-pay-token\#send-token-request)

Send the token request to the Tap token [endpoint](https://developers.tap.company/docs/create-samsungpay-token).

### Receive and Store Token   [Skip link to Receive and Store Token](https://developers.tap.company/docs/samsung-pay-token\#receive-and-store-token)

Receive the token response and process the payment using [Charges](https://developers.tap.company/docs/create-a-charge) API.

## Sample Token Request Payload   [Skip link to Sample Token Request Payload](https://developers.tap.company/docs/samsung-pay-token\#sample-token-request-payload)

Below is an example of a Samsung Pay token Curl request:

Tap Token - Samsung Pay

```rdmd-code lang-curl theme-light

curl --request POST \
  --url https://api.tap.company/v2/tokens \
  --header 'authorization: Bearer sk_test_ltWcmEKnXQr4jaAD2UiPCfJ3' \
  --header 'content-type: application/json' \
  --data '{
	"type": "samsungpay",
	"token_data": {
		"data": "eyJhbGciOiJSUzI1NiIsImtpZCI6Im1ka29yYTd0cWVGb0hRNkluMXpabFQ5MTJBZ0I0bFExOStZRHNsVGUxNVU9IiwidHlwIjoiSk9TRSIsImN0eSI6IkpXRSJ9.ZXlKaGJHY2lPaUpTVTBFeFh6VWlMQ0pyYVdRaU9pSnRaR3R2Y21FM2RIRmxSbTlJVVRaSmJqRjZXbXhVT1RFeVFXZENOR3hSTVRrcldVUnpiRlJsTVRWVlBTSXNJblI1Y0NJNklrcFBVMFVpTENKamFHRnVibVZzVTJWamRYSnBkSGxEYjI1MFpYaDBJam9pVWxOQlgxQkxTU0lzSW1WdVl5STZJa0V4TWpoSFEwMGlmUS5GczRSaGZPZE0zQUtpUU9JcWwySDB0dWNTXzFyVWR2bVh5LWhDY3AxOU5SVWFKcE96S1ZROTVxQ1ZsREF6ektmZ1hQbHU0RWd5Y0t5cTd2bmNzN3BOempMU2Z4ajFpejhFb2JmcVFHQ2dPMjRoRG8zRDJyaE9kQTJTWVktVVRwWGRQR2s4OUQ3MFRQeTlZZzh1UnRyREFfMC0zVnRxYTlRZThmXzVGclA3UUpieTVKSUZyNm5jRXktT25EQlFRb3lQV3d6cnVNcUhXMlIzSjh0WHhCZkp1R2gydURFMkJrVVlfQzFjM3dwZzVIWkhXV01VajZjem5tM2RGWnhXSnhHR1VnTHFKOU5aV1NKcUtyeUtYQWpZMGFRdjVvbXFCaDNjZHZSTnBKaWU0NDF2dS1pODVISzRaSE5zajM1SjBzU1FjMW4zUmR6azJjaEt2UnJCLXkycFEub3VzcEJSalU5bDBOei00Wi5Lam04VC1ZYnp6NDJvX3Y5aXNlTk42eHRoX3BEYTRlTHItcWZaMFFVVkN5bHNleHVoUTJJSTBHbGg4VElIMTIyMXZpTFRNXzNlX3h4UnJVRTJKR3RLMjdPZlpTS2xheTRQdGZKRTIyd0hUTlV1ZDREbjN2T1ZmcFRNd1lxamVLU2IxS0xodzZtSVQ4WUVaaHlFa0dzY0RncFJzV1BGWE5IT1BZbnlDcVhTQ0s2cmpLNm9tdTduYmRUZzRhcGNmZjRiZk96c0lqTFpOdF9XbWh3S21MdG8xVXIxblB2bVFhUFpkVTAxYW9HRDNfNVN4MDU1Zy5mUVVCYWE5NW9HNi1CMDdIeUpwVkRB.Jp7cToKxDfkMeeIV5hddA3PDwtD35fp4cq56cwUhNsQQ9HI5O2ucYsz_BVf0q0efRYXMDK8jMSOWHxt75gX3rxdgAQSASPRfUZH7KQ9x-LUfhG-0MaoROMpQdW0df0gzrGL9J2bZQ1u8Sa06Aho_opat2bCalF9AzQS0ycCkzCBbqPIcrGS40ATlN6VCc48Bn1JTkoUbxo4x_JqDDI-OdqHJ7DTCQHMVLpQDpwbzR1lSz5qiz0i3jchdxGf3LfsnqKKGPMKD_q1qlRnBsoJ6ZF0sSMcvW8NbyMPiu-b5RZbz8S_kec35Pcf2rFjNxac3BsqFIVWwGC_e1Ib7YpDhEw"
	},
	"client_ip": "37.34.236.190"
}'

```

### Detailed Description   [Skip link to Detailed Description](https://developers.tap.company/docs/samsung-pay-token\#detailed-description)

**type**: Indicates the type of payment method. For Samsung Pay, use "samsungpay".

**token\_data**: Contains the token details.

**data**: The actual token data provided by Samsung Pay.

## API response   [Skip link to API response](https://developers.tap.company/docs/samsung-pay-token\#api-response)

The API response includes a `token_id` and additional card details such as funding type, brand, expiration date, and more.

JSON

```rdmd-code lang-json theme-light

{
	"id": "tok_SyvF30241193Isu28y210n229",
	"status": "ACTIVE",
	"created": 1732792170229,
	"object": "token",
	"live_mode": false,
	"type": "SAMSUNGPAY",
	"purpose": "CHARGE",
	"used": false,
	"card": {
		"id": "card_8Tfu3024119ide228kh10v235",
		"object": "card",
		"on_file": false,
		"funding": "DEBIT",
		"fingerprint": "KdAa4VA7oIQyWx6NtBTDtt8p0sYYMugESUmNkDANru4%3D",
		"brand": "MASTERCARD",
		"scheme": "MASTERCARD",
		"category": "Visa Proprietary",
		"exp_month": 9,
		"exp_year": 27,
		"last_four": "1213",
		"first_six": "518573",
		"first_eight": "51857316",
		"name": "/",
		"issuer": {
			"country": "SA",
			"id": "bin_6c271124728d451b98f4d687119dfafd"
		}
	},
	"payment": {
		"id": "card_8Tfu3024119ide228kh10v235",
		"on_file": false,
		"card_data": {
			"exp_month": 9,
			"exp_year": 27,
			"last_four": "1213",
			"first_six": "518573",
			"first_eight": "51857316"
		},
		"fingerprint": "KdAa4VA7oIQyWx6NtBTDtt8p0sYYMugESUmNkDANru4%3D",
		"scheme": "MASTERCARD",
		"category": "Visa Proprietary",
		"issuer": {
			"country": "SA",
			"id": "bin_6c271124728d451b98f4d687119dfafd"
		}
	},
	"merchant": {
		"id": "12345"
	},
	"client_ip": "37.34.236.190"
}

```

## Charge the Token   [Skip link to Charge the Token](https://developers.tap.company/docs/samsung-pay-token\#charge-the-token)

Sample to control the source object in the charge API: with `token_id`

JSON

```rdmd-code lang-json theme-light

{
	"amount": 1,
	"currency": "SAR",
	"reference": {
		"transaction": "merchant_reference",
		"order": "merchant_reference"
	},
	"customer": {
		"id": "tap_generated_customer_id"
	},
	"merchant": {
		"id": "your_merchant_id"
	},
	"source": {
		"id": "tok_CUBiv13xxxx2ZiYP5XXXXX"
	},
	"post": {
		"url": "https://yourwebsite.com/v1/payment/tappayment-webhook"
	},
	"redirect": {
		"url": "https://yourwebsite.com/v1/payment/confirmation_page"
	}
}

```

The API response will include the status `captured`, indicating that the payment was successfully processed.

Updated3 months ago

* * *

Did this page help you?

Yes

No