The structure of Tap's Marketplace model is built on Destinations, each Business under your Marketplace should have a `destination_id`. This page guides you through creating a `destination_id` by onboarding your Businesses.

> ## 📘
>
> For onboarding steps described on this page, you need to use the **Marketplace Keys** provided by Tap.

* * *

## Step 1: Uploading KYC documents   [Skip link to Step 1: Uploading KYC documents](https://developers.tap.company/docs/marketplace-onboarding-businesses\#step-1-uploading-kyc-documents)

Before you begin, you need to identify the Business's entity type. Tap supports two types of entities:

1. Corporate
2. Individual

You need to provide the required KYC documents, in order to get approval for your Business's account. The minimum KYC requirements depend on the entity type and the country of the Business. You are able to get the KYC requirements from your Account Manager.

For each document, you need to make a [File API request](https://developers.tap.company/docs/files). You'll receive a `file_id` for each file you upload, which you'll use in creating a business.

Create a File

```rdmd-code lang-curl theme-light

curl --location --request POST 'https://api.tap.company/v2/files' \
--header 'Authorization: Bearer sk_test_BPmcTgEfuK1dHslMaLGY42Ry' \
--header 'Content-Type: multipart/form-data' \
--header 'content-type: multipart/form-data; boundary=---011000010111000001101001' \
--form 'file=""' \
--form 'purpose="identity_document"' \
--form 'title="Commercial License "' \
--form 'expires_at="1913743462"' \
--form 'file_link_create="true"'

```

Response

```rdmd-code lang-json theme-light

{
  "id": "file_641212279714869248",
  "object": "file",
  "live_mode": false,
  "api_version": "1.0",
  "feature_version": "1.0",
  "created": 1572947320,
  "filename": "8801760e0a28ae2105e4ada503e30b8c.jpg",
  "purpose": "identity_document",
  "size": 346827,
  "title": "test",
  "type": "jpg",
  "url": "/files/file_641212279714869248",
  "links": [\
    {\
      "id": "link_641212281036075008",\
      "object": "file_link",\
      "live_mode": true,\
      "api_version": "1.0",\
      "feature_version": "1.0",\
      "created": 1572947320,\
      "expired": false,\
      "expires_at": 1234567,\
      "metadata": {\
        "key1": "value1",\
        "key2": "value2"\
      },\
      "url": "/links/fl_test_641212281036075009"\
    }\
  ]
}

```

* * *

## Step 2: Creating a Business   [Skip link to Step 2: Creating a Business](https://developers.tap.company/docs/marketplace-onboarding-businesses\#step-2-creating-a-business)

After uploading all KYC documents, you need to make a [business](https://developers.tap.company/docs/business) `request in order to generate a` destination \_id\` for your Business.

- Specify the `type` based on your Business entity type. If it is a licensed business set `type` to **"corp"**, otherwise set it to **"indv"**.
- `legal_name` should be the same as the Business name on the commercial registration or license.
- Specify the sector of your Business, you can choose the suitable sector after connecting with your Account Manager.
- In the `images` object, specify the `file_id` you received in the first step.

JSON

```rdmd-code lang-json theme-light

"images": [\
    "file_656840219076980736",\
    "file_656840219076980736"\
]

```

Create a Business

```rdmd-code lang-curl theme-light

curl --request POST \
  --url https://api.tap.company/v2/business \
  --header 'authorization: Bearer sk_test_BPmcTgEfuK1dHslMaLGY42Ry' \
  --header 'content-type: application/json' \
  --data '
  {
  "name": {
    "en": "Flexwares",
    "ar": " تاپ للدفع"
  },
  "type": "corp",
  "entity": {
    "legal_name": {
      "en": "Flexwares",
      "ar": "فلكس ويرزدفع"
    },
    "is_licensed": true,
    "license_number": "2134342SE",
    "not_for_profit": false,
    "country": "KW",
    "settlement_by": "Acquirer",
    "documents": [\
      {\
        "type": "Commercial Registration",\
        "number": "1234567890",\
        "issuing_country": "SA",\
        "issuing_date": "2019-07-09",\
        "expiry_date": "2021-07-09",\
        "images": [\
          "file_656840219076980736"\
        ]\
      },\
      {\
        "type": "Commercial license",\
        "number": "1234567890",\
        "issuing_country": "SA",\
        "issuing_date": "2019-07-09",\
        "expiry_date": "2021-07-09",\
        "images": [\
          "file_656840219076980736"\
        ]\
      },\
      {\
        "type": "Trademark Document",\
        "number": "1234567890",\
        "issuing_country": "SA",\
        "issuing_date": "2019-07-09",\
        "expiry_date": "2021-07-09",\
        "images": [\
          "file_656840219076980736"\
        ],\
        "files": [\
          "file_656840219076980736"\
        ]\
      }\
    ],
    "bank_account": {
      "iban": "INBNK00045545555555555555"
    }
  },
  "contact_person": {
    "name": {
      "title": "Mr",
      "first": "Muhammed",
      "middle": "L",
      "last": "Fazan"
    },
    "contact_info": {
      "primary": {
        "email": "mfaz@fexwares.company",
        "phone": {
          "country_code": "965",
          "number": "900000"
        }
      }
    },
    "is_authorized": true,
    "identification": [\
      {\
        "type": "Identity Card",\
        "issuing_country": "SA",\
        "issuing_date": "2019-07-09",\
        "expiry_date": "2020-07-09",\
        "images": [\
          "file_656840219076980736",\
          "file_656840219076980736"\
        ]\
      },\
      {\
        "type": "Passport",\
        "issuing_country": "SA",\
        "issuing_date": "2012-07-09",\
        "expiry_date": "2022-07-09",\
        "images": [\
          "file_656840219076980736",\
          "file_656840219076980736"\
        ]\
      }\
    ]
  },
  "brands": [\
    {\
      "name": {\
        "en": "flexwareTip",\
        "ar": "فلكس ويرز ت"\
      },\
      "sector": [\
        "Sec 1",\
        "Sec 2"\
      ],\
      "website": "https://www.flexwares.company/",\
      "social": [\
        "https://twitter.com/flexwares",\
        "https://www.linkedin.com/company/flexwares/"\
      ],\
      "logo": "file_656840219076980736",\
      "content": {\
        "tag_line": {\
          "en": "Walk free",\
          "ar": "المشي الحرتروني",\
          "zh": "自由走"\
        },\
        "about": {\
          "en": "The Flexwares is a shoe store company selling awsome and long lasting shoes. Come and check out our products online. ",\
          "ar": "هذه هي شركة لبيع الأحذية تبيع أحذية رهيبة وطويلة الأمد. تعال وتحقق من منتجاتنا عبر الإنتر",\
          "zh": "这是一家鞋店公司，销售长久耐用的鞋子。快来在线查看我们的产品。"\
        }\
      }\
    }\
  ],
  "post": {
    "url": "http://flexwares.company/post_url"
  },
  "metadata": {
    "mtd": "metadata"
  }
}
  '

```

Response

```rdmd-code lang-json theme-light

{
  "id": "bus_cGTwK2120921MnyG22ps0o754",
  "status": "Active",
  "created": 1579684891457,
  "object": "business",

  ...

  "name": {
    "ar": " تاپ للدفع",
    "en": "Flexwares"
  },
  "type": "corp",

  ...

  "entity": {
    "id": "ent_cnTwK2120921iX7822E20W754",
    "status": "Active",
    "created": 1579684888483,
    "legal_name": {
      "ar": "فلكس ويرزدفع",
      "en": "Flexwares"
    },

  ...

	}

  ...

  "destination_id": "8302217348"
}

```

In the response of `\business` request, you will receive a `destination_id`. Save the `destination_id`, this is the ID you will use to process the Business's transactions.

* * *

## Business account approval   [Skip link to Business account approval](https://developers.tap.company/docs/marketplace-onboarding-businesses\#business-account-approval)

The KYC verification process will be carried out by our team prior to the account approval. If any required KYC document is missing, or more information is need, our team will reach out to you.

* * *

## See also   [Skip link to See also](https://developers.tap.company/docs/marketplace-onboarding-businesses\#see-also)

[**Split Payments** \\
Split the amount at the time of the transaction](https://developers.tap.company/docs/split-payments)

[**After Payments**](https://developers.tap.company/docs/)

Updatedover 1 year ago

* * *

Did this page help you?

Yes

No