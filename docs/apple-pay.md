Apple Pay is a digital wallet and mobile payment service developed by Apple Inc. It allows users to make secure and convenient payments using their Apple devices.

Apple Pay should be enabled from the _tap_ side before using it on the Merchant side.

> ## 🚧  It's currently supported in UAE, KSA, KW, QA, and Bahrain with currencies AED, SAR, KWD, QAR, and BHD respectively, and USD is an addition. We keep adding more countries and currencies. For more updates, please keep in touch with TAP support teams

# Integration Channel   [Skip link to Integration Channel](https://developers.tap.company/docs/apple-pay\#integration-channel)

When it comes to Apple Pay payment method integration, the first thing to sort out is the channel in which you are integrating: Web or Mobile.

with Apple pay

Apple Pay integration depends on the UI mode chosen by the merchant.

## Apple Pay Button on your Website   [Skip link to Apple Pay Button on your Website](https://developers.tap.company/docs/apple-pay\#apple-pay-button-on-your-website)

iFrame and popup windows do not support the Apple Pay option. So, merchants can add a separate button for Apple Pay on the merchant's checkout page for the customers' choice.

- Which can be integrated using backend API/s. [API's flow](https://developers.tap.company/docs/apple-pay-token)
- Or use our built-in SDK for button integration [SDK flow](https://developers.tap.company/docs/web-applepay-sdk)

## Apple Pay Button on your Mob application   [Skip link to Apple Pay Button on your Mob application](https://developers.tap.company/docs/apple-pay\#apple-pay-button-on-your-mob-application)

You can integrate Apple Pay button on your mobile application using the below options

- Using backend API/s. [API's flow](https://developers.tap.company/docs/apple-pay-token)
- Or use our built-in Apple Pay iOS kit for button integration [Apple Pay iOS kit](https://github.com/Tap-Payments/TapApplePayKit-iOS)

## Apple Pay Button on Tap Hosted Web Checkout page   [Skip link to Apple Pay Button on Tap Hosted Web Checkout page](https://developers.tap.company/docs/apple-pay\#apple-pay-button-on-tap-hosted-web-checkout-page)

It doesn't require any configuration from the merchant's side. The Apple Pay payment option will appear on our hosted payment page automatically. Customers can choose and make a payment.

> ## 🚧  For a better user experience, we recommend integrating Apple Pay button on your Web channel

## Apple Pay Button on Tap Hosted Mob Checkout page   [Skip link to Apple Pay Button on Tap Hosted Mob Checkout page](https://developers.tap.company/docs/apple-pay\#apple-pay-button-on-tap-hosted-mob-checkout-page)

Apple Pay button is available through our mobile SDKs (PURCHASE mode)

Check out our native iOS SDK [Here](https://github.com/Tap-Payments/goSellSDK-iOS)

Mapping with Apple Pay, follow the steps [Here](https://github.com/Tap-Payments/goSellSDK-iOS#apple-pay)

> ## 🚧  For a better user experience, we recommend integrating Apple Pay button on your Mob channel either using Apple Pay iOS kit provided by tap or by using direction integration with Apple Pay (and using tap token API)

Updated10 months ago

* * *

- [Apple Pay SDK](https://developers.tap.company/docs/apple-pay-web-sdk)