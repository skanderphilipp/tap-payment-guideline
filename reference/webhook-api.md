This documentation outlines the integration process for receiving and handling payout information through our Webhook and Payout Download API. The process is designed to provide detailed payout information, including transaction-level data, to our users whether merchants or platforms.

# Flow Overview   [Skip link to Flow Overview](https://developers.tap.company/reference/webhook-api\#flow-overview)

**Payout Webhook:** Initiated for each payout, this webhook sends a summary of payout-related information.

**Payout Download API:** After receiving a payout ID from the webhook, this API is used to download detailed payout files, including transaction-level data.

# Payout Webhook Specification   [Skip link to Payout Webhook Specification](https://developers.tap.company/reference/webhook-api\#payout-webhook-specification)

## Payout Webhook structure   [Skip link to Payout Webhook structure](https://developers.tap.company/reference/webhook-api\#payout-webhook-structure)

**The webhook response includes the following objects:**

- **_payoutId_** :Unique identifier for the payout.
- _**payoutStatus**_ : Shows status of the payout (PENDING, INITIATED, FAILED, PAID\_OUT).
- **_payoutDate_** :Date when the payout was processed.
- **_payoutAmount_**: Total amount of the payout.
- **_payoutCurrency_**: Currency of the payout amount.
- _**merchantId**_: Unique identifier for the merchant.
- **_wallet_** : Which will include walletId, legacy\_id, walletCountry, wallet Bank (bankId, bankCountry, bankName, swift and beneficiary information (beneficiaryName and beneficiaryIBAN).

### Response Example   [Skip link to Response Example](https://developers.tap.company/reference/webhook-api\#response-example)

Payout Response

```rdmd-code lang-curl theme-light
{
  "id": "payout_33271023375023",
  "status": "PAID_OUT",
  "date": 1698589980000,
  "amount": 8.16,
  "currency": "SAR",
  "merchant_id": "26374580",
  "wallet": {
    "id": "26374580",
    "legacy_id": "26374580",
    "country": "SA",
    "bank": {
      "id": "55",
      "country": "SA",
      "name": "RAJHI",
      "swift": "RJHISARI",
      "beneficiary": {
        "name": "Nowaf Naif D Almarkhan",
        "iban": "XXXXX8715"
      }
    }
  }
}

```

## Webhook Endpoint   [Skip link to Webhook Endpoint](https://developers.tap.company/reference/webhook-api\#webhook-endpoint)

User needs to provide an endpoint to receive webhook notifications. This endpoint should be capable of handling HTTPS POST responses with a JSON payload.

Also there is an alternative approach to filtering the payout report according to specific dates. Instead of manually sorting through the report, you can utilize our "List All Payouts" endpoint, which provides the functionality to filter the report based on specific dates. By utilizing this endpoint, you will be able to streamline the process and efficiently extract the desired data without the need for manual filtering.

## List all payout endpoint   [Skip link to List all payout endpoint](https://developers.tap.company/reference/webhook-api\#list-all-payout-endpoint)

### Request Example   [Skip link to Request Example](https://developers.tap.company/reference/webhook-api\#request-example)

```rdmd-code lang- theme-light
curl --request POST \
  --url https://api.tap.company/v2/payouts/list \
  --header 'authorization: Bearer sk_test_UCSe**********zyh8' \
  --header 'content-type: application/json' \
  --data '{
	"period": {
		"date": {
			"from": 1701523751000,
			"to": 1704202151000
		}
	}
}'

```

### Response Example   [Skip link to Response Example](https://developers.tap.company/reference/webhook-api\#response-example-1)

cURL

```rdmd-code lang-curl theme-light
{
	"object": "list",
	"live_mode": false,
	"api_version": "V2",
	"count": 7,
	"has_more": false,
	"payouts": [\
		{\
			"id": "payout_1234567234567876",\
			"status": "PAID_OUT",\
			"date": 1690848301000,\
			"amount": 7351.874,\
			"currency": "KWD",\
			"merchant_id": "20860903",\
			"wallet": {\
				"id": "wallet_34567876",\
				"legacy_id": "34567876",\
				"country": "KW",\
				"bank": {\
					"id": "10",\
					"country": "KW",\
					"name": "KFH",\
					"swift": "KFHOKWKW",\
					"beneficiary": {\
						"name": "TEST",\
						"iban": "XXXXX6275"\
					}\
				}\
			},\
			"settlements_available": true\
		},\
		{\
			"id": "payout_1234567234567877",\
			"status": "PAID_OUT",\
			"date": 1691107501000,\
			"amount": 10233.934,\
			"currency": "KWD",\
			"merchant_id": "20860903",\
			"wallet": {\
				"id": "wallet_34567877",\
				"legacy_id": "34567877",\
				"country": "KW",\
				"bank": {\
					"id": "10",\
					"country": "KW",\
					"name": "KFH",\
					"swift": "KFHOKWKW",\
					"beneficiary": {\
						"name": "TEST",\
						"iban": "XXXXX6275"\
					}\
				}\
			},\
			"settlements_available": true\
		},\
		{\
			"id": "payout_1234567234567879",\
			"status": "PAID_OUT",\
			"date": 1691193901000,\
			"amount": 7197.136,\
			"currency": "KWD",\
			"merchant_id": "20860903",\
			"wallet": {\
				"id": "wallet_34567879",\
				"legacy_id": "34567879",\
				"country": "KW",\
				"bank": {\
					"id": "10",\
					"country": "KW",\
					"name": "KFH",\
					"swift": "KFHOKWKW",\
					"beneficiary": {\
						"name": "TEST",\
						"iban": "XXXXX6275"\
					}\
				}\
			},\
			"settlements_available": true\
		},\
		{\
			"id": "payout_1234567234567878",\
			"status": "PAID_OUT",\
			"date": 1691625901000,\
			"amount": 7300.088,\
			"currency": "KWD",\
			"merchant_id": "20860903",\
			"wallet": {\
				"id": "wallet_34567878",\
				"legacy_id": "34567878",\
				"country": "KW",\
				"bank": {\
					"id": "10",\
					"country": "KW",\
					"name": "KFH",\
					"swift": "KFHOKWKW",\
					"beneficiary": {\
						"name": "TEST",\
						"iban": "XXXXX6275"\
					}\
				}\
			},\
			"settlements_available": false,\
			"settlements_description": ""\
		},\
		{\
			"id": "payout_1234567234567871",\
			"status": "PAID_OUT",\
			"date": 1691798701000,\
			"amount": 15767.762,\
			"currency": "KWD",\
			"merchant_id": "20860903",\
			"wallet": {\
				"id": "wallet_34567871",\
				"legacy_id": "34567871",\
				"country": "KW",\
				"bank": {\
					"id": "10",\
					"country": "KW",\
					"name": "KFH",\
					"swift": "KFHOKWKW",\
					"beneficiary": {\
						"name": "TEST",\
						"iban": "XXXXX6275"\
					}\
				}\
			},\
			"settlements_available": true\
		},\
		{\
			"id": "payout_1234567234567872",\
			"status": "PAID_OUT",\
			"date": 1691885101000,\
			"amount": 7917.486,\
			"currency": "KWD",\
			"merchant_id": "20860903",\
			"wallet": {\
				"id": "wallet_34567872",\
				"legacy_id": "34567872",\
				"country": "KW",\
				"bank": {\
					"id": "10",\
					"country": "KW",\
					"name": "KFH",\
					"swift": "KFHOKWKW",\
					"beneficiary": {\
						"name": "TEST",\
						"iban": "XXXXX6275"\
					}\
				}\
			},\
			"settlements_available": true\
		},\
		{\
			"id": "payout_1234567234567873",\
			"status": "PAID_OUT",\
			"date": 1692057901000,\
			"amount": 11190.685,\
			"currency": "KWD",\
			"merchant_id": "20860903",\
			"wallet": {\
				"id": "wallet_34567873",\
				"legacy_id": "34567873",\
				"country": "KW",\
				"bank": {\
					"id": "10",\
					"country": "KW",\
					"name": "KFH",\
					"swift": "KFHOKWKW",\
					"beneficiary": {\
						"name": "TEST",\
						"iban": "XXXXX6275"\
					}\
				}\
			},\
			"settlements_available": true\
		}\
	]
}

```

## Security   [Skip link to Security](https://developers.tap.company/reference/webhook-api\#security)

Webhook responses will include a signature header for verification. Please ensure your endpoint validates this signature before processing the endpoint.

# Payout Download API   [Skip link to Payout Download API](https://developers.tap.company/reference/webhook-api\#payout-download-api)

The below describes the Payout Download API request and response. Again, note that in the request, you will be passing the Payout ID that you will get from the Payout Webhook:

## Request   [Skip link to Request](https://developers.tap.company/reference/webhook-api\#request)

cURL

```rdmd-code lang-curl theme-light
curl --location 'https://api.tap.company/v2/payouts/download' \
--header 'Authorization: Bearer sk_live_jKA******************8Mn' \
--header 'Content-Type: application/json' \
--data '{
  "payouts": {
    "payout_id": [\
      "payout_33235465657023"\
    ]
  }
}'

```

### [Skip link to undefined](https://developers.tap.company/reference/webhook-api\#section-)

**The payout request includes the following object:**

**payoutId:** The unique identifier for the payout (obtained from the webhook).

## Response   [Skip link to Response](https://developers.tap.company/reference/webhook-api\#response)

After executing the provided cURL command, you will receive a response in a file format. It is important that you save this file as it will be in the format of a zip file. Inside the zip file, you will find the payout information and sheets.

text

```rdmd-code lang-curl theme-light
PKRe�W���9�&29102023  - CHARGES 332387573923.csv��Kn�0��z�`�p�Oeg$�������L�BmI����պ�z��$���n��_���?Q~����jӬ�CRZ�M(�._����|j�����	�~��)|��}[4M"�m��̷�7U[&�mZU���SQ���x#_}��fs�4T'&�;���N��_�1,B��p0qT|��-";9J��l|�98Q�8�E�W�b�J��\.��ۛ��N0���]���M��e���z����m������i�.ߎ�"(þ}�b�PJ�(HJ�y=������"�V�]���wBO�4m���5�fT.���o_]���w�c��q]�������h$�A����(λ�g(.�=�{����:�١L��ب�H�7��W:�N!(#)�,fY�5t���P�eYP��P!-�aD�@�2�*���p�/��f�˃#"N5�N<2�^C�[��λ`Wρ�Ș9w2^�~�5��xb���t�Q��r�Ө��I�V�G�Q��y%G�ߐ���Ռ�x6d����}�������3�(�cȼ>���\
��9�P]�U
Bά�IX�2c����SO�_PKRe�W��;,�/-29101023  - PAYOUT SUMMARY 3327134823.csvUOI�@��������<�w�B�$Ì�i��̓O���/���^��{�������E�)���0�� MbQ�b��P)b�,�Y�L|�YK��a��L$����"������4��0�5���L�|4��0��4)lQ;��b��
:h��g�Cʃ75a�{{"7����V��e��5�"&ǉ��PKRe�W���9�&29102023  - CHARGES 33271023375023.csvPKRe�W��;,�/-}29102023  - PAYOUT SUMMARY 33271023375023.csvPK��

```

## Sample Folder after Calling the Payout Download API   [Skip link to Sample Folder after Calling the Payout Download API](https://developers.tap.company/reference/webhook-api\#sample-folder-after-calling-the-payout-download-api)

You can find a sample of the payout folder that will be downloaded after calling the above API by clicking on this [link](https://drive.google.com/drive/folders/1D5YTG5ZucN8urWquzbh7rtEt3IeoLWgi).

# File Structure   [Skip link to File Structure](https://developers.tap.company/reference/webhook-api\#file-structure)

Each payout file would have the two standard sheets below:

**_Summary Sheet:_** This contains a summarized information of the payout.

**_Charges Sheet:_** List of charges associated with the payout.

Aside from the two standard sheets above, there could be additional sheets for potential transaction types (refunds, disputes, dispute\_release) affecting the payout amount:

**_Refund Sheet:_** List of refunds associated with the payout. Note that refunds reduce the payment amount.

**_Dispute Sheet:_** List of transactions that are disputed by cardholders. Note that disputes reduce the payment amount.

_**Dispute\_Release Sheet:**_ List of transactions that were disputed earlier and resolved in favor of the merchant. Note that disputes releases increase the payment amount.

- Disputed transactions, if any, are received by us from issuer banks, where upon receipt, we would place the transaction, or equivalent amount, on hold. Hence, an incoming dispute reduces the payout amount.
- The subsequent actions can be in days or months after the receipt of the disputes, depending on the case, and are either releasing the transection or chargeback the transaction, depending on the dispute resolution.
- If the resolution was to release the transaction, then this will be listed in Dispute\_Release sheet (of a future payout).
- If the resolution was to chargeback the transaction, there won't be any further impact to the payout amount (of any future payout) as the transaction was placed on hold earlier.
- Dispute resolution is carried out based on the scheme dispute guidelines.

### Additional Information   [Skip link to Additional Information](https://developers.tap.company/reference/webhook-api\#additional-information)

- The webhook and payout file is at a payout level irrespective of how many payouts the user has in a given day.
- In case of a combined payout for multiple wallets/terminals, the process remains the same, where the webhook and payout files will be at a payout level.

**Security and Authentication**

Authentication details for accessing the Payout Download API will be provided separately. Please ensure secure handling of all credentials and access tokens.

# Integration Steps   [Skip link to Integration Steps](https://developers.tap.company/reference/webhook-api\#integration-steps)

1. Set up a secure endpoint to receive webhook notifications.
2. Validate the webhook signature.
3. Use the payoutId from the webhook to call the Payout Download API.
4. Process and store the data from the downloaded payout files as per your system requirements.