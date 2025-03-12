To process a charge as a merchant-initiated transaction, you must set the "customer\_initiated" boolean to false and the "3DSecure" to false, and also provide a Payment Agreement ID. Without this ID, an error will occur due to the missing "agreement\_id." This ID is essential for non-3D Secure transactions as it links the charge to the payment agreement associated with the customer's saved card.

JSON

```rdmd-code lang-json theme-light
{
	"errors": [\
		{\
			"code": "1216",\
			"description": "Agreement id is missing"\
		}\
	],
	"http_code": "400"
}

```

## Creating a Non-3D Secure Charge with a Payment Agreement   [Skip link to Creating a Non-3D Secure Charge with a Payment Agreement](https://developers.tap.company/docs/merchant-initiated-transaction\#creating-a-non-3d-secure-charge-with-a-payment-agreement)

**Obtain the valid payment agreement ID:** Ensure you have the correct payment agreement ID associated with the saved card. This can be done by creating the agreement in advance and noting its ID, or by having it generated automatically during the agreement creation process. The ID must correspond to the associated contract—be it a saved card ID, subscription ID, invoice ID, or order ID.

**Verify the customer ID:** Confirm that you possess a valid customer ID that matches the customer linked to the saved card. This step is vital to ensure the charge is accurately associated with the correct customer account.

**Generate a valid token ID:** Use the saved card ID and customer ID to generate a token ID. This token acts as a secure identifier for the saved card during the charging process.

**Specify the initiator of the transaction:** Determine who is initiating the transaction. Set the "customer\_initiated" boolean to true for customer-led transactions, which typically involve 3D Secure authentication. For merchant-initiated transactions, set this boolean to false.

By following these steps and correctly providing all necessary parameters—including the payment agreement ID, customer ID, and token ID—and setting the "customer\_initiated" boolean appropriately while disabling "3D Secure," you can successfully create a charge. This process enables you to invoice the customer as per the agreement's terms without the need for 3D Secure authentication.

> ## 📘  For enabling non-3D Secure transactions in a live environment, please contact your Tap account manager to activate the necessary settings on your merchant account.

## How to Create a Charge Using a Payment Agreement: Understanding Request Parameters and Process   [Skip link to How to Create a Charge Using a Payment Agreement: Understanding Request Parameters and Process](https://developers.tap.company/docs/merchant-initiated-transaction\#how-to-create-a-charge-using-a-payment-agreement-understanding-request-parameters-and-process)

To initiate a charge under a payment agreement, certain parameters matching the agreed-upon merchant and customer terms must be included in your charge request. When these parameters are correctly configured, you can process a charge without requiring 3D Secure authentication, as it will be based on the payment agreement's prior authorization.

For illustrative purposes, a sample charge request is provided below in URL format. Use this as a model, inserting your unique details and settings, to properly formulate your charge request. Essential parameters linking the charge to the payment agreement will be outlined.

cURL

```rdmd-code lang-curl theme-light
curl --request POST \
  --url https://api.tap.company/v2/charges \
  --header 'authorization: Bearer sk_test_wXOnrWkK2d9BbFCHj3gf6V1v' \
  --header 'content-type: application/json' \
  --header 'lang_code: EN' \
  --data '{
	"amount": 1,
	"currency": "SAR",
	"payment_agreement": {
		"id": "payment_agreement_TS05A1920230911b2K12105431",
	},
	"customer_initiated": "false",
	"threeDSecure": true,
	"save_card": false,
	"description": "Test Description",
	"statement_descriptor": "Sample",
	"metadata": {
		"udf1": "test 1",
		"udf2": "test 2"
	},
	"reference": {
		"transaction": "txnss_0001",
		"order": "ord_0001&&&"
	},
	"receipt": {
		"email": false,
		"sms": true
	},
	"customer": {
		"id": "cus_TS01A0520231538Ps321805785"
	},
	"merchant": {
		"id": ""
	},
	"source": {
		"id": "tok_ex6t5523232urdf21fu44961"
	},
	"post": {
		"url": "https://posturl"
	},
	"redirect": {
		"url": "https://bfc-test.com"
	}
}'

```

In the provided charge request, the relevant parameters related to the payment agreement are as follows:

| Parameter | Description | Example |
| --- | --- | --- |
| threeDSecure | This parameter is set to false, indicating that the transaction should be processed without 3D Secure authentication. It aligns with the agreement terms, allowing the merchant to charge the customer without the additional security step. |  |
| save\_card | This parameter is set to false, indicating that the customer's card details will not be saved for future use. This aligns with the concept of the payment agreement, which prioritizes the transaction itself rather than storing the card information for recurring charges. |  |
| customer | Within the "customer" object, the "id" field specifies the customer ID. Ensures that the charge is associated with the correct customer. |  |
| source | The "source" object contains the "id" field, which represents the token ID of the saved card. This token ID is created using the saved card ID and the customer ID, serving as a secure identifier throughout the charging process. |  |
| customer\_initiated | This parameter is set to "false," indicating that the merchant is initiating the transaction on behalf of the customer. This aligns with the discussion on differentiating between customer-initiated and merchant-initiated transactions. |  |
| payment\_agreement | Within the "payment\_agreement" object, the "id" field specifies the payment agreement ID. It links the charge to the specific agreement established between the merchant and the customer. The agreement ID allows the merchant to charge the customer based on the terms agreed upon. |  |

Including the specified parameters in the charge request ensures the transaction adheres to the payment agreement. Consequently, the merchant can charge the customer without the need for 3D Secure authentication, in line with the agreed-upon terms and conditions.

## Charge Response with Payment Agreement Created   [Skip link to Charge Response with Payment Agreement Created](https://developers.tap.company/docs/merchant-initiated-transaction\#charge-response-with-payment-agreement-created)

JSON

```rdmd-code lang-json theme-light
{
	"id": "chg_TS03A4020230203x2XZ2205881",
	"object": "charge",
	"live_mode": false,
	"customer_initiated": false,
	"api_version": "V2",
	"method": "CREATE",
	"status": "CAPTURED",
	"amount": 1.00,
	"currency": "SAR",
	"threeDSecure": false,
	"card_threeDSecure": false,
	"save_card": false,
	"merchant_id": "",
	"product": "GOSELL",
	"statement_descriptor": "Sample",
	"description": "Test Description",
	"metadata": {
		"udf1": "test 1",
		"udf2": "test 2"
	},
	"transaction": {
		"authorization_id": "157811",
		"timezone": "UTC+03:00",
		"created": "1684721020944",
		"expiry": {
			"period": 30,
			"type": "MINUTE"
		},
		"asynchronous": false,
		"amount": 1.00,
		"currency": "SAR"
	},
	"reference": {
		"track": "tck_TS06A4220230203r0MP2205147",
		"payment": "4222230203051476421",
		"gateway": "123456789",
		"acquirer": "314123157811",
		"transaction": "txnss_0001",
		"order": "ord_0001&&&"
	},
	"response": {
		"code": "000",
		"message": "Captured"
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
		"first_six": "446404",
		"scheme": "MADA",
		"brand": "VISA",
		"last_four": "0007"
	},
	"receipt": {
		"id": "204222230203054620",
		"email": false,
		"sms": true
	},
	"customer": {
		"id": "cus_TS01A0520231538Ps321805785",
		"first_name": "test23",
		"middle_name": "test",
		"last_name": "test",
		"email": "tes2t1234@test.com",
		"phone": {
			"country_code": "965",
			"number": "00000000"
		}
	},
	"merchant": {
		"country": "SA",
		"currency": "SAR",
		"id": "1201232"
	},
	"source": {
		"object": "token",
		"type": "CARD_NOT_PRESENT",
		"payment_type": "DEBIT",
		"payment_method": "VISA",
		"channel": "INTERNET",
		"id": "tok_ex6t5523232urdf21fu44961"
	},
	"redirect": {
		"status": "PENDING",
		"url": "https://bfc-test.com"
	},
	"post": {
		"status": "PENDING",
		"url": "https://posturl"
	},
	"activities": [\
		{\
			"id": "activity_TS06A4220230203Rn032205241",\
			"object": "activity",\
			"created": 1684721020944,\
			"status": "INITIATED",\
			"currency": "SAR",\
			"amount": 1.00,\
			"remarks": "charge - created"\
		},\
		{\
			"id": "activity_TS06A4320230203j4LH2205408",\
			"object": "activity",\
			"created": 1684721023408,\
			"status": "CAPTURED",\
			"currency": "SAR",\
			"amount": 1.00,\
			"remarks": "charge - captured"\
		}\
	],
	"auto_reversed": false,
	"payment_agreement": {
		"id": "payment_agreement_TS05A1920230911b2K12105431",
		"total_payments_count": 3,
		"contract": {
			"id": "card_gv7U4235591d8l21OQ4u663",
			"type": "UNSCHEDULED"
		},
		"variable_amount": {
			"id": "variable_amount_TS05A1920230911Hr2i2105431"
		}
	}
}

```

The response from the charge request provides important information about the transaction and the associated payment agreement.

Here are the key details:

| Parameter | Description | Example |
| --- | --- | --- |
| id | The unique identifier for the charge transaction. |  |
| customer\_initiated | Indicates whether the transaction was customer-initiated (in this case, it is set to false).<br>status: Indicates the status of the charge, which in this case is set to "CAPTURED," indicating a successful transaction. |  |
| status | Indicates the status of the charge, which in this case is set to "CAPTURED," indicating a successful transaction. |  |
| amount and currency | The amount and currency of the transaction (1.00 SAR). |  |
| threeDSecure and card\_threeDSecure | Both are set to false, indicating that the 3D Secure authentication process was skipped for this charge. |  |
| save\_card | Indicates whether the card details were saved for future use (in this case, it is set to false). |  |
| customer | Provides details about the customer associated with the transaction, including their ID, name, email, and phone number. |  |
| source | Contains information about the payment source, such as the token type (CARD\_NOT\_PRESENT), payment type (CREDIT), payment method (VISA), and channel (INTERNET). |  |
| redirect and post | Contains the status and URLs for redirection and post-transaction processing, respectively. |  |
| payment\_agreement | Contains details about the payment agreement associated with the transaction, including the agreement ID, total payments count, and the contract type (UNSCHEDULED). |  |

Updatedover 1 year ago

* * *