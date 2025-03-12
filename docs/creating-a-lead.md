Lead creation is the initial step in onboarding a merchant with Tap. It involves gathering essential information about the business or brand and setting the groundwork for the merchant account. This guide explains the parameters and the process involved in creating a lead, providing a smooth start to the onboarding journey.

## Sample Request   [Skip link to Sample Request](https://developers.tap.company/docs/creating-a-lead\#sample-request)

Please refer to [create lead API](https://developers.tap.company/reference/create-a-lead-v3)

## Lead Response   [Skip link to Lead Response](https://developers.tap.company/docs/creating-a-lead\#lead-response)

Here's a sample response to a successful lead creation request:

JSON

```rdmd-code lang-json theme-light
{
  "id": "led_xxxxxxxx",
  "status": "active",
  "created": 1739599571326,
  "object": "lead",
  "live_mode": false,
  "api_version": "v3",
  "feature_version": "v1",
  "country": "AE",
  "pending_action": "tap",
  "last_contact": 0,
  "brand": {
    "id": "brd_xxxxxxxxxx",
    "name": [\
      {\
        "lang": "en",\
        "text": "brandName"\
      }\
    ],
    "segment": {
      "type": {
        "code": "bus_xxxxxxx",
        "name": [\
          {\
            "lang": "ar",\
            "text": "جهة غير ربحية"\
          },\
          {\
            "lang": "en",\
            "text": "Non Profit"\
          }\
        ]
      },
      "team": {
        "code": "Small",
        "name": [\
          {\
            "lang": "ar",\
            "text": "3 إلى 10"\
          },\
          {\
            "lang": "en",\
            "text": "3 to 10"\
          }\
        ]
      }
    }
  },
  "users": [\
    {\
      "name": [\
        {\
          "title": "Mr.",\
          "first": "John",\
          "middle": "Bob",\
          "last": "Doe",\
          "lang": "en"\
        }\
      ],\
      "contact": {\
        "email": [\
          {\
            "address": "test@tap.com",\
            "primary": true\
          }\
        ],\
        "phone": [\
          {\
            "country_code": "971",\
            "number": "123456712",\
            "primary": true\
          }\
        ]\
      },\
      "identification": {\
        "number": "123456",\
        "country": "SA",\
        "type": "national_id",\
        "nationality": "SA"\
      },\
      "primary": true\
    }\
  ],
  "entity": {
    "legal_name": [\
      {\
        "lang": "en",\
        "text": "brandName"\
      }\
    ],
    "carries_a_license": true,
    "license": {
      "number": "1234567",
      "country": "AE",
      "type": "LLC"
    }
  },
  "wallet": {
    "currency": "AED",
    "linked_financial_account": {
      "bank": {
        "account": {
          "name": "John",
          "number": "123456789",
          "swift": "AEXXXXXX",
          "iban": "AE123456789012345"
        }
      }
    }
  },
  "post": {
    "url": "https://www.example.com/postURL"
  }
}

```

Updated21 days ago

* * *