# Introduction   [Skip link to Introduction](https://developers.tap.company/docs/benefitpay-web-sdk\#introduction)

This guide provides instructions for integrating the Benefit Pay button into your website, with scripts available for both Vanilla JavaScript and React JS, accommodating your preferred programming language.

Once the scripts are added, the Benefit Pay button will appear in your web application. When clicked, users will receive a QR code that directs them to the Benefit Pay app for secure and efficient payment completion.

# Prerequisites   [Skip link to Prerequisites](https://developers.tap.company/docs/benefitpay-web-sdk\#prerequisites)

In order for Benefit Pay Web SDK to function, the domain name needs to be registered with Tap. Reach out to tap support team and provide your domain name(s) where you wish to put the Benefit Pay button. Once tap registers the domain, your public key respective to the domain will be generated and made available on the tap business dashboard. You will have to provide the respective Public Key, Hash String and merchant ID in order to initiate the Benefit Pay Web SDK.

# Benefit Pay Web SDK Integration   [Skip link to Benefit Pay Web SDK Integration](https://developers.tap.company/docs/benefitpay-web-sdk\#benefit-pay-web-sdk-integration)

We have provided the Benefit Pay Web SDK codes, in both React.js and Vanilla JS providing merchants with more options depending on the programming language that they are using.

## Benefit Pay Integration using React JS   [Skip link to Benefit Pay Integration using React JS](https://developers.tap.company/docs/benefitpay-web-sdk\#benefit-pay-integration-using-react-js)

The React module for the Benefit Pay web SDK is available through the NPM registry. You can install it using either of the following commands:

**Install the library via NPM:**

```rdmd-code lang- theme-light
npm install @tap-payments/benefit-pay-button

```

**Or using Yarn:**

```rdmd-code lang- theme-light
yarn add @tap-payments/benefit-pay-button

```

### Example of the React JS Integration Code (ES6)   [Skip link to Example of the React JS Integration Code (ES6)](https://developers.tap.company/docs/benefitpay-web-sdk\#example-of-the-react-js-integration-code-es6)

The following code demonstrates how to integrate the Benefit Pay button in a React.js project. Be sure to pass the public key and merchant ID provided by Tap.

React JS

```rdmd-code lang-javascript theme-light
import React from 'react'
import { BenefitPayButton, Edges, Locale } from '@tap-payments/benefit-pay-button'

const App = () => {
	return (
		<BenefitPayButton
			// required (The public Key provided by Tap)
			operator={{
				publicKey: 'pk_test_xxxx',
    		hashString: myHashString
			}}
			// optional (to enable the debug mode)
			debug={true}
			// required
			merchant={{
				// required (The merchant identifier provided by Tap)
				id: 'merchant_xxxx'
			}}
			// required
			transaction={{
				// required (The amount to be charged)
				amount: '12',
				// required (The currency of the amount)
				currency: 'BHD'
			}}
			reference={{
				transaction: 'txn_123',
				order: 'ord_123'
			}}
			// optional (The billing contact information)
			customer={{
				//"OPTIONAL : Customer ID",
				names: [\
					{\
						// required : en or ar",\
						lang: Locale.EN,\
						// required : First name of the customer.",\
						first: 'test',\
						// required : Last name of the customer.",\
						last: 'tester',\
						// optional : Middle name of the customer.",\
						middle: 'test'\
					}\
				],
				// optional: Defines the contact details for the customer
				contact: {
					// optional: The customer's email",
					email: 'test@gmail.com',
					// optional: The customer's phone number"
					phone: {
						// required:  The customer's country code",
						countryCode: '+20',
						// required:  The customer's phone number
						number: '1000000000'
					}
				}
			}}
			//optional (for styling button)
			interface={{
				// optional (The locale of the Benefit Pay button and it can be one of these locales:[EN,AR])
				locale: Locale.EN,
				// optional (The border of the button and it can be one of these values:[curved,straight])
				edges: Edges.CURVED
			}}
			post={{
				url: ''
			}}
			// optional (A callback function that will be called when you button is clickable)
			onReady={() => {
				console.log('Ready')
			}}
			// optional (A callback function that will be called when the button clicked)
			onClick={() => {
				console.log('Clicked')
			}}
			// optional (A callback function that will be called when you cancel the payment)
			onCancel={() => console.log('cancelled')}
			// optional (A callback function that will be called when you have an error)
			onError={(err) => console.log('onError', err)}
			// optional (A async function that will be called after creating the token successfully)
			onSuccess={(data) => {
				// do your stuff here...
				console.log(data)
			}}
		/>
	)
}

```

## Benefit Pay Integration using Vanilla JS   [Skip link to Benefit Pay Integration using Vanilla JS](https://developers.tap.company/docs/benefitpay-web-sdk\#benefit-pay-integration-using-vanilla-js)

Vanilla JS

```rdmd-code lang-javascript theme-light
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta http-equiv="X-UA-Compatible" content="IE=edge" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Benefit pay button</title>
		<script src="https://tap-sdks.b-cdn.net/benefit-pay/build-1.0.20/main.js"></script>
	</head>

	<body>
		<div id="benefit-pay-button"></div>
		<script type="text/javascript">
			const { render, Edges, Locale, ThemeMode } = window.TapBenefitpaySDK
			render(
				{
					operator: {
						publicKey: 'pk_test_xxxx',
            hashString: myHashString
					},
					debug: true,
					merchant: {
						id: 'merchant_xxxx'
					},
					transaction: {
						amount: '12',
						currency: 'BHD'
					},
					reference: {
						transaction: 'txn_123',
						order: 'ord_123'
					},
					customer: {
						names: [\
							{\
								lang: Locale.EN,\
								first: 'test',\
								last: 'tester',\
								middle: 'test'\
							}\
						],
						contact: {
							email: 'test@gmail.com',
							phone: {
								countryCode: '20',
								number: '1234567'
							}
						}
					},
					interface: {
						locale: Locale.EN,
						edges: Edges.CURVED
					},
					post: {
						url: ''
					},
					onReady: () => {
						console.log('Ready')
					},
					onClick: () => {
						console.log('Clicked')
					},
					onCancel: () => console.log('cancelled'),
					onError: (err) => console.log('onError', err),
					onSuccess: (data) => {
						console.log(data)
					}
				},
				'benefit-pay-button'
			)
		</script>
	</body>
</html>

```

# Hash String Calculation   [Skip link to Hash String Calculation](https://developers.tap.company/docs/benefitpay-web-sdk\#hash-string-calculation)

In the Benefit Pay integration, the hash string is a crucial security measure used to verify the integrity and authenticity of the request. The hash string is generated by concatenating specific transaction details and then applying the HMAC SHA256 hashing algorithm to the resulting string. The hash is signed using the merchant's secret key, which should be kept confidential and never shared with anyone.

This ensures that the request sent to the payment gateway has not been tampered with, and only valid transactions from authorized sources are processed.

## How Hashing Works:   [Skip link to How Hashing Works:](https://developers.tap.company/docs/benefitpay-web-sdk\#how-hashing-works)

- **String Preparation:** First, you need to concatenate the relevant transaction data (like public key, amount, currency, etc.) into a single string, in a specific order. This string will be used to generate the hash.
- **Hashing Algorithm:** Once the string is prepared, it should be hashed using the HMAC SHA256 algorithm. The merchant's secret key will be used as the key for the hashing process.
- **Resulting Hash String:** The output of this operation will be a unique hash string, which is sent along with the request to the payment gateway. The gateway will verify this hash to ensure that the request is legitimate.

## Required Fields for Hash Generation:   [Skip link to Required Fields for Hash Generation:](https://developers.tap.company/docs/benefitpay-web-sdk\#required-fields-for-hash-generation)

- **Public Key:** The public key provided by Tap, used to identify the merchant in the payment request.
- **Secret Key:** A confidential key provided by Tap. It is used to sign the request and must be stored securely.
- **Amount:** The amount to be processed. This value must be formatted to 3 decimal places (e.g., 3 BHD = 3.000).
- **Currency:** The currency of the transaction, represented by a 3-letter ISO code (e.g., BHD for Bahraini Dinar).
- **Post URL:** The URL to which the payment gateway will send the response (commonly used for webhooks to update transaction status).
- **Transaction Reference:** A unique identifier for the transaction. This helps in tracking and identifying individual payments.

> ## 🚧  Make sure the amount is set in a 3 decimal format (e.g., 3 BHD should be 3.000 in the hash string) and the secret key never logged or exposed in client-side code

## Hash String Code Sample   [Skip link to Hash String Code Sample](https://developers.tap.company/docs/benefitpay-web-sdk\#hash-string-code-sample)

Hash

```rdmd-code lang-javascript theme-light
// Input fields for Hash Calculation
publicApiKey = 'pk_test_xxxx';  //Your Public API Key Provided by Tap
amount = 'charge.amount'; 		//charge amount formatted to 3 decimal places
currency = 'charge.currency'; //charge currency (BHD)
transactionReference = 'reference.transaction' //reference transaction
postUrl = 'charge.postUrl' //the Post URL that receives the webhook
secretAPIKey = "sk_test_xxxx"; //Your secret API Key provided by Tap

// Concatenate the fields to form the string that will be hashed
toBeHashed = `x_publickey${publicApiKey}x_amount${amount}x_currency${currency}x_transaction${transactionReference}x_post${postUrl}`;

// Log the string to be hashed for verification
console.log("String to be hashed: ", toBeHashed);

// Create the hash string using HMAC SHA256 and your secret API key
myHashString = hash_hmac('sha256', toBeHashed, secretAPIKey);

// Output the resulting hash string (this is what you need to send)
console.log("Generated Hash String: ", myHashString);

```

# Event Handling   [Skip link to Event Handling](https://developers.tap.company/docs/benefitpay-web-sdk\#event-handling)

Use event handling to manage actions related to the Benefit Pay button. These callback functions handle button clicks, cancellations, errors, and successful payments.

JS

```rdmd-code lang-javascript theme-light
onCancel: async () => {
  console.log('onCancel');
},
onError: async (error) => {
  console.log('onError', error);
},
onSuccess: async (data) => {
  console.log('onSuccess', data);
},
onReady: async () => {
  console.log('onReady');
}

```

# Parameters   [Skip link to Parameters](https://developers.tap.company/docs/benefitpay-web-sdk\#parameters)

| Name | Type | R/O | Description |
| --- | --- | --- | --- |
| **operator** | object | Required | The operator object that contains the public key + hashString |
| **operator.publicKey** | string | Required | The public key provided by Tap |
| **operator.hashString** | string | Required | The hash string to secure your transaction |
| **debug** | bool | Optional | To enable the debug mode |
| **merchant** | object | Required | The merchant object that contains the merchant identifier |
| **merchant.id** | string | Required | The merchant identifier provided by Tap |
| **transaction** | object | Required | The transaction object that contains the amount and currency |
| **transaction.amount** | string | Required | The amount to be charged |
| **transaction.currency** | string | Required | The currency of the amount |
| **reference** | object | Optional | The reference object that contains the transaction and order references |
| **reference.transaction** | string | Required | passed by the merchant for further processing whenever needed. |
| **reference.order** | string | Optional | passed by the merchant for further processing whenever needed. |
| **customer** | object | Required | The customer object that contains the customer details |
| **customer.id** | object | Optional | The customer ID |
| **customer.names** | array | Required | The customer names and it can be one of these values: \[EN, AR\] |
| **customer.names\[idx\].lang** | string | Required | The customer name language and it can be one of these values: \[EN, AR\] |
| **customer.names\[idx\].first** | string | Required | The customer first name |
| **customer.names\[idx\].last** | string | Required | The customer last name |
| **customer.names\[idx\].middle** | string | Optional | The customer middle name |
| **customer.contact** | object | Optional | The customer contact object that contains the email and phone number |
| **customer.contact.email** | string | Required | The customer email |
| **customer.contact.phone** | object | Required | The customer phone object that contains the country code and number |
| **customer.contact.phone.countryCode** | string | Required | The customer country code |
| **customer.contact.phone.number** | string | Required | The customer phone number |
| **interface** | object | Optional | The interface object that contains the locale and edges |
| **interface.locale** | string | Optional | The locale of the Benefit Pay button and it can be one of these locales: \[EN, AR\] |
| **interface.edges** | string | Optional | The border of the button and it can be one of these values: \[CURVED, STRAIGHT\] |
| **post** | object | Required | This is the webhook for your server, needed to update you server. |
| **post.url** | string | Required | This is the webhook URL for your server, needed to update you server. |
| **onReady** | func | Optional | A callback function that will be called when the button become ready |
| **onClick** | func | Optional | A callback function that will be called when the button clicked |
| **onCancel** | func | Optional | A callback function that will be called when you cancel the payment |
| **onError** | func | Optional | A callback function that will be called when you have an error |
| **onSuccess** | func | Optional | A callback function that will be called after finishing the payment successfully |

Should you encounter any difficulties or have specific questions, reach out to the Tap Payments support team for prompt assistance. Happy integrating!

Updated4 months ago

* * *