[Instructions](https://developers.tap.company/docs/apple-pay) to follow before starting to integrate Apple pay into your mobile or web channel

We provide a web SDK which can be used by merchants to integrate Apple Pay button into the merchant's website using React JS or Vanilla JS. The button can be placed anywhere on the page. On click of the button, Apple Pay payment starts.

# Prerequisites   [Skip link to Prerequisites](https://developers.tap.company/docs/apple-pay-web-sdk\#prerequisites)

In order for Apple Pay Web SDK to function, the domain name needs to be registered with Tap. Reach out to tap support team and provide your domain name(s) (including list of sub-domain(s)), where you wish to put the Apple Pay button. Once tap registers the domain, your public key respective to the domain will be generated and made available on the tap business dashboard. You will have to provide the respective pk\_key and merchant ID inorder to initiate the Apple Pay Web SDK.

The next step is to make sure that the domain verification file is hosted on every domain(s) submitted.

> ## 🚧  Host your domain-verification file at the following path for each domain (or sub-domain) before you’re registering the domain with Tap:
>
> https://\[DOMAIN\_NAME\]/.well-known/apple-developer-merchantid-domain-association
>
> The domain-verification file must be in place before you register with Tap
>
> Ensure that the file is accessible via browser at the correct location. Example: [https://abc.com/.well-known/apple-developer-merchantid-domain-association](https://abc.com/.well-known/apple-developer-merchantid-domain-association)

# Register Merchant Domain Name with Apple Pay   [Skip link to Register Merchant Domain Name with Apple Pay](https://developers.tap.company/docs/apple-pay-web-sdk\#register-merchant-domain-name-with-apple-pay)

Tap Payments will register the merchant's domain name with Apple Pay on behalf of the merchant. **The merchant needs to provide the domain name to Tap Payments support team for this registration.** This step ensures that payments are processed with the Tap Apple Pay certificate without the need for the merchant to have access to Apple Developer portal and hence eliminates the need to share CSR/CER files between the two parties.

The merchant receives from Tap Payments a domain association file that needs to be added in the below path, following the guidelines of [Apple](https://developer.apple.com/documentation/applepaywebmerchantregistrationapi/preparing_merchant_domains_for_verification).

Path

```rdmd-code lang-css theme-light
https://[DOMAIN_NAME]/.well-known/apple-developer-merchantid-domain-association

```

> ## 🚧  Ensure the following are done correctly
>
> 1. The domain name(s) provided for registration should matche the domain(s) where Tap Payments Apple Pay Button SDK(s) are implemented. Any mismatch may result in payment failures.
> 2. Ensure that the file is accessible at the correct location. You can visit your own domain path to make sure that the contents of the file are visible through the respective link. Example: [https://abc.com/.well-known/apple-developer-merchantid-domain-association](https://abc.com/.well-known/apple-developer-merchantid-domain-association)

# ApplePay Web SDK Integration   [Skip link to ApplePay Web SDK Integration](https://developers.tap.company/docs/apple-pay-web-sdk\#applepay-web-sdk-integration)

We have provided the ApplePay Web SDK codes, in both React JS and Vanilla JS providing merchants with more options depending on the programming language that they are using.

## ApplePay Web SDK using React JS   [Skip link to ApplePay Web SDK using React JS](https://developers.tap.company/docs/apple-pay-web-sdk\#applepay-web-sdk-using-react-js)

The react module for Apple Pay WEB SDK is available through the NPM registry. Installation is done using the npm install command:

### Install the Libraries   [Skip link to Install the Libraries](https://developers.tap.company/docs/apple-pay-web-sdk\#install-the-libraries)

This is a [React](https://react.dev/) module available through the [npm registry](https://www.npmjs.com/). Installation is done using the

[npm install](https://docs.npmjs.com/downloading-and-installing-packages-locally) command:

console

```rdmd-code lang-json theme-light
npm install @tap-payments/apple-pay-button@1.1.6

```

OR

console

```rdmd-code lang-json theme-light
yarn add @tap-payments/apple-pay-button@1.1.6

```

### Example of the React JS Integration Code (ES6)   [Skip link to Example of the React JS Integration Code (ES6)](https://developers.tap.company/docs/apple-pay-web-sdk\#example-of-the-react-js-integration-code-es6)

Below is the React JS example code that you can add in your project, noting that you need to pass the `publicKey` that is provided by Tap after you have shared the domain of your website.

Tap will also provide you with the `merchant.id` that needs to be passed in line 14 in the below code block, which represents your account ID at Tap. And make sure that the domain added is the exact one that you have given to Tap to whitelist.

Refer to the [Configurations](https://developers.tap.company/docs/apple-pay-web-sdk-v20#configurations) section for the definition of each field.

React JS

```rdmd-code lang-javascript theme-light
import React from 'react'
import { createRoot } from 'react-dom/client'
import { ApplePayButton, abortApplePaySession } from '@tap-payments/apple-pay-button'

const App = () => {
	return (
		<ApplePayButton
			debug={false}
			scope='TapToken'
			publicKey='pk_test_Vlk842B1EA7tDN5QbrfGjYzh'
			environment='production'
			merchant={{
				domain: 'demo.staging.tap.company',
				id: '1124340'
			}}
			acceptance={{
				supportedBrands: ['mada', 'masterCard', 'visa']
			}}
			features={{
				supportsCouponCode: false,
			}}
			transaction={{
				currency: 'KWD',
				amount: '20'
                  }}
		 	customer={{
				name: [\
					{\
						locale: 'en',\
						first: 'test',\
						last: 'tester',\
						middle: 'test'\
					}\
				],
				contact: {
					email: 'test@gmail.com',
					phone: {
						number: '1000000000',
						countryCode: '+20'
					}
				}
			}}
			interface={{
				locale: 'en',
				theme: 'dark',
				type: 'buy',
				edges: 'curved'
			}}
			onCancel={() => {
				// it's called when the user cancels the payment
				console.log('onCancel')
			}}
			onError={(error) => {
				// it's called when there is an error with the payment
				console.log('onError', error)
			}}
			onReady={() => {
				// it's called when the apple pay button is ready to click
				console.log('onReady')
			}}
			onSuccess={async (data, event) => {
				// it's called when the payment is successful
				console.log('onSuccess', data)
				// event is the same as the event in the onpaymentauthorized event https://developer.apple.com/documentation/apple_pay_on_the_web/applepaypaymentauthorizedevent
				console.log('apple pay event', event)
			}}
		/>
	)
}

const root = createRoot(document.getElementById('root')!)
root.render(<App />)

```

## ApplePay Web SDK using Vanilla JS   [Skip link to ApplePay Web SDK using Vanilla JS](https://developers.tap.company/docs/apple-pay-web-sdk\#applepay-web-sdk-using-vanilla-js)

When implementing the below code, in order to add the ApplePay button on-page in your website, make sure that you pass the `publicKey` and `merchant.id` that Tap Payments will provide to you to have it linked to your account. Moreover, please add the domain that you have provided to Tap to whitelist in order to eliminate any errors.

Refer to the [Configurations](https://developers.tap.company/docs/apple-pay-web-sdk-v20#configurations) section for the definition of each field.

Vanilla JS

```rdmd-code lang-javascript theme-light
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>apple pay button</title>
    <link rel="stylesheet" href="https://tap-sdks.b-cdn.net/apple-pay/build-1.1.6/main.css" />
    <script src="https://tap-sdks.b-cdn.net/apple-pay/build-1.1.6/main.js"></script>
</head>

<body>
    <div id="apple-pay-button"></div>
    <script type="text/javascript">

        const { render, abortApplePaySession } =
            window.TapApplepaySDK
        render(
            {
                debug: false,
                scope: 'TapToken',
                publicKey: 'pk_test_Vlk842B1EA7tDN5QbrfGjYzh',
                environment: 'production',
                merchant: {
                    domain: 'demo.staging.tap.company',
                    id: '1124340'
                },
                acceptance: {
                    supportedBrands: ['mada','masterCard', 'visa']
                },
                features: {
                    supportsCouponCode: false
                },
                transaction: {
                    currency: 'AED',
                    amount: '20'

                },
                customer: {
                    name: [\
                        {\
                            locale: 'en',\
                            first: 'test',\
                            last: 'tester',\
                            middle: 'test'\
                        }\
                    ],
                    contact: {
                        email: 'test@gmail.com',
                        phone: {
                            number: '1000000000',
                            countryCode: '+20'
                        }
                    }
                },
                interface: {
                    locale: 'en',
                    theme: 'dark',
                    type: 'buy',
                    edges: 'curved'
                },
                onCancel: () => {
                    // it's called when the user cancels the payment
                    console.log('onCancel')
                },
                onError: (error) => {
                    // it's called when there is an error with the payment
                    console.log('onError', error)
                },
                onReady: () => {
                    // it's called when the apple pay button is ready to click
                    console.log('onReady')
                },
                onSuccess: async (data, event) => {
                    // it's called when the payment is successful
                    console.log('onSuccess', data)
                    // event is the same as the event in the onpaymentauthorized event https://developer.apple.com/documentation/apple_pay_on_the_web/applepaypaymentauthorizedevent
                    console.log('apple pay event', event)
                }
            'apple-pay-button'
        )
    </script>
</body>

</html>

```

# Specify the Environment   [Skip link to Specify the Environment](https://developers.tap.company/docs/apple-pay-web-sdk\#specify-the-environment)

In the Web SDK configuration, you can specify different values to indicate the environment you are working on. Choosing the correct environment based on your development stage is required. To determine the appropriate environment such as development, beta, or production, please refer to the following guidelines:

> ## 🚧  Apple Pay Testing Information
>
> You can use both test and live keys in all of the three environments, noting the below:
>
> **Using Test Keys:** When using test keys, transactions will be processed in a sandbox environment. No real money will be deducted, even if you use a real Apple Pay card. This is ideal for testing the integration without any financial impact.
>
> **Using Live Keys:** When using live keys, transactions will be processed in a live environment. This means real money will be deducted from the card used in the transaction. Ensure that your integration is thoroughly tested in the sandbox environment before switching to live keys.

### Development Environment   [Skip link to Development Environment](https://developers.tap.company/docs/apple-pay-web-sdk\#development-environment)

Mark the environment as Development when you are still testing in development mode. You can use the test keys in this mode.

JavaScript

```rdmd-code lang-javascript theme-light
publicKey={'pk_test_Vlk842B1EA7tDN5QbrfGjYzh'}
environment={Environment.Development} // or environment='development'
   merchant={{
    domain: 'demo.staging.tap.company',
    id: '1124340',
   }}

```

### Beta Environment   [Skip link to Beta Environment](https://developers.tap.company/docs/apple-pay-web-sdk\#beta-environment)

Mark the environment as Beta when you are in the process of QA live testing. This is usually used with live keys and live cards.

JavaScript

```rdmd-code lang-javascript theme-light
publicKey={'pk_live_2nDLY8eJ******VIm936P'} or { 'pk_test_Vlk842B1EA7tDN5QbrfGjYzh'}
environment={Environment.Beta} // or environment='beta'
   merchant={{
    domain: 'demo.staging.tap.company',
    id: '1124340'
   }}

```

### Production Environment   [Skip link to Production Environment](https://developers.tap.company/docs/apple-pay-web-sdk\#production-environment)

Once your website is in production and accessible to the customers, mark the environment as Production to show that you are fully live and ready to accept live payments with ApplePay.

JavaScript

```rdmd-code lang-javascript theme-light
publicKey={'pk_live_2nDLY8eJ******VIm936P'}
environment={Environment.Production} // or environment='production'
   merchant={{
    domain: 'demo.tap.company',
    id: '1124340'
   }}

```

> ## 👍  The Tap Payments Apple Pay Button SDK is designed to simplify the integration process. It abstracts the complexity of working directly with Apple Pay APIs.

# Event Handling in ApplePay Web SDK   [Skip link to Event Handling in ApplePay Web SDK](https://developers.tap.company/docs/apple-pay-web-sdk\#event-handling-in-applepay-web-sdk)

Implement the necessary event handling mechanism to capture the click event on the Apple Pay button. In the callback functions, you will see all the actions that are provided by the ApplePay Web SDK, noting that the `onSuccess` one will give you a result as data if the integration is working well. The data will contain the token ID in the syntax of `tok_xxx`, that needs to be passed in the `source.id` of the [Charge API](https://developers.tap.company/reference/create-a-charge) to complete the payment with ApplePay.

The below code snippet is available as part of the full ApplePay Web SDK code in the [Integration Section](https://developers.tap.company/docs/apple-pay-web-sdk-v20#applepay-web-sdk-integration).

> ## 📘  Refer to the [Configurations](https://developers.tap.company/docs/apple-pay-web-sdk-v20\#configurations) section for the definition of each callback function

Vanilla JSReact JS

```rdmd-code lang-javascript theme-light
onCancel: () => {
	// it's called when the user cancels the payment
	console.log('onCancel')
},
onError: (error) => {
	// it's called when there is an error with the payment
	console.log('onError', error)
},
onReady: () => {
	// it's called when the apple pay button is ready to click
	console.log('onReady')
},
onSuccess: async (data, event) => {
	// it's called when the payment is successful
	console.log('onSuccess', data)
	// event is the same as the event in the onpaymentauthorized event https://developer.apple.com/documentation/apple_pay_on_the_web/applepaypaymentauthorizedevent
	console.log('apple pay event', event)
},
onMerchantValidation: (status) => {
	// it's called when the merchant validation is done
	console.log('onMerchantValidation', status)
},
onPaymentMethodSelected: async (paymenMethod) => {
	// it's a function that give you a chance to update the total
	// amount and the line items based on the payment method
	return {
		newTotal: {
			label: 'Merchant Name',
			amount: '1.00'
		}
		// you can pass rest of options regarding applepay documentation (https://developer.apple.com/documentation/apple_pay_on_the_web/applepaypaymentmethodupdate)
	}
},
onShippingMethodSelected: async (shippingMehod) => {
	// it's a function that give you a chance to update the total
	// amount and the line items based on the shipping method
	return {
		newTotal: {
			label: 'Merchant Name',
			amount: '1.00'
		}
		// you can pass rest of options regarding applepay documentation (https://developer.apple.com/documentation/apple_pay_on_the_web/applepayshippingmethodupdate)
	}
},
onShippingContactSelected: async (shippingContact) => {
	// it's a function that give you a chance to update the total
	// amount and the line items based on the shipping contact
	return {
		newTotal: {
			label: 'Merchant Name',
			amount: '1.00'
		}
		// you can pass rest of options regarding applepay documentation (https://developer.apple.com/documentation/apple_pay_on_the_web/applepayshippingmethodupdate)
	}
},
onCouponChanged: async (couponCode) => {
	// it's a function that give you a chance to update the total
	// amount and the line items based on the coupon code
	return {
		newTotal: {
			label: 'Merchant Name',
			amount: '1.00'
		}
		// you can pass rest of options regarding applepay documentation (https://developer.apple.com/documentation/apple_pay_on_the_web/applepaypaymentmethodupdate)
	}
}

```

```rdmd-code lang-javascript theme-light
onCancel={() => {
	// it's called when the user cancels the payment
	console.log('onCancel')
}}
onError={(error) => {
	// it's called when there is an error with the payment
	console.log('onError', error)
}}
onReady={() => {
	// it's called when the apple pay button is ready to click
	console.log('onReady')
}}
onSuccess={async (data, event) => {
	// it's called when the payment is successful
	console.log('onSuccess', data)
	// event is the same as the event in the onpaymentauthorized event https://developer.apple.com/documentation/apple_pay_on_the_web/applepaypaymentauthorizedevent
	console.log('apple pay event', event)
}}
onMerchantValidation={(status) => {
	// it's called when the merchant validation is done
	console.log('onMerchantValidation', status)
}}
onPaymentMethodSelected={async (paymenMethod) => {
	// it's a function that give you a chance to update the total
	// amount and the line items based on the payment method
	return {
		newTotal: {
			label: 'Merchant Name',
			amount: '1.00'
		}
		// you can pass rest of options regarding applepay documentation (https://developer.apple.com/documentation/apple_pay_on_the_web/applepaypaymentmethodupdate)
	}
}}
onShippingMethodSelected={async (shippingMehod) => {
	// it's a function that give you a chance to update the total
	// amount and the line items based on the shipping method
	return {
		newTotal: {
			label: 'Merchant Name',
			amount: '1.00'
		}
		// you can pass rest of options regarding applepay documentation (https://developer.apple.com/documentation/apple_pay_on_the_web/applepayshippingmethodupdate)
	}
}}
onShippingContactSelected={async (shippingContact) => {
	// it's a function that give you a chance to update the total
	// amount and the line items based on the shipping contact
	return {
		newTotal: {
			label: 'Merchant Name',
			amount: '1.00'
		}
		// you can pass rest of options regarding applepay documentation (https://developer.apple.com/documentation/apple_pay_on_the_web/applepayshippingmethodupdate)
	}
}}
onCouponChanged={async (couponCode) => {
	// it's a function that give you a chance to update the total
	// amount and the line items based on the coupon code
	return {
		newTotal: {
			label: 'Merchant Name',
			amount: '1.00'
		}
		// you can pass rest of options regarding applepay documentation (https://developer.apple.com/documentation/apple_pay_on_the_web/applepaypaymentmethodupdate)
	}
}}

```

> ## 🚧  Safely store and transmit the token ID as it represents sensitive payment information. Follow industry-standard security practices to protect the token ID and prevent unauthorized access.

# Complete the Payment   [Skip link to Complete the Payment](https://developers.tap.company/docs/apple-pay-web-sdk\#complete-the-payment)

Construct the [Charges API request](https://developers.tap.company/docs/create-a-charge) with the necessary parameters, including the token ID, amount, currency, and any additional information required. Note that the token ID will be available in the callback function `onSuccess()` after the ApplePay tokenization is done.

> ## 📘  Update the user interface based on the status of the charge API response

## Handling Charge Status and Error Cases   [Skip link to Handling Charge Status and Error Cases](https://developers.tap.company/docs/apple-pay-web-sdk\#handling-charge-status-and-error-cases)

When creating a charge and interacting with the Tap Payments API, it's essential to handle various charge status scenarios and error cases. This ensures that you can provide appropriate feedback to your users and handle any potential issues gracefully. Follow these guidelines for effective charge status handling:

**Successful Charge**: If the charge status is CAPTURED, update the user interface to indicate a successful payment. Provide confirmation details such as the transaction ID and any relevant information.

**Failed Charge**: If the charge status is any other status than CAPTURED, it is not success. Therefore update the user interface to indicate the failure and provide an error message explaining the reason for the failure. It's important to display user-friendly error messages to assist the user in resolving any issues.

**Error Handling**: In case of any API errors or network failures, handle them gracefully. Display an error message to the user, offering guidance on what to do next. Additionally, consider logging the error details for troubleshooting purposes.

> ## 📘  Remember to test the integration thoroughly in a development or staging environment before deploying it to production. This will help identify and address any issues or potential pitfalls in the integration.

# Configurations   [Skip link to Configurations](https://developers.tap.company/docs/apple-pay-web-sdk\#configurations)

| Name | Type | R/O | Description |
| --- | --- | --- | --- |
| publicKey | string | required | The public Key provided by Tap |
| environment | enum | required | The environment of the SDK and it can be one of these environments: \[Development, Production\] |
| debug | boolean | optional | To enable the debug mode |
| merchant.id | string | required | The merchant identifier provided by Tap |
| merchant.domain | string | required | The merchant domain name |
| transaction.amount | string | required | The amount to be charged |
| transaction.currency | string | required | The currency of the amount |
| scope | enum | optional | The scope of the SDK |
| acceptance.supportedBrands | array | optional | The supported networks for the Apple Pay button |
| acceptance.supportedCards | array | optional | The supported cards for the Apple Pay button |
| acceptance.supportedCardsWithAuthentications | array | optional | The supported cards with authentications for the Apple Pay button |
| interface.theme | enum | optional | The theme of the Apple Pay button |
| interface.locale | Locale | optional | The locale of the Apple Pay button |
| interface.type | ButtonType | optional | The type of the Apple Pay button |
| interface.edges | ButtonType | optional | The border of the Apple Pay button |
| customer | object | required | The Customer details information |
| onCancel | function | optional | A callback function that will be called when you cancel the process |
| onError | function | optional | A callback function that will be called when you have an error |
| onSuccess | function | optional | A async function that will be called after creating the token successfully |
| onClick | function | optional | A callback function that will be called when the button is clicked |
| onReady | function | optional | A callback function that will be called when the button is clickable |
| onMerchantValidation | function | optional | A callback function that will be called when validate merchant callback status changed. available status are `initiated`, `completed`, `error` |
| onShippingMethodSelected | function | optional | A callback function that will be called when user change shipping method |
| onShippingContactSelected | function | optional | A callback function that will be called when user change shipping contacts or address |
| onPaymentMethodSelected | function | optional | A callback function that will be called when user change selected card payment |
| onCouponChanged | function | optional | A callback function that will be called when user apply new coupon code |

Should you encounter any difficulties or have specific questions, reach out to the Tap Payments support team for prompt assistance. Happy integrating!

Updated3 months ago

* * *