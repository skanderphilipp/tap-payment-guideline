## Overview   [Skip link to Overview](https://developers.tap.company/reference/business\#overview)

The business API is used to create a business account on Tap. With these APIs, you can directly onboard the business and upload required documents such as ID, Commercial Registration license, and Logo.

**Business KYC:**

The following documents and fields are required:

- Identity document (Civil ID or Passport)
- Commercial Registration License
- Business Logo

Please note that all required fields on the documents must be filled out:

- Identity Document: Issue date, expiry date, issuing country
- Commercial Registration License: Issue Date, expiry date, commercial registration number
- Logo: File size cannot exceed 1 MB.

> ## 📘
>
> When uploading the documents, please attach the File\_ID reference to each document type.

Banking Information:

- IBAN (34 digits)
- Swift code (8 digits)
- Account number (16 digits)

Business Owner/Authorized Signatory KYC:

- Name of Owner/Authorized Signatory (First Name, Middle Name, Last Name)
- Contact Details (Country Code and Mobile Number)
- Email Address (of the Business Owner)

Authorization of Business:

- Any document to verify the authorized signatory / owner of the business.

Business information:

- Sector (e.g., Fashion, Food, Tourism)
- Website
- Social Media Pages (e.g., LinkedIn, Instagram, Facebook)
- About (Miscellaneous Business Information)

## The Business Request Example   [Skip link to The Business Request Example](https://developers.tap.company/reference/business\#the-business-request-example)

JSON

```rdmd-code lang-json theme-light
{
	"name": {
		"en": "Flexwares",
		"ar": "فلكس ويرزدفع"
	},
	"type": "corp",
	"entity": {
		"legal_name": {
			"en": "Flexwares",
			"ar": "فلكس ويرزدفع"
		},
		"is_licensed": "true",
		"license": {
			"type": "Commercial Registration",
			"number": "2134342SE"
		},
		"not_for_profit": false,
		"country": "KW",
		"tax_number": "1234567890",
		"documents": [\
			{\
				"type": "Commercial Registration",\
				"number": "1234567890",\
				"issuing_country": "KW",\
				"issuing_date": "2019-07-09",\
				"expiry_date": "2021-07-09",\
				"files": [\
					"file_984450183956131840"\
				]\
			}\
		],
		"bank_account": {
			"iban": "INBNK00045545555555555555",
			"swift_code": "SWFT12345678909836435647",
			"account_number": "DFGHGFVB876215bsdjhkn"
		},
		"billing_address": {
			"recipient_name": "test",
			"address_1": "Address one",
			"address_2": "Address two",
			"po_box": "0000",
			"district": "Salmiya",
			"city": "Hawally",
			"state": "Kuwait",
			"zip_code": "30003",
			"country": "KW"
		}
	},
	"contact_person": {
		"name": {
			"title": "Mr",
			"first": "Test",
			"middle": "Test",
			"last": "Test"
		},
		"contact_info": {
			"primary": {
				"email": "test@test.com",
				"phone": {
					"country_code": "965",
					"number": "51234567"
				}
			}
		},
		"nationality": "KW",
		"date_of_birth": "2000-01-02",
		"is_authorized": true,
		"authorization": {
			"name": {
				"title": "Mr",
				"first": "Test",
				"middle": "Test",
				"last": "Test"
			},
			"type": "identity_document",
			"issuing_country": "KW",
			"issuing_date": "2012-03-03",
			"expiry_date": "2020-03-03",
			"files": [\
				"file_984450183956131840"\
			]
		},
		"identification": [\
			{\
				"name": {\
					"title": "Mr",\
					"first": "Test",\
					"middle": "Test",\
					"last": "Test"\
				},\
				"type": "identity_document",\
				"number": "123456789",\
				"issuing_country": "KW",\
				"issuing_date": "2012-02-02",\
				"expiry_date": "2012-02-02",\
				"files": [\
					"file_984450183956131840"\
				]\
			}\
		]
	},
	"brands": [\
		{\
			"name": {\
				"en": "Flexwares",\
				"ar": "فلكس ويرزدفع"\
			},\
			"sector": [\
				"Others"\
			],\
			"website": "https://www.flexwares.company/",\
			"social": [\
				"https://add.cc"\
			],\
			"logo": "file_984450183956131840",\
			"content": {\
				"tag_line": {\
					"en": "Walk free",\
					"ar": "المشي الحرتروني",\
					"zh": "自由走"\
				},\
				"about": {\
					"en": "The Flexwares is a shoe store company selling awsome and long lasting shoes. Come and check out our products online.",\
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

```

## The Business Response Example   [Skip link to The Business Response Example](https://developers.tap.company/reference/business\#the-business-response-example)

JSON

```rdmd-code lang-json theme-light
{
    "id": "bus_SdTwK2822815pAo319Mi5H407",
    "status": "Active",
    "created": 1655626538781,
    "object": "business",
    "live_mode": false,
    "api_version": "v2",
    "feature_version": "v1",
    "name": {
        "ar": "فلكس ويرزدفع",
        "en": "Flexwares"
    },
    "type": "corp",
    "brands": [\
        {\
            "id": "brd_u5TwK3422815FcYJ19zE5D771",\
            "status": "Active",\
            "created": 1655626534771,\
            "name": {\
                "ar": "فلكس ويرزدفع",\
                "en": "Flexwares"\
            },\
            "sector": [\
                "Others"\
            ],\
            "logo": "file_984450183956131840",\
            "content": {\
                "tag_line": {\
                    "ar": "المشي الحرتروني",\
                    "en": "Walk free",\
                    "zh": "自由走"\
                },\
                "about": {\
                    "ar": "هذه هي شركة لبيع الأحذية تبيع أحذية رهيبة وطويلة الأمد. تعال وتحقق من منتجاتنا عبر الإنتر",\
                    "en": "The Flexwares is a shoe store company selling awsome and long lasting shoes. Come and check out our products online.",\
                    "zh": "这是一家鞋店公司，销售长久耐用的鞋子。快来在线查看我们的产品。"\
                }\
            },\
            "website": "https://www.flexwares.company/",\
            "social": [\
                "https://add.cc"\
            ]\
        }\
    ],
    "entity": {
        "id": "ent_NpTwK2822815gW2C19rt5d407",
        "status": "Active",
        "created": 1655626532930,
        "legal_name": {
            "ar": "فلكس ويرزدفع",
            "en": "Flexwares"
        },
        "license": {
            "type": "Commercial Registration",
            "number": "2134342SE"
        },
        "country": "KW",
        "documents": [\
            {\
                "id": "doc_YfTwK3222815z2Z619qt5e543",\
                "status": "Active",\
                "created": 1655626532543,\
                "type": "Commercial Registration",\
                "number": "1234567890",\
                "issuing_country": "KW",\
                "issuing_date": "2019-07-09T00:00:00.000+00:00",\
                "expiry_date": "2021-07-09T00:00:00.000+00:00",\
                "files": [\
                    "file_984450183956131840"\
                ]\
            }\
        ],
        "wallets": [\
            {\
                "id": "wal_1pTwK2822815mZfK19sH5I407",\
                "status": "Active",\
                "created": 1655626533149,\
                "base_currency": "KWD",\
                "country": "KW",\
                "primary_wallet": true,\
                "bank_account": {\
                    "id": "bka_0LTwK3222815C1ox191B5b736",\
                    "status": "Active",\
                    "created": 1655626532737,\
                    "iban": "INBNK00045545555555555555",\
                    "account_number": "DFGHGFVB876215bsdjhkn",\
                    "swift_code": "SWFT12345678909836435647"\
                },\
                "is_merchant": false,\
                "is_non_resident": false\
            }\
        ],
        "branches": [\
            {\
                "id": "brc_r0TwK3422815btrF19IN5z868",\
                "created": 1655626534868,\
                "virtual": true,\
                "brands": [\
                    "brd_u5TwK3422815FcYJ19zE5D771"\
                ]\
            }\
        ],
        "operator": {
            "id": "opr_sqTwK2822815Lagg19Qv5U407",
            "status": "Active",
            "created": 1655626534452,
            "developer_id": "dev_75TwK2822815F5cQ19v35I407",
            "name": "Default",
            "is_merchant": false,
            "api_credentials": {
                "test": {
                    "secret": "sk_test_OvnL46M5a2I7zuDpQrh10SxV",
                    "public": "pk_test_KH8sjIAUcXob14fVNkDY7t0M"
                }
            },
            "_merchant": false
        },
        "is_licensed": true,
        "not_for_profit": false,
        "taxable": true,
        "tax_number": "1234567890",
        "billing_address": {
            "id": "add_AZTwK32228158J4p19yP5L833",
            "country": "KW",
            "state": "Kuwait",
            "city": "Hawally",
            "zip_code": "30003",
            "recipient_name": "test",
            "po_box": "0000",
            "district": "Salmiya",
            "address_1": "Address one",
            "address_2": "Address two"
        }
    },
    "user": {
        "id": "usr_75TwK2822815F5cQ19v35I407",
        "status": "Active",
        "created": 1655626538781,
        "name": {
            "title": "Mr",
            "first": "Test",
            "middle": "Test",
            "last": "Test"
        },
        "contact_info": {
            "primary": {
                "email": "test@test.com",
                "phone": {
                    "country_code": "965",
                    "number": "51234567"
                }
            }
        },
        "authorization": {
            "id": "doc_gKTwK3222815xU0m19Fb5O447",
            "status": "CREATED",
            "created": 1655626532447,
            "name": {
                "title": "Mr",
                "first": "Test",
                "middle": "Test",
                "last": "Test"
            },
            "type": "identity_document",
            "issuing_country": "KW",
            "issuing_date": "2012-03-03T00:00:00.000+00:00",
            "expiry_date": "2020-03-03T00:00:00.000+00:00",
            "files": [\
                "file_984450183956131840"\
            ]
        },
        "identification": [\
            {\
                "id": "doc_p5TwK32228154T0d19DH5U350",\
                "status": "CREATED",\
                "created": 1655626532350,\
                "name": {\
                    "title": "Mr",\
                    "first": "Test",\
                    "middle": "Test",\
                    "last": "Test"\
                },\
                "type": "identity_document",\
                "number": "123456789",\
                "issuing_country": "KW",\
                "issuing_date": "2012-02-02T00:00:00.000+00:00",\
                "expiry_date": "2012-02-02T00:00:00.000+00:00",\
                "files": [\
                    "file_984450183956131840"\
                ]\
            }\
        ],
        "nationality": "KW",
        "date_of_birth": "2000-01-02T00:00:00.000+00:00",
        "is_authorized": true,
        "is_verified": false
    },
    "post": {
        "url": "http://flexwares.company/post_url"
    },
    "metadata": {
        "mtd": "metadata"
    }

  "destination_id": "56657933"
}

```