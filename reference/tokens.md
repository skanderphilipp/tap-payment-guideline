## Overview   [Skip link to Overview](https://developers.tap.company/reference/tokens\#overview)

Tokenization is a secure process that Tap uses to collect sensitive card or personally identifiable information (PII) from customers. It returns a `token_id` representing the information collected to be used on your server.

To ensure PCI compliance, it's recommended that you use Tap's recommended [payments integrations](https://developers.tap.company/docs/) to perform the tokenization process client-side. This way, no sensitive card data is stored on your server.

If you can't use client-side tokenization, you can still create tokens using the API, but it requires either your publishable or secret API key. In this case, you are responsible for any PCI compliance required, and it's important to keep your secret API key safe.

Remember that tokens can't be stored or used more than once. To store cards for future use, you can create Customer objects and save the cards on the customer. You can then create a new token from the saved card to charge again.

**Card Token**

You can use the Create a Token API to pass the credit card information to create the token.

> ## 📘
>
> It's important to note that for access to Token API, you need to submit the Merchant's PCI Compliance Certificate to Tap. You can create the token, by using our [Checkout Card SDK](https://ixlcfimy.readme.io/docs/card-js-library) without PCI compliance.

**Encrypted Card Token**

To create a token, you can pass the encrypted card information through this API. However, please note that a PCI compliance certificate is required to access this endpoint. To obtain access, please contact the Tap Support Team.

**Saved Card Token**

Before charging or authorizing a saved card, you must first create a token. To do so, you will need to include the `card_id` and `customer_id` in the Token API request.

**Usage of Token**

You can use the `token_id` generated from the Token API request in both the [Charge](https://ixlcfimy.readme.io/reference/create-a-charge) or [Authorize](https://ixlcfimy.readme.io/reference/create-an-authorize) API requests. Additionally, you can save the card for future charges or authorizations by using the `token_id` in the Create Card API request.

## Token Request Example   [Skip link to Token Request Example](https://developers.tap.company/reference/tokens\#token-request-example)

To create a token, you'll need to use the [Create a Token (Card)](https://developers.tap.company/reference/create-a-token) endpoint.

JSON

```rdmd-code lang-json theme-light
{
  "card": {
    "number": 5123450000000008,
    "exp_month": 7,
    "exp_year": 2022,
    "cvc": 100,
    "name": "test user",
    "address": {
      "country": "Kuwait",
      "line1": "Salmiya, 21",
      "city": "Kuwait city",
      "street": "Salim",
      "avenue": "Gulf"
    }
  },
  "client_ip": "192.168.1.20"
}

```

## Token Response Example   [Skip link to Token Response Example](https://developers.tap.company/reference/tokens\#token-response-example)

JSON

```rdmd-code lang-json theme-light
{
    "id": "tok_CWqLQ1311012WPdW527633",
    "object": "token",
    "client_ip": "192.168.1.20",
    "created": 1612876885622,
    "live_mode": false,
    "type": "CARD",
    "used": false,
    "card": {
        "id": "card_C9vyl1311012RofB527622",
        "object": "card",
        "address": {
            "country": "Kuwait",
            "city": "Kuwait city",
            "avenue": "Gulf",
            "street": "Salim",
            "line1": "Salmiya, 21"
        },
        "funding": "CREDIT",
        "fingerprint": "Q%2FcqTEPF%2FZuM7IaWN%2F7QR8kjZsJ1zzAdrmAhTXaBTOk%3D",
        "brand": "VISA",
        "scheme": "VISA",
        "exp_month": 12,
        "exp_year": 25,
        "last_four": "2393",
        "first_six": "479045",
        "name": "test user",
        "issuer": {
            "bank": "KUWAIT FINANCE HOUSE",
            "country": "KW",
            "id": ""
        }
    }
}

```