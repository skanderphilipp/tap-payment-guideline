# Overview   [Skip link to Overview](https://developers.tap.company/reference/customers\#overview)

Tap Payments' Customer API enables merchants to efficiently manage customer information for transactions. By passing a customer ID through the API, merchants can reuse the same customer details for future transactions. In the absence of a customer ID, Tap will create a new one.

> ## 📘  It is recommended to save the customer ID after a successful transaction so that future card details can be saved to the same customer ID.

To create a new customer in Tap Payments, it is mandatory to provide at least one of the following fields: first name, email, or first name + mobile number. This implies that while submitting customer information to Tap Payments, at least one of these fields must be included. The required customer information includes first name, middle name, last name, email, phone number, description, metadata, and currency.

## Customer Request Example   [Skip link to Customer Request Example](https://developers.tap.company/reference/customers\#customer-request-example)

```rdmd-code lang- theme-light
{
	"first_name": "test23",
	"middle_name": "test",
	"last_name": "test",
	"email": "tes2t1234@test.com",
	"phone": {
		"country_code": "965",
		"number": "00000000"
	},
	"description": "test",
	"metadata": {
		"udf1": "test"
	},
	"currency": "KWD"
}

```

## Customer Response Example   [Skip link to Customer Response Example](https://developers.tap.company/reference/customers\#customer-response-example)

```rdmd-code lang- theme-light
{
	"object": "customer",
	"live_mode": true,
	"created": "1681736385471",
	"merchant_id": "",
	"description": "test",
	"metadata": {
		"udf1": "test"
	},
	"currency": "KWD",
	"id": "cus_LV01H4520231259n9Y91704471",
	"first_name": "test23",
	"middle_name": "test",
	"last_name": "test",
	"email": "tes2t1234@test.com",
	"phone": {
		"country_code": "965",
		"number": "00000000"
	}
}

```