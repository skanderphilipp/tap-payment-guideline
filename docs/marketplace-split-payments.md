As a Marketplace, you can split the transaction amount among one or more Destinations.

To split the transaction's amount, you'll need to add the `destinations` object to the transaction. You need to specify all the destinations, and the amount to be split for each one of them.

For example, you want to split a transaction of 20 KWD placed on your Marketplace as follows:

- 14 KWD goes to a Business with a `destination _id` **12345**
- 4 KWD goes to a delivery Business with a `destination _id` **56789**
- 2 KWD goes to your account as your Marketplace's commission.

> ## 📘
>
> The remaining amount of the transaction after the split, will goes directly to your Marketplace account.

The structure of the `destinations` object will be:

JSON

```rdmd-code lang-json theme-light
"destinations": {
    "destination": [\
      {\
        "id": "12345",\
        "amount": 14,\
        "currency": "KWD"\
      },\
      {\
        "id": "56789",\
        "amount": 4,\
        "currency": "KWD"\
      }\
    ]
  }

```

Transactions will reflect on the Marketplace account and the Businesses' account as transfers.

Updatedover 1 year ago

* * *