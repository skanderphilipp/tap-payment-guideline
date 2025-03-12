## Overview   [Skip link to Overview](https://developers.tap.company/reference/getting-started-with-your-api-10\#overview)

To create merchants for your business, you must provide information about the linked entity, brand, and branch. If the wallet belongs to the same business and entity, the merchant can be linked to an existing wallet. Otherwise, you can create a new wallet for each merchant and link it with a bank account.

## Merchant Request Example   [Skip link to Merchant Request Example](https://developers.tap.company/reference/getting-started-with-your-api-10\#merchant-request-example)

JSON

```rdmd-code lang-json theme-light
{
	"display_name": "ABC",
	"business_id": "bus_qPUaS82Ejz412id3z592",
	"business_entity_id": "ent_FDUaS82310VX12Zu3z592",
	"charge_currenices": [\
		"SAR"\
	],
	"country":"SA",
	"email":"example@company.com"
}

```

## Merchant Response Example   [Skip link to Merchant Response Example](https://developers.tap.company/reference/getting-started-with-your-api-10\#merchant-response-example)

JSON

```rdmd-code lang-json theme-light
{
  "id": "533990",
  "status": "ACTIVE",
  "created": 1572954294744,
  "object": "Merchant",
  "live_mode": false,
  "api_version": "v2",
  "feature_version": "v2",
  "display_name": "merchantplasy",
  "business_id": "bus_kP981311012y2GD527203",
  "business_entity_id": "bsa_4sqU1311012pvDb527869",
  "brand_id": "brd_a0n41311012JKs0527019",
  "charge_currenices": [\
    "KWD"\
  ],
  "wallets": {
    "id": "wal_8Cfq1311012QoDY527801",
    "status": "ACTIVE",
    "created": 1572954119801,
    "base_currency": "currency_YH3M1311012RFUc7214",
    "country": "country_as_QDVW13110125v1z7214",
    "settlement_by": "Acquirer",
    "bank_account": {
      "id": "bka_dz441311012kNsf527869",
      "status": "ACTIVE",
      "created": 1572954118869,
      "iban": "KWNBOKXXXXXXXXXXXXXXXXXXX"
    }
  },
  "settlement_by": "Acquirer"
}

```