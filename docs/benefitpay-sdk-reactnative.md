# Introduction   [Skip link to Introduction](https://developers.tap.company/docs/benefitpay-sdk-reactnative\#introduction)

Before diving into the development process, it's essential to establish the prerequisites and criteria necessary for a successful build. In this step, we'll outline the specific requirements, including the minimum SDK version and other important details you need to consider. Let's ensure your project is set up for success from the very beginning.

# Sample demo   [Skip link to Sample demo](https://developers.tap.company/docs/benefitpay-sdk-reactnative\#sample-demo)

![](https://files.readme.io/322930971d5718aa177620996a1847c3f4a651d481792159fb62ed75586d75fb-277257470-5849ba95-3375-4b8e-8bb9-c34d6dab2008-ezgif.com-video-to-gif-converter.gif)

# Step 1: Requirements   [Skip link to Step 1: Requirements](https://developers.tap.company/docs/benefitpay-sdk-reactnative\#step-1-requirements)

1. React native 0.64
2. A minimum [Android SDK/API](https://developer.android.com/guide/topics/manifest/uses-sdk-element#ApiLevels) level of 24+
3. In order to accept online payments on your application, you will need to add at least the Internet permission in the manifest file.

D

```rdmd-code lang-d theme-light
<uses-permission android:name="android.permission.INTERNET" />
//get internet access to complete online payments

```

# Step 2: Get Your Public Keys   [Skip link to Step 2: Get Your Public Keys](https://developers.tap.company/docs/benefitpay-sdk-reactnative\#step-2-get-your-public-keys)

While you can certainly use the sandbox keys available within our sample app which you can get by following the [installation](https://developers.tap.company/docs/android-card-sdk#step-3-installation-using-gradle) process, however, we highly recommend visiting our [onboarding](https://register.tap.company/ae/en/sell) page, there you'll have the opportunity to register your package name and acquire your essential Tap Key for activating Card integration.

# Step 3: Installation   [Skip link to Step 3: Installation](https://developers.tap.company/docs/benefitpay-sdk-reactnative\#step-3-installation)

We got you covered, `benefit-pay-react-native` can be installed with all possible technologies.

### Node modules   [Skip link to Node modules](https://developers.tap.company/docs/benefitpay-sdk-reactnative\#node-modules)

D

```rdmd-code lang-d theme-light
npm install benefit-pay-react-native

```

D

```rdmd-code lang-d theme-light
yarn install benefit-pay-react-native

```

Then run in your terminal

D

```rdmd-code lang-d theme-light
cd ios
pod install
pod update

```

### Import the dependency   [Skip link to Import the dependency](https://developers.tap.company/docs/benefitpay-sdk-reactnative\#import-the-dependency)

D

```rdmd-code lang-d theme-light
import BenefitPayView from ‘benefit-pay-react-native’;

```

# Step 4: Integrating Benefit-pay-react-native   [Skip link to Step 4: Integrating Benefit-pay-react-native](https://developers.tap.company/docs/benefitpay-sdk-reactnative\#step-4-integrating-benefit-pay-react-native)

This integration offers a simple integration designed for rapid development and streamlined merchant requirements.

## Integration Flow   [Skip link to Integration Flow](https://developers.tap.company/docs/benefitpay-sdk-reactnative\#integration-flow)

Here, you'll discover a comprehensive table featuring the parameters applicable to the simple integration. Additionally, you'll explore the various methods for integrating the SDK, either using storyboard to create the layout and then implementing the controllers functionalities by code, or directly using code. Furthermore, you'll gain insights into card tokenization after the initial payment and learn how to receive the callback notifications.

### Parameters   [Skip link to Parameters](https://developers.tap.company/docs/benefitpay-sdk-reactnative\#parameters)

Each parameter is linked to the `Parameters Reference` section, which provides a more in depth explanation of it.

| Configuration | Description | Required | Type | Sample |
| --- | --- | --- | --- | --- |
| operator | This is the `Key` that you will get after registering you bundle id. | True | `String` | `let operator {publicKey: 'pk_test_YhUjg9PNT8oDlKJ1aE2fMRz7', hashString:''}` |
| Transaction | amount and `currency` to generate a new transaction. It will be linked this token. | True | `Transaction` | `let order: = { amount: 1, currency: TapCurrencyCode.SAR, description: '', id: '', , reference : ''}` |

### Widget initialisation   [Skip link to Widget initialisation](https://developers.tap.company/docs/benefitpay-sdk-reactnative\#widget-initialisation)

D

```rdmd-code lang-d theme-light
function MinRequirement() {
  return (
    <View
      style={{
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center',
      }}
    >
      <BenefitPayView
        onSuccess={(data) => {
          console.log(
            '🚀 ~ tokenValue:',
            data
          );
        }}
        onError={(data) => {
          console.log(
            '🚀 ~ onError:',
            data
          );
        }}
        style={{ width: '100%' }}
        config={{
          androidOperator: {
            hashString: '',
            publicKey: 'pk_live_********',
          },
          iOSOperator: {
            hashString: '',
            publicKey: 'pk_live_********',
          },
          merchant: {
            id: '',
          },
          transaction: {
            amount: 1,
            currency: TapCurrencyCode.BHD,
          },
          customer: {
            id:"",
            name: [\
              {\
                first: 'Tap',\
                lang: Locale.en,\
                middle: 'Company',\
                last: 'Payments',\
              },\
            ],
            contact: {
              phone: {
                number: '88888888',
                countryCode: '+965',
              },
              email: 'tappayments@tap.company',
            },
          },
        }}
        onReady={() => {
          console.log(
            '🚀 ~ file: HomeScreen.tsx:145 ~ HomeScreen ~ onReady:',
          );
        }}
      />
    </View>
  );
}

```

# Parameters Reference   [Skip link to Parameters Reference](https://developers.tap.company/docs/benefitpay-sdk-reactnative\#parameters-reference)

Below you will find more details about each parameter shared in the above tables that will help you easily integrate BenefitPay-React-Native SDK.

| Parameter | Description | Required | Type | Fields | Sample |
| --- | --- | --- | --- | --- | --- |
| operator | It links the payment gateway to your merchant account with Tap, in order to know your business name, logo, etc... | True | string | **publicKey**<br>Definition:This is a unique public key that you will receive after creating an account with Tap which is considered a reference to identify you as a merchant. You will receive 2 public keys, one for sandbox/testing and another one for production.<br>**hashString**<br>Definition: It is an encrypted string that combines the sensitive details of your transaction to mitigate any fraud manipulations.. | ` "operator": {          "publicKey": "pk_test_HJN863LmO15EtDgo9cqK7sjS",          "hashString": ""       },` |
| transaction | This defined the details of the order that you are trying to purchase, in which you need to specify some details like the reference, scope... | True | Dictionary | **currency**<br>Definition: The currency which is linked to the order being paid.<br>**amount**<br>Definition: The order amount to be paid by the customer.<br>Note: Minimum amount to be added is 0.1. | `"transaction": {    "amount": 1.0,   "currency": "BHD", }` |
| merchant | This defined the details of the order that you are trying to purchase, in which you need to specify some details like the id, amount, currency ... | True | Dictionary | **id**<br>Definition: Generated once your account with Tap is created, which is unique for every merchant. | `const merchant = {id:""}` |
| customer | Here, you will collect the information of the customer that is paying.. | True | Dictionary | **id**<br>Definition: This is an optional field that you do not have before the charge is processed. But, after the charge, then you will receive the customer ID in the response which can be handled in the onSuccess callback function.<br>**name**<br>Definition: Full Name of the customer paying.<br>`Fields: `<br>1\. lang<br>Definition: Language chosen to write the customer name.<br>2\. first<br>Definition: Customer's first name.<br>3\. middle<br>Definition: Customer's middle name.<br>4\. last<br>Definition: Customer's last name.<br>**contact**<br>Definition: The customer's contact information like email address and phone number.<br>Note: The contact information has to either have the email address or the phone details of the customers or both but it should not be empty.<br>Fields:<br>5\. email<br>Definition: Customer's email address<br>Note: The email is of type string.<br>6\. phone<br>Definition: Customer's Phone number details<br>a. countryCode<br>b. number | ` "id": customerIdController.text,     "names": const [       {         "first": "TAP",         "middle": "",         "last": "PAYMENTS",         "lang": "en",       }     ],     "contact": const {       "email": "[tap@tap.company](mailto:tap@tap.company) ",       "phone": {         "countryCode": "+965",         "number": "88888888"       }      },     },    }` |
| interface | This will help you control the layout (UI) of the payment form, like changing the theme light to dark, the language used (en or ar), ... | False | Dictionary | **locale**<br>Definition: The language of the pay button. Accepted values as of now are:<br>Possible Values:<br>\- en(for english)<br>\- ar(for arabic). **edges**<br>Definition: Control the edges of the payment form.<br>Possible Values:<br>\- curved<br>\- flat | ` "interface":  {  "locale": "en",     "edges": "flat",    }` |
| post | Here you can pass the webhook URL you have, in order to receive notifications of the results of each Transaction happening on your application. | False | Dictionary | **url**<br>Definition: The webhook server's URL that you want to receive notifications on. | ` "post": const {"url": "http\://your_website.com/post_url"},` |
| redirect | Redirection Url. | False | String |  | `const redirect: 'tapredirectionwebsdk://'` |
| metadata | transaction meta data. | False | String |  | `const metadata: 'metadata'` |

### BenefitPayView Callbacks   [Skip link to BenefitPayView Callbacks](https://developers.tap.company/docs/benefitpay-sdk-reactnative\#benefitpayview-callbacks)

callbacks that allows integrators to get notified from events fired from the `BenefitPayView`.

D

```rdmd-code lang-d theme-light
{
  ///  Will be fired whenever there is an error related to the button connectivity or apis
  ///  - Parameter  data: includes a JSON format for the error description and error
  const onError = (data: String) => {}
	///  Will be fired whenever the charge is completed, regardless of its status.
	///  - Parameter  data: includes a JSON format for the charge details
  const onSuccess = (data: String) => {}
	///  Will be fired whenever the order is created. use it, if you want to retrieve its data from your backend for state manegement purposes
	///  - Parameter  data: Order id.
  const onOrderCreated = (data: String)  => {}
	///  Will be fired whenever the charge is created. use it, if you want to retrieve its data from your backend for state manegement purposes
	///  - Parameter  data: json data representing the charge model.
  const onChargeCreated = (data: String)  => {}
  ///  Will be fired whenever the benefit pay button is rendered and loaded
  const onReady = ()  => {}
  ///  Will be fired whenever the customer clicked on the benefit pay button. Now the button will be in loading state to render the benefit pay popup
  const onClicked = ()  => {}
  ///  Will be fired whenever the customer cancels the payment. This will reload the button once again
  func onCanceled = () => {}

}

```

### Expected Callbacks Responses   [Skip link to Expected Callbacks Responses](https://developers.tap.company/docs/benefitpay-sdk-reactnative\#expected-callbacks-responses)

### onError   [Skip link to onError](https://developers.tap.company/docs/benefitpay-sdk-reactnative\#onerror)

D

```rdmd-code lang-d theme-light
{
    "error":""
}

```

### onOrderCreated   [Skip link to onOrderCreated](https://developers.tap.company/docs/benefitpay-sdk-reactnative\#onordercreated)

D

```rdmd-code lang-d theme-light
"ord_uAx145231127yHYS19Ou9B126"

```

### onChargeCreated   [Skip link to onChargeCreated](https://developers.tap.company/docs/benefitpay-sdk-reactnative\#onchargecreated)

D

```rdmd-code lang-d theme-light
{
    "id": "chg_TS07A5220231433Ql241910314",
    "object": "charge",
    "live_mode": false,
    "customer_initiated": true,
    "api_version": "V2",
    "method": "CREATE",
    "status": "INITIATED",
    "amount": 0.1,
    "currency": "BHD",
    "threeDSecure": true,
    "card_threeDSecure": false,
    "save_card": false,
    "order_id": "ord_uAx145231127yHYS19Ou9B126",
    "product": "GOSELL",
    "order": {
        "id": "ord_uAx145231127yHYS19Ou9B126"
    },
    "transaction": {
        "timezone": "UTC+03:00",
        "created": "1697726033236",
        "url": "",
        "expiry": {
            "period": 30,
            "type": "MINUTE"
        },
        "asynchronous": false,
        "amount": 0.1,
        "currency": "BHD"
    },
    "response": {
        "code": "100",
        "message": "Initiated"
    },
    "receipt": {
        "email": true,
        "sms": true
    },
    "customer": {
        "first_name": "TAP",
        "last_name": "PAYMENTS",
        "email": "tap@tap.company",
        "phone": {
            "country_code": " 965",
            "number": "88888888"
        }
    },
    "merchant": {
        "country": "KW",
        "currency": "KWD",
        "id": "599424"
    },
    "source": {
        "object": "source",
        "id": "src_benefit_pay"
    },
    "redirect": {
        "status": "PENDING",
        "url": ""
    },
    "post": {
        "status": "PENDING",
        "url": ""
    },
    "activities": [\
        {\
            "id": "activity_TS02A5420231433Mx4g1910470",\
            "object": "activity",\
            "created": 1697726033236,\
            "status": "INITIATED",\
            "currency": "BHD",\
            "amount": 0.1,\
            "remarks": "charge - created"\
        }\
    ],
    "auto_reversed": false,
    "gateway_response": {
        "name": "BENEFITPAY",
        "request": {
            "amount": "0.100",
            "currency": "BHD",
            "hash": "gMjpC12Ffz+CMhyvm+/jdYJmqbPdgAhHJvvGBABYhCI=",
            "reference": {
                "transaction": "chg_TS07A5220231433Ql241910314"
            },
            "merchant": {
                "id": "00000101"
            },
            "application": {
                "id": "4530082749"
            },
            "configuration": {
                "show_result": "0",
                "hide_mobile_qr": "0",
                "frequency": {
                    "start": 120,
                    "interval": 60,
                    "count": 10,
                    "type": "SECOND"
                }
            }
        }
    }
}

```

### onSuccess   [Skip link to onSuccess](https://developers.tap.company/docs/benefitpay-sdk-reactnative\#onsuccess)

D

```rdmd-code lang-d theme-light
{
    "id": "chg_TS07A5220231433Ql241910314",
    "object": "charge",
    "live_mode": false,
    "customer_initiated": true,
    "api_version": "V2",
    "method": "UPDATE",
    "status": "INITIATED",
    "amount": 0.1,
    "currency": "BHD",
    "threeDSecure": true,
    "card_threeDSecure": false,
    "save_card": false,
    "order_id": "ord_uAx145231127yHYS19Ou9B126",
    "product": "GOSELL",
    "description": "",
    "order": {
        "id": "ord_uAx145231127yHYS19Ou9B126"
    },
    "transaction": {
        "timezone": "UTC+03:00",
        "created": "1697726033236",
        "url": "https://sandbox.payments.tap.company/test_gosell/v2/payment/tap_process.aspx?chg=8D9e9fdEo5N03hWrGnROvEEFw4DfqYVFv8R7R34GITc%3d",
        "expiry": {
            "period": 30,
            "type": "MINUTE"
        },
        "asynchronous": false,
        "amount": 0.1,
        "currency": "BHD"
    },
    "response": {
        "code": "100",
        "message": "Initiated"
    },
    "receipt": {
        "email": true,
        "sms": true
    },
    "customer": {
        "first_name": "TAP",
        "last_name": "PAYMENTS",
        "email": "tap@tap.company",
        "phone": {
            "country_code": " 965",
            "number": "88888888"
        }
    },
    "merchant": {
        "country": "KW",
        "currency": "KWD",
        "id": "599424"
    },
    "source": {
        "object": "source",
        "id": "src_benefit_pay"
    },
    "redirect": {
        "status": "PENDING",
        "url": ""
    },
    "post": {
        "status": "PENDING",
        "url": ""
    },
    "activities": [\
        {\
            "id": "activity_TS02A5420231433Mx4g1910470",\
            "object": "activity",\
            "created": 1697726033236,\
            "status": "INITIATED",\
            "currency": "BHD",\
            "amount": 0.1,\
            "remarks": "charge - created"\
        }\
    ],
    "auto_reversed": false,
    "gateway_response": {
        "name": "BENEFITPAY",
        "request": {
            "amount": "0.100",
            "currency": "BHD",
            "hash": "gMjpC12Ffz+CMhyvm+/jdYJmqbPdgAhHJvvGBABYhCI=",
            "reference": {
                "transaction": "chg_TS07A5220231433Ql241910314"
            },
            "merchant": {
                "id": "00000101"
            },
            "application": {
                "id": "4530082749"
            },
            "configuration": {
                "show_result": "0",
                "hide_mobile_qr": "0",
                "frequency": {
                    "start": 120,
                    "interval": 60,
                    "count": 10,
                    "type": "SECOND"
                }
            }
        }
    }
}

```

# Generate the hash string   [Skip link to Generate the hash string](https://developers.tap.company/docs/benefitpay-sdk-reactnative\#generate-the-hash-string)

1. Install crypto-js `npm install crypto-js`
2. Import



D





```rdmd-code lang-d theme-light
     import sha256 from 'crypto-js/sha256';
     import hmacSHA256 from 'crypto-js/hmac-sha256';
     import Base64 from 'crypto-js/enc-base64';

```

3. Copy this helper method code



D





```rdmd-code lang-d theme-light
/\*_
        This is a helper method showing how can you generate a hash string when performing live charges
     - Parameter publicKey:             The Tap public key for you as a merchant pk_.....
     - Parameter secretKey:             The Tap secret key for you as a merchant sk_.....
     - Parameter amount:                The amount you are passing to the SDK, ot the amount you used in the order if you created the order before.
     - Parameter currency:              The currency code you are passing to the SDK, ot the currency code you used in the order if you created the order before. PS: It is the capital case of the 3 iso country code ex: SAR, KWD.
     - Parameter post:                  The post url you are passing to the SDK, ot the post url you pass within the Charge API. If you are not using postUrl please pass it as empty string
     - Parameter transactionReference:  The reference.trasnsaction you are passing to the SDK(not all SDKs supports this,) or the reference.trasnsaction  you pass within the Charge API. If you are not using reference.trasnsaction please pass it as empty string
     _/
      const generateTapHashString = (
        publicKey: string,
        secretKey: string,
        amount: number,
        currency: string,
        postUrl: string = '',
        transactionReference: string = ''
      ) => {
        // Let us generate our encryption key
        // For amounts, you will need to make sure they are formatted in a way to have the correct number of decimal points. For BHD we need them to have 3 decimal points
        const formattedAmount = amount.toFixed(3);
        // Let us format the string that we will hash
        const toBeHashed = 'x_publickey${publicKey}x_amount${formattedAmount}x_currency${currency}x_transaction${transactionReference}x_post${postUrl}';
        // let us generate the hash string now using the HMAC SHA256 algorithm
        const hashDigest = sha256(toBeHashed);
        const hmacDigest = Base64.stringify(hmacSHA256(hashDigest, secretKey));
        return hmacDigest;
      };

```

4. Call it as follows:



D





```rdmd-code lang-d theme-light
let hashString = generateTapHashString(publicKey: publicKey, secretKey: secretString, amount: amount, currency: currency, postUrl: postUrl)

```

5. Pass it within the operator model



D





```rdmd-code lang-d theme-light
let operatorModel = {publicKey: "pk_test_HJN863LmO15EtDgo9cqK7sjS", hashString: hashString}

```


Updated2 months ago

* * *

- [react-native](https://www.npmjs.com/search?q=keywords:react-native)
- [ios](https://www.npmjs.com/search?q=keywords:ios)
- [android](https://www.npmjs.com/search?q=keywords:android)