Before using the save cards feature, ensure that it is enabled on your account. If you don't have it enabled already, just contact our customer support team and they can enable it for you.

1. To save a card, create an Authorize, Charge, or Verify Card request and set the 3D Secure and save\_card flags to true in the request body.

JSON request

```rdmd-code lang-json theme-light
{
  ...
  "threeDSecure": true,
  "save_card": true,
  ...
}

```

2. The transaction response will include the card ID, which contains card information such as the brand name, first six and last four digits of the card, and more.

Transaction Response

```rdmd-code lang-text theme-light
{
...
"card": {
    "id": "card_IQPXL3xxxxxxxxxxxxxxx",
    "object": "card",
    "first_six": "450875",
    "brand": "VISA",
    "last_four": "1019"
  },
...
}

```

( **Note:** You will not receive the card ID if the save cards feature is not enabled. The response through 'post\_url' or 'redirect\_url' contains the same details.)

3. Once you have the card ID, you can use it for various purposes, including charging returning customers, creating subscriptions, generating fresh tokens, and more.

Updatedover 1 year ago

* * *