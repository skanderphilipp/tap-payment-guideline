# Overview   [Skip link to Overview](https://developers.tap.company/reference/destinations\#overview)

The "destinations" parameter can be used to transfer funds from one business to another within Tap. It allows the merchant to split a payment and send a portion of it to a different business, known as the destination business.

## The Destination Request   [Skip link to The Destination Request](https://developers.tap.company/reference/destinations\#the-destination-request)

JSON

```rdmd-code lang-json theme-light
{
  "display_name": "destplay",
  "business_id": "bus_Wntp1311012lnAh527153",
  "business_entity_id": "bsa_MxYZ1311012Viln527900",
  "brand_id": "brd_O4ZZ1311012Adr8527056",
  "branch_id": "brc_3Ud11311012OgEi527915",
  "bank_account": {
    "iban": "KWNBOKXXXXXXXXXXXXXXXXXXX"
  },
  "settlement_by": "Acquirer"
}

```

## The Destination Response   [Skip link to The Destination Response](https://developers.tap.company/reference/destinations\#the-destination-response)

JSON

```rdmd-code lang-json theme-light
{
  "id": "7691116100",
  "status": "Active",
  "created": 1573480740377,
  "object": "merchant",
  "live_mode": false,
  "api_version": "v2",
  "feature_version": "v2",
  "display_name": "mecplay",
  "business_id": "bus_jICJ50019921aGRG11Ja103291",
  "business_entity_id": "ent_QTFo56019921OSHN11Bv10y128",
  "brand_id": "brd_Uf1y59019921WrJI11h7107174",
  "branch_id": "brc_cemO2019922120F11jP10B63",
  "wallets": {
    "id": "wal_St480191659nfRg11aV108158",
    "status": "Active",
    "created": 1573480740158,
    "base_currency": "currency_YH3M1311012RFUc7214",
    "country": "country_as_QDVW13110125v1z7214",
    "settlement_by": "Acquirer",
    "primary_wallet": false
  },
  "bank_account": {
    "id": "bka_kKSB59191658lXvp11bY10h930",
    "status": "Active",
    "created": 1573480739930,
    "iban": "KWNBOKXXXXXXXXXXXXXXXXXXX"
  },
  "settlement_by": "Acquirer"
}

```