Google Pay should be enabled from the _tap_ side before using it on the Merchant side.

It's currently supported in UAE, KSA, and KW, with currencies AED, SAR, and KWD, respectively, and USD is an addition.

_"We keep adding more countries and currencies. For more updates, please keep in touch with TAP support teams"_

* * *

# Integration with Google Pay   [Skip link to Integration with Google Pay](https://developers.tap.company/docs/google-pay\#integration-with-google-pay)

Google Pay integration depends on the UI mode chosen by the merchant.

* * *

## Web-based \[redirect/popup\]   [Skip link to Web-based [redirect/popup]](https://developers.tap.company/docs/google-pay\#web-based-redirectpopup)

It doesn't require any configuration from the merchant's side. The Google Pay option will appear on our hosted payment page or popup window automatically. Customers can choose and make a payment.

* * *

## Web-based \[iframe\]   [Skip link to Web-based [iframe]](https://developers.tap.company/docs/google-pay\#web-based-iframe)

Tap iFrame/embedded form does not support the Google Pay option. So, merchants can add a separate button for Google Pay on the checkout page for the customers' choice.

The button can be integrated with the backend APIs, as explained below

Google Pay Integration [Google References](https://developers.google.com/pay/api/web/guides/resources/demos)

When you follow google example in the link above you will find an object named _tokenizationSpecification_ and inside that object you will find another object called _parameters_ you have to pass the keyword **tappayments** in the _gateway_ and your MID with tap inside _gatewayMerchantId_ like below

google pay

```rdmd-code lang-javascript theme-light

const tokenizationSpecification = {
      type: "PAYMENT_GATEWAY",
      parameters: {
        gateway: "tappayments",
        gatewayMerchantId: "your MID",
      },
    };

```

After you send the request you will get the token data in the response under `paymentData.paymentMethodData.tokenizationData.token` as per the example in google pay documentation.

## Mobile-based   [Skip link to Mobile-based](https://developers.tap.company/docs/google-pay\#mobile-based)

You can follow our [documentation on github](https://github.com/Tap-Payments/goSellSDK-AndroidX?tab=readme-ov-file#google_pay) for Google Pay integration with full details.

API Call for tokenizing the data that comes from the google pay callback function, as below:

### API request   [Skip link to API request](https://developers.tap.company/docs/google-pay\#api-request)

Sample request

cURL

```rdmd-code lang-curl theme-light

curl --location --request POST 'https://api.tap.company/v2/tokens' \
--header 'Authorization: Bearer sk_test_jrJQTIMVt9oY0FNyEbCguXXX' \
--header 'Content-Type: application/json' \
--data-raw '{
    "type": "googlepay",
    "token_data": {
        "signature": "MEUCIQCgAIHrd65KhLQR4KMDqwfSYyjdF/rKUQG7eVPAP2NIuAIgWcA02MjvXAD9Xo4u2O6gl6PBjNNJeLTNy++paOGE3nE=",
        "intermediateSigningKey": {
            "signedKey": "{\"keyValue\":\"/uCLf1SqYc4feUicYPJSIu1djT3RQXe/71W50TegMLcs94OScACGtOPaiJmZwUPxCA\\u003d\\u003d\",\"keyExpiration\":\"1663134862361\"}",
            "signatures": [\
                "MEYCIQDf7b5O3xatEfZu9aK1+IebTs1N2otF++MtdgwitZK6iUf2hNdb4XXut+k5H8tHj"\
            ]
        },
        "protocolVersion": "ECv2",
        "signedMessage": "{\"encryptedMessage\":\"8tW8iQuL8dOyZ1+OhZMMzVXFggBsE2dKobOsNw00nOQI7JuY7Zfqq4kbae+o48HoXDayEHkjFlnXW/QZBIHBqWgrMce9LJj+jnYTN7WcAAxLNbwf3leZs+zV7GMV+0aMAsOOdvKdurCg7LBIDJZeNbMyomtp9HqQ+paLjgxqtvOGnZ5jJoYMTQqOR+qdFmxvsOqhHZHtiRvdTQi8Z9p9+jvbn28M0DRle1COyQOrhnOVZ7RUu1kYaMm7cOxeXbXP4CuuCb2EQZ\",\"ephemeralPublicKey\":\"BPYdAC923D/jRypCseOUA9bersY0i\\u003d\",\"tag\":\"UcPrx3j4NzXy38/pKZ4nXEViVSKacXEQpxeRxqdkZPU\\u003d\"}"
    },
    "client_ip": "192.168.1.20"
}'

```

* * *

### API Response   [Skip link to API Response](https://developers.tap.company/docs/google-pay\#api-response)

A token\_id is expected in the API response, and it also contains the card information.

JSON

```rdmd-code lang-json theme-light

{
   "id": "tok_zMMQ40227330XHU6SXXXXX",
   "created": 1662449620276,
   "object": "token",
   "live_mode": false,
   "type": "GOOGLEPAY",
   "used": false,
   "card": {
       "id": "card_3snF4022733eqh56yL8E279",
       "object": "card",
       "funding": "CREDIT",
       "fingerprint": "FEAWi7M8%2BpIXbsraeWsHfuMOg2AeIpG5Pp2wkf4LHPU%3D",
       "brand": "VISA",
       "scheme": "VISA",
       "exp_month": 12,
       "exp_year": 2027,
       "last_four": "3478",
       "first_six": "489537"
   }
}

   "type": "googlepay"

}

```

* * *

### Charge the Token   [Skip link to Charge the Token](https://developers.tap.company/docs/google-pay\#charge-the-token)

Sample to control the source object in the [charge API](https://developers.tap.company/reference/create-a-charge): with "token\_id"

JSON

```rdmd-code lang-json theme-light

{
...
	"source": {
		"id": "tok_zMMQ40227330XHU6SXXXXX"
    }
"post": {
    "url": "https://webhook.site/fd8b0712-d70a-4280-8d6f-9f14407b3bbd"
     },
 "redirect": {
    "url": "https://customer.redirection_url"
     }
...
}

```

If 3Ds card, the API response would be INITIATED, and then it processes the further authentication.

If a Non-3Ds card is used in the google pay token, payment will be directly CAPTURED in the API response (Not Initiated).

Updated4 months ago

* * *

Did this page help you?

Yes

No