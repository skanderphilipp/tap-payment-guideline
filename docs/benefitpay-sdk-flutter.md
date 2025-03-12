# Introduction   [Skip link to Introduction](https://developers.tap.company/docs/benefitpay-sdk-flutter\#introduction)

Welcome to the Benefit Pay SDK! Before starting the development process, it's important to establish the essential prerequisites and criteria for a seamless integration. In this guide, we’ll cover the specific requirements for iOS and Android, including the minimum SDK versions and other key considerations. Let’s set your project up for success right from the start!

# Sample Demo   [Skip link to Sample Demo](https://developers.tap.company/docs/benefitpay-sdk-flutter\#sample-demo)

![](https://files.readme.io/e606c82-ezgif.com-optimize-3.gif)

> ## 📘  BenefitPay SDK allows users to make payments in two ways:
>
> 1. Scanning a QR code to initiate the payment
> 2. Directly using the BenefitPay App to make the payment

# Step 1: Requirements   [Skip link to Step 1: Requirements](https://developers.tap.company/docs/benefitpay-sdk-flutter\#step-1-requirements)

- We support from iOS 13.0+
- Dart 3.0.0+
- Java version 11
- A minimum [Android SDK/API level](https://developer.android.com/guide/topics/manifest/uses-sdk-element#ApiLevels) of 24
- in order to accept online payments on your application, you will need to add at least the Internet permission in the manifest file.

Dart

```rdmd-code lang-json theme-light
xml <uses-permission android:name="android.permission.INTERNET" /> //get internet access to complete online payments

```

# Step 2: Get Your Public Keys   [Skip link to Step 2: Get Your Public Keys](https://developers.tap.company/docs/benefitpay-sdk-flutter\#step-2-get-your-public-keys)

While you can certainly use the sandbox keys available within our sample app which you can get by following the [installation](https://pub.dev/packages/benefit_pay_flutter) process. However, we highly recommend visiting our [onboarding](https://register.tap.company/ae/en/sell) page, there you'll have the opportunity to register your package name and acquire your essential Tap Key for activating Card-Flutter integration. If you will support both iOS and Android, you will need to have two different keys for each app.

# Step 3: Installation   [Skip link to Step 3: Installation](https://developers.tap.company/docs/benefitpay-sdk-flutter\#step-3-installation)

In the `pubspec.yaml` of your flutter project, add the following dependency:

`benefit_pay_flutter: ^1.0.0`

To download the example code from [GitHub](https://github.com/Tap-Payments/BenefitPay-Flutter)

# Step 4: Integrating BenefitPay-Flutter   [Skip link to Step 4: Integrating BenefitPay-Flutter](https://developers.tap.company/docs/benefitpay-sdk-flutter\#step-4-integrating-benefitpay-flutter)

## Integration Flow   [Skip link to Integration Flow](https://developers.tap.company/docs/benefitpay-sdk-flutter\#integration-flow)

Note that in Flutter, you will use our button like any other widget. While creating, the widget you will also need to pass the parameters & listen to the callbacks based on your needs.

1. You will have to create a variable of type TapBenefitPayWidget
2. While initializing the widget:
   - Pass the parameters to the widget.
   - Implement the provided interfaces/callbacks
3. Our button widget is a stateful one and depends on a stateful variable to listen to all callbacks.

### Using Code to create the TapBenefitPayWidget   [Skip link to Using Code to create the TapBenefitPayWidget](https://developers.tap.company/docs/benefitpay-sdk-flutter\#using-code-to-create-the-tapbenefitpaywidget)

- Creating the TapBenefitPayWidget from code

1. Head to your controller where you want to display the TapBenefitPayWidget as a widget.
2. Import `TapBenefitPayWidget` as follows

`import 'package:benefit_pay_flutter/benefit_pay_flutter.dart';.`
3. In the coming code sample, we will show how to embed the button form within your widget tree.



Dart





```rdmd-code lang-json theme-light
TapBenefitPayWidget(
      sdkConfiguration: const {},
    ),

```


### Configuring the BenefitPay-Flutter SDK   [Skip link to Configuring the BenefitPay-Flutter SDK](https://developers.tap.company/docs/benefitpay-sdk-flutter\#configuring-the-benefitpay-flutter-sdk)

While creating the widget as previously mentioned, it is time to pass the parameters needed for the SDK to work as expected and serve your needs correctly.

1. Pass these parameters to the TapBenefitPayWidget widget

Dart

```rdmd-code lang-json theme-light
sdkConfiguration: const {

  "merchant": {
    "id": "",
  },
  "scope": "charge",
  "redirect": "",
  "customer": {
    "names": [\
      {\
        "middle": "Middle",\
        "last": "Payments",\
        "lang": "en",\
        "first": "Tap"\
      }\
    ],
    "contact": {
      "phone": {
        "number": "66178990",
        "countryCode": "965"
      },
      "email": "email@email.com"
    },
    "id":"",
  },
  "locale": "en",
  "edges": "curved",
  "reference": {"transaction": "transaction", "order": "12"},
  "metadata": "",
  "post": {"url": ""},
  "transaction": {
    "amount": "10",
    "currency": "BHD",
  },
  "operator": {
    "hashString": "",
    "publicKey": 'pk_live_********',
  },

}

```

**Full code snippet for creating the parameters + passing it TapBenefitPayWidget variable + Listening to callbacks**

Dart

```rdmd-code lang-json theme-light
 import 'package:benefit_pay_flutter/benefit_pay_flutter.dart'; import 'package:flutter/material.dart';
 class BenefitPayScreen extends StatefulWidget {
  final Map<String, dynamic> dictionaryMap;

  const BenefitPayScreen({
    super.key,
    required this.dictionaryMap,
  });

@override State<BenefitPayScreen> createState() => _BenefitPayScreenState(); }
 class _BenefitPayScreenState extends State<BenefitPayScreen> {
  String sdkResponse = "";

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.white,
      appBar: AppBar(
        title: const Text('Plugin example app'),
      ),
      body: Padding(
        padding: const EdgeInsets.symmetric(
          horizontal: 18,
          vertical: 50,
        ),
        child: SingleChildScrollView(
          child: Center(
            child: SelectableText(
              sdkResponse.isEmpty ? " " : "SDK RESPONSE : $sdkResponse",
            ),
          ),
        ),
      ),
      bottomSheet: Padding(
        padding: const EdgeInsets.only(bottom: 20),
        child: TapBenefitPayWidget(
          sdkConfiguration: widget.dictionaryMap,
          onReady: () {
            developer.log(">ON READY >>>>");
          },
          onCancel: () {
            developer.log(">ON CANCEL >>>>");
            setState(() {
              sdkResponse = "Cancelled";
            });
          },
          onSuccess: (String? value) {
            developer.log(">ON SUCCESS >>>> $value");
            setState(() {
              sdkResponse = value ?? "";
            });
          },
          onError: (String? error) {
            developer.log(">ON ERROR >>>> $error");
            setState(() {
              sdkResponse = error ?? "";
            });
          },
          onClick: () {

          },
          onOrderCreated: (String? value) {
            developer.log(">ON ORDER CREATED >>>> $value");
            setState(() {
              sdkResponse = value ?? "";
            });
          },
          onChargeCreated: (String? value) {
            developer.log(">ON CHARGE CREATED >>>> $value");
            setState(() {
              sdkResponse = value ?? "";
            });
          },
        ),
      ),
    );
   }
 }

```

# Parameters Reference   [Skip link to Parameters Reference](https://developers.tap.company/docs/benefitpay-sdk-flutter\#parameters-reference)

Below you will find more details about each parameter shared in the above tables that will help you easily integrate BenefitPay-Flutter SDK.

| Parameter | Description | Required | Type | Fields | Sample |
| --- | --- | --- | --- | --- | --- |
| operator | It links the payment gateway to your merchant account with Tap, in order to know your business name, logo, etc... | True | string | **publicKey**<br>Definition:This is a unique public key that you will receive after creating an account with Tap which is considered a reference to identify you as a merchant. You will receive 2 public keys, one for sandbox/testing and another one for production.<br>**hashString**<br>Definition: It is an encrypted string that combines the sensitive details of your transaction to mitigate any fraud manipulations.. | ` "operator": {          "publicKey": "pk_test_HJN863LmO15EtDgo9cqK7sjS",          "hashString": ""       },` |
| transaction | This defined the details of the order that you are trying to purchase, in which you need to specify some details like the reference, scope... | True | Dictionary | **currency**<br>Definition: The currency which is linked to the order being paid.<br>**amount**<br>Definition: The order amount to be paid by the customer.<br>Note: Minimum amount to be added is 0.1. | `"transaction": {    "amount": 1.0,   "currency": "BHD", }` |
| customer | Here, you will collect the information of the customer that is paying.. | True | Dictionary | **id**<br>Definition: This is an optional field that you do not have before the charge is processed. But, after the charge, then you will receive the customer ID in the response which can be handled in the onSuccess callback function.<br>**name**<br>Definition: Full Name of the customer paying.<br>`Fields: `<br>1\. lang<br>Definition: Language chosen to write the customer name.<br>2\. first<br>Definition: Customer's first name.<br>3\. middle<br>Definition: Customer's middle name.<br>4\. last<br>Definition: Customer's last name.<br>**contact**<br>Definition: The customer's contact information like email address and phone number.<br>Note: The contact information has to either have the email address or the phone details of the customers or both but it should not be empty.<br>Fields:<br>5\. email<br>Definition: Customer's email address<br>Note: The email is of type string.<br>6\. phone<br>Definition: Customer's Phone number details<br>a. countryCode<br>b. number | ` "id": customerIdController.text,     "names": const [       {         "first": "TAP",         "middle": "",         "last": "PAYMENTS",         "lang": "en",       }     ],     "contact": const {       "email": "[tap@tap.company](mailto:tap@tap.company) ",       "phone": {         "countryCode": "+965",         "number": "88888888"       }      },     },    }` |
| interface | This will help you control the layout (UI) of the payment form, like changing the theme light to dark, the language used (en or ar), ... | False | Dictionary | **locale**<br>Definition: The language of the pay button. Accepted values as of now are:<br>Possible Values:<br>\- en(for english)<br>\- ar(for arabic). **edges**<br>Definition: Control the edges of the payment form.<br>Possible Values:<br>\- curved<br>\- flat | ` "interface":  {  "locale": "en",     "edges": "flat",    }` |
| post | Here you can pass the webhook URL you have, in order to receive notifications of the results of each Transaction happening on your application. | True | Dictionary | **url**<br>Definition: The webhook server's URL that you want to receive notifications on. | ` "post": const {"url": "http\://your_website.com/post_url"},` |

# Generate the hash string   [Skip link to Generate the hash string](https://developers.tap.company/docs/benefitpay-sdk-flutter\#generate-the-hash-string)

1. Add the dependency `crypto: Latest version`
2. Copy this helper method code


This is a helper method showing how can you generate a hash string when performing live charges

   - Parameter publicKey: The Tap public key for you as a merchant pk\_.....
   - Parameter secretKey: The Tap secret key for you as a merchant sk\_.....
   - Parameter amount: The amount you are passing to the SDK, to the amount you used in the order if you created the order before.
   - Parameter currency:The currency code you are passing to the SDK, to the currency code you used in the order if you created the order before. PS: It is the capital case of the 3 iso country codes ex: SAR, KWD.
   - Parameter post: The post URL you are passing to the SDK, to the post url you pass within the Charge API.


     If you are not using postUrl please pass it as an empty string
   - Parameter transactionReference: The reference.trasnsaction you are passing to the SDK(not all SDKs supports this,) or the reference.trasnsaction you pass within the Charge API.


     If you are not using reference.trasnsaction please pass it as an empty string.

> ## 🚧  For the production environment, it is required to provide the hashsting parameter, as it is a necessary component for the functionality to work correctly.
>
> Conversely, in the sandbox environment, the hashsting parameter is not required.

Dart

```rdmd-code lang-json theme-light
  String generateTapHashString(
        String publicKey,
        String secretKey,
        double amount,
        String currency, {
        String postUrl = "",
        String transactionReference = "",
     }) {
       // Let us generate our encryption key
       var key = utf8.encode(secretKey);
       // For amounts, you will need to make sure they are formatted in a way to have     the correct number of decimal points. For BHD we need them to have 3 decimal points
       var formattedAmount = amount.toStringAsFixed(3);
       // Let us format the string that we will hash
       var toBeHashed = 'x_publickey$publicKey'
       'x_amount$formattedAmount'
       'x_currency$currency'
       'x_transaction$transactionReference'
       'x_post$postUrl';
       // let us generate the hash string now using the HMAC SHA256 algorithm
       var hmacSha256 = Hmac(sha256, key);
       var signature = hmacSha256.convert(utf8.encode(toBeHashed));
       var hashedString = signature.toString();
       return hashedString;
}

```

3. Next, you should call it as shown below:






dart





```rdmd-code lang-Text theme-light
    String hashString = generateTapHashString(publicKey: publicKey, secretKey: secretString, amount: amount, currency: currency, postUrl: postUrl,transactionReference:transactionReference);

```

4. Finally, you need to Pass it within the operator model as shown below:






dart





```rdmd-code lang-Text theme-light
     { "operator": {"publicKey": "pk_test_HJN863LmO15EtDgo9cqK7sjS", "hashString": hashString } }

```


Reaching this point, you will be successfully integrated our benefitpay-sdk into your flutter application

Updated2 months ago

* * *