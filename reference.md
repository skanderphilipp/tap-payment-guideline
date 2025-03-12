Tap APIs follow the RESTful architecture, returning all responses in JSON format.

There are two modes available for using Tap APIs: Test and Live. Each mode requires a different API key, which can be generated using the instructions provided in the "Generate API Key" section below.

> ## 📘  Integrations:
>
> 1. Looking to integrate your website, eCommerce store or mobile app with Tap Payment Gateway? Visit the Integrations guide to find the right integration method for you.
> 2. You can also accept payments without a website or app using goCollect app.
> 3. If you are looking for multi-vendor integration, contact the Tap Support Team with your requirements.

## API Authentication   [Skip link to API Authentication](https://developers.tap.company/reference/api-endpoint\#api-authentication)

To ensure secure authentication, Tap APIs use HTTP Token Authentication. You must provide your API key as the bearer in the Authorization header in the format "Authorization: Bearer YOUR\_SECRET\_KEY".

Please note that API requests made without proper authentication will fail.

> ## 🚧  Watch Out
>
> The Authorization header value should strictly adhere to the format mentioned above. Invalid formats will result in authentication failures.
>
> Few examples of invalid headers are:
>
> BASIC YOUR\_SECRET\_KEY
>
> basic YOUR\_SECRET\_KEY
>
> Basic "YOUR\_SECRET\_KEY"
>
> Basic $YOUR\_SECRET\_KEY

## API Credentials   [Skip link to API Credentials](https://developers.tap.company/reference/api-endpoint\#api-credentials)

To generate your Tap API key, follow these steps:

1. Log in to your Tap Dashboard using your credentials.
2. Navigate to goSell → API Credentials → Generate Key to view the secret keys for your desired mode.

> ## ❗️
>
> Do not share your API Key with anyone or on any public platforms. This can pose security threats for your Tap account.