## Overview   [Skip link to Overview](https://developers.tap.company/reference/cards-2\#overview)

You can save multiple cards under a customer to charge at a later date for quicker checkouts and a seamless payment experience for your customers. Once cards are saved, you can retrieve them for a customer, update or delete them, and use them for future charges. This feature eliminates the need for customers to enter their payment details every time they make a purchase, enhancing their overall shopping experience.

> ## 📘  Save Card Feature
>
> To save cards for a `customer.id`, the Save Card feature has to be activated for the Merchant Account. Contact your account manager to enable the Save Card feature.

**Usage of Saved Card**

A saved `card.id`, cannot be directly used in the [Create a Charge](https://developers.tap.company/reference/create-a-charge) or [Create an Authorize](https://developers.tap.company/reference/create-an-authorize) request. First, you need to create the `token.id` for this saved `card.id`, and then use this `token.id` to initiate a transaction.

## Card Request Example   [Skip link to Card Request Example](https://developers.tap.company/reference/cards-2\#card-request-example)

The Token ID and Customer ID are both required to successfully save a card.

You can use our JS library to create the token without being PCI compliant.

JSON

```rdmd-code lang-json theme-light
{
    "id": "card_C9vyl1311012RofB527622",
    "object": "card",
    "address": {
        "country": "Kuwait",
        "city": "Kuwait city",
        "avenue": "Gulf",
        "street": "Salim",
        "line1": "Salmiya, 21"
    },
    "customer": "cus_w4P24120191640b9N91106702",
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

```

## Card Response Example   [Skip link to Card Response Example](https://developers.tap.company/reference/cards-2\#card-response-example)

Card response will return the Card ID. you can use this Card ID for future charges or authorizations.

> ## 📘
>
> If you want to use the saved card in a charge or authorize request API, you need to create the token first and pass the Token ID in the source object. Saved Card ID will not be accepted in a charge or authorize request.

JSON

```rdmd-code lang-json theme-light
{
  "id": "card_amo4Nm9tMnY1N2hqbjQ4N2ltNWU",
  "object": "card",
  "last4": "4242",
  "exp_month": 12,
  "exp_year": 20,
  "brand": "VISA",
  "name": "TEST",
  "address_line1": "",
  "address_country": "",
  "address_city": "",
  "phone_number": "",
  "address_zip": 0
}

```