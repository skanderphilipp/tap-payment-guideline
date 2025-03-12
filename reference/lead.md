The Lead API facilitates the creation of leads and the merchant onboarding process by enabling the efficient submission and validation of essential KYC details. By using this API, businesses can efficiently manage and automate the initial steps of onboarding new merchants or clients.

## Benefits for Businesses:   [Skip link to Benefits for Businesses:](https://developers.tap.company/reference/lead\#benefits-for-businesses)

- **Improved Onboarding Speed:** By streamlining the lead creation and KYC submission processes, businesses can onboard merchants more quickly, reducing the time to revenue.
- **Regulatory Compliance:** The API ensures that all KYC information is collected in accordance with regulatory requirements, helping businesses avoid penalties and legal issues.
- **Scalability:** The Lead API can handle large volumes of leads and onboarding requests, making it suitable for businesses of all sizes.

## Key Considerations:   [Skip link to Key Considerations:](https://developers.tap.company/reference/lead\#key-considerations)

- **Unique entity Information:** Each lead should be associated with a unique legal entity
- **Distinct Email Addresses:** Please ensure to provide a unique email address for each lead.
- **Separate Brand details:** When onboarding multiple merchants or clients, it's essential to provide unique brand information for each submission.
- **Mandatory Field:** Treat the National ID as a mandatory field for all Saudi merchants. The Lead API submission should be configured to reject any submission for Saudi merchants that lacks a valid National ID. This helps in maintaining compliance with local regulations and prevents incomplete data submissions.

## Segment Keys   [Skip link to Segment Keys](https://developers.tap.company/reference/lead\#segment-keys)

Tap will generate keys (Public Key - Secret Key) for your segment:

- Segment must use the secret key in case of any direct API call.
- Segment must use the public key in the integration with connect SDK.

## Files API   [Skip link to Files API](https://developers.tap.company/reference/lead\#files-api)

Before passing any files to the Lead API, you must create them using the TAP [Files API.](https://developers.tap.company/reference/files) The Files API enables you to upload and manage the files associated with the lead.

## Lead API   [Skip link to Lead API](https://developers.tap.company/reference/lead\#lead-api)

Once you have the segment keys and any required files in place, you can use the Lead API to send the merchant information and initiate the onboarding process.

POST [https://api.tap.company/v3/connect/lead](https://api.tap.company/v3/connect/lead)

### Request   [Skip link to Request](https://developers.tap.company/reference/lead\#request)

cURL

```rdmd-code lang-curl theme-light
curl --request POST \
  --url https://api.tap.company/v3/connect/lead \
  --header 'Authorization: Bearer sk_test_xxxx' \
  --header 'Content-Type: application/json' \
  --data '{
   "brand":{
      "name":{
         "en":"merchantNameEn",
         "ar":"merchantNameAr"
      },
      "sector":[\
         "telecom",\
         "finance"\
      ],
      "logo":"file_xxxx",
      "channel_services":[\
         {\
            "channel":"website",\
            "address":"https://www.website.company"\
         },\
         {\
            "channel":"twitter",\
            "address":"https://twitter.com/xxxx"\
         },\
         {\
            "channel":"instagram",\
            "address":"https://www.instagram.com/company/xxxx"\
         },\
         {\
            "channel":"ios",\
            "address":"IOS App Name"\
         },\
         {\
            "channel":"android",\
            "address":"Android App Name"\
         }\
      ],
      "operations":{
         "start_date":"2021-10-10",
         "sales":{
            "period":"monthly",
            "range":{
               "from":"10000",
               "to":"80000"
            },
            "currency":"SAR"
         },
         "customer_base":{
            "period":"monthly",
            "range":{
               "from":"10000",
               "to":"20000"
            },
            "locations":[\
               "local",\
               "regional"\
            ]
         }
      },
      "terms":[\
         {\
            "term":"general",\
            "agree":true\
         },\
         {\
            "term":"chargeback",\
            "agree":true\
         },\
         {\
            "term":"refund",\
            "agree":true\
         }\
      ]
   },
   "entity":{
      "country":"SA",
      "is_licensed":true,
      "license":{
         "number":"xxxx",
         "references":[\
            {\
               "reference":"xxxx",\
               "type":"unified_number"\
            }\
         ],
         "country":"SA",
         "city":"Riyadh",
         "type":"commercial_registration",
         "issuing_date":"2024-04-01",
         "expiry_date":"2024-04-01",
         "documents":[\
            {\
               "type":"commercial_registration",\
               "number":"xxxx",\
               "issuing_country":"SA",\
               "issuing_date":"2024-04-01",\
               "expiry_date":"2024-04-01",\
               "images":[\
                  "file_xxxx"\
               ]\
            },\
            {\
               "type":"memorandum_of_association",\
               "number":"1243577890",\
               "issuing_country":"SA",\
               "issuing_date":"2019-07-09",\
               "expiry_date":"2021-07-09",\
               "images":[\
                  "file_xxxx"\
               ]\
            }\
         ]
      },
      "tax":{
         "number":"xxxx",
         "issuing_date":"2023-01-20",
         "expiry_date":"2023-01-20",
         "documents":[\
            {\
               "type":"TAX Document",\
               "number":"xxxx",\
               "issuing_country":"SA",\
               "issuing_date":"2019-07-09",\
               "expiry_date":"2021-07-09",\
               "images":[\
                  "file_xxxx"\
               ]\
            }\
         ]
      }
   },
   "wallet":{
      "bank":{
         "name":"Ryiadh Bank",
         "account":{
            "name":"ABC",
            "number":"77777777777",
            "swift":"77777777777",
            "iban":"SA0xxxx59584"
         },
         "documents":[\
            {\
               "type":"Bank Statement",\
               "number":"xxxx",\
               "issuing_country":"SA",\
               "issuing_date":"2019-07-09",\
               "images":[\
                  "file_xxxx"\
               ]\
            }\
         ]
      }
   },
   "user":{
      "name":{
         "lang":"en",
         "title":"Mr",
         "first":"John",
         "middle":"Bob",
         "last":"Doe"
      },
      "email":[\
         {\
            "type":"WORK",\
            "address":"user@abc.com",\
            "primary":true\
         }\
      ],
      "phone":[\
         {\
            "type":"WORK",\
            "country_code":"966",\
            "number":"xxxx",\
            "primary":true\
         }\
      ],
      "address":[\
         {\
            "type":"HOME",\
            "line1":"line1",\
            "line2":"line2",\
            "line3":"line3",\
            "line4":"line4",\
            "avenue":"",\
            "street":"",\
            "building":"",\
            "apartment":"",\
            "country":"SA",\
            "state":"Saudi",\
            "city":"Riyadh",\
            "area":"",\
            "zip_code":"30003",\
            "postal_code":""\
         }\
      ],
      "birth":{
         "city":"Riyadh",
         "country":"SA"
      },
      "nationality":"SA",
      "identification":{
         "number":"1087078604",
         "type":"national_id",
         "issuer":"SA"
      },
      "primary":true
   },
   "post":{
      "url":"http://example.com/postUrl"
   },
   "metadata":{
      "mtd":"metadata"
   }
}'

```

### Response   [Skip link to Response](https://developers.tap.company/reference/lead\#response)

Same request data sent will be available in the response along with the lead ID

JSON

```rdmd-code lang-json theme-light
{
	"id": "led_xxxx",
	"brand": {
		"name": {
			"en": "merchantNameEn",
			"ar": "merchantNameAr"
		},
		"sector": [\
			"telecom",\
			"finance"\
		],
		"logo": "file_xxxx",
		"channel_services": [\
			{\
				"channel": "website",\
				"address": "https://www.website.company/"\
			},\
			{\
				"channel": "twitter",\
				"address": "https://twitter.com/xxxx"\
			},\
			{\
				"channel": "instagram",\
				"address": "https://www.instagram.com/company/xxxx"\
			},\
			{\
				"channel": "ios",\
				"address": "IOS App Name"\
			},\
			{\
				"channel": "android",\
				"address": "Android App Name"\
			}\
		],
		"operations": {
			"start_date": "2021-10-10",
			"sales": {
				"period": "monthly",
				"range": {
					"from": "10000",
					"to": "80000"
				},
				"currency": "SAR"
			},
			"customer_base": {
				"period": "monthly",
				"range": {
					"from": "10000",
					"to": "20000"
				},
				"locations": [\
					"local",\
					"regional"\
				]
			}
		},
		"terms": [\
			{\
				"term": "general",\
				"agree": true\
			},\
			{\
				"term": "chargeback",\
				"agree": true\
			},\
			{\
				"term": "refund",\
				"agree": true\
			}\
		]
	},
	"entity": {
		"country": "SA",
		"is_licensed": true,
		"license": {
			"number": "xxxx",
			"references": [\
				{\
					"reference": "xxxx",\
					"type": "unified_number"\
				}\
			],
			"country": "SA",
			"city": "Riyadh",
			"type": "commercial_registration",
			"issuing_date": "2024-04-01",
			"expiry_date": "2024-04-01",
			"documents": [\
				{\
					"type": "commercial_registration",\
					"number": "1010951143",\
					"issuing_country": "SA",\
					"issuing_date": "2024-04-01",\
					"expiry_date": "2024-04-01",\
					"images": [\
						"file_xxxx"\
					]\
				},\
				{\
					"type": "memorandum_of_association",\
					"number": "1243577890",\
					"issuing_country": "SA",\
					"issuing_date": "2019-07-09",\
					"expiry_date": "2021-07-09",\
					"images": [\
						"file_643320430437906816"\
					]\
				}\
			]
		},
		"tax": {
			"number": "12435778912",
			"issuing_date": "2023-01-20",
			"expiry_date": "2023-01-20",
			"documents": [\
				{\
					"type": "TAX Document",\
					"number": "12435778912",\
					"issuing_country": "SA",\
					"issuing_date": "2019-07-09",\
					"expiry_date": "2021-07-09",\
					"images": [\
						"file_xxxx"\
					]\
				}\
			]
		}
	},
	"wallet": {
		"bank": {
			"name": "Ryiadh Bank",
			"account": {
				"name": "ABC",
				"number": "77777777777",
				"swift": "77777777777",
				"iban": "SA04xxxx59584"
			},
			"documents": [\
				{\
					"type": "Bank Statement",\
					"number": "9876573221",\
					"issuing_country": "SA",\
					"issuing_date": "2019-07-09",\
					"images": [\
						"file_xxxx"\
					]\
				}\
			]
		}
	},
	"user": {
		"name": {
			"lang": "en",
			"title": "Mr",
			"first": "John",
			"middle": "Bob",
			"last": "Doe"
		},
		"email": [\
			{\
				"type": "WORK",\
				"address": "user@abc.com",\
				"primary": true\
			}\
		],
		"phone": [\
			{\
				"type": "WORK",\
				"country_code": "966",\
				"number": "5987657",\
				"primary": true\
			}\
		],
		"address": [\
			{\
				"type": "HOME",\
				"line1": "line1",\
				"line2": "line2",\
				"line3": "line3",\
				"line4": "line4",\
				"avenue": "",\
				"street": "",\
				"building": "",\
				"apartment": "",\
				"country": "SA",\
				"state": "Saudi",\
				"city": "Riyadh",\
				"area": "",\
				"zip_code": "30003",\
				"postal_code": ""\
			}\
		],
		"birth": {
			"city": "Riyadh",
			"country": "SA"
		},
		"nationality": "SA",
		"identification": {
			"number": "xxxx",
			"type": "national_id",
			"issuer": "SA"
		},
		"primary": true
	},
	"post": {
		"url": "http://example.com/postUrl"
	},
	"metadata": {
		"mtd": "metadata"
	},
	"reference_lead_id": "xxxx"
}

```