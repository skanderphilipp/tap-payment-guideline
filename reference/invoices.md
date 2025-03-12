## Overview   [Skip link to Overview](https://developers.tap.company/reference/invoices\#overview)

To create an invoice, the merchant needs to provide both the order and customer information. Invoices can be retrieved individually or as a complete list. Each invoice has a unique, randomly generated ID called Invoice ID that starts with "inv\_".

**Flow:**

After creating an invoice using our API, the merchant will share the invoice URL with the customer via email or SMS. The customer can then view the invoice and pay using one of the merchant's accepted payment methods.

Once the customer has paid the invoice, they will be redirected to the merchant's specified redirect URL if provided. Additionally, if the merchant has provided a post URL, the invoice response will be posted to that URL.

## Invoices Request Example   [Skip link to Invoices Request Example](https://developers.tap.company/reference/invoices\#invoices-request-example)

To generate an invoice, both the order and customer information are required.

**Draft** -\> A merchant can create a draft invoice and save it without generating or sending it to the customer. Then, using the finalized API, they can generate the actual invoice and send it to the customer.

**Customer** -\> When creating an invoice, the customer's ID or information is required. If the merchant provides customer information, Tap will create a new customer and share the customer ID in the invoice response. The merchant can store this ID for future invoice creation.

**Order** -\> The invoice request should include the order amount and currency, which will be considered as the invoice amount and currency. Alternatively, the merchant can pass the order ID in the request.

**Items** -\> The invoice request can also include product IDs or item information. If a product ID is provided, the product information will be collected and linked with the order. If the merchant provides item information, Tap will create a new product ID and share it in the invoice response. The merchant can store this ID for future invoice creation.

Finally, merchants can also specify which currencies and payment methods are available for an invoice.

JSON

```rdmd-code lang-json theme-light

{
  "draft": false,
  "due": 1604728943000,
  "expiry": 1604728943000,
  "description": "test invoice",
  "mode": "INVOICE",
  "savecard": false,
  "note": "test note",
  "notifications": {
    "channels": [\
      "SMS",\
      "EMAIL"\
    ],
    "dispatch": true
  },
  "currencies": [\
    "KWD"\
  ],
  "metadata": {
    "udf1": "1",
    "udf2": "2",
    "udf3": "3"
  },
  "charge": {
    "receipt": {
      "email": true,
      "sms": true
    },
    "statement_descriptor": "test"
  },
  "customer": {
    "email": "test@test.com",
    "first_name": "test",
    "last_name": "test",
    "middle_name": "test",
    "phone": {
      "country_code": "965",
      "number": "51234567"
    }
  },
  "order": {
    "amount": 12,
    "currency": "KWD",
    "items": [\
      {\
        "amount": 10,\
        "currency": "KWD",\
        "description": "test",\
        "discount": {\
          "type": "P",\
          "value": 0\
        },\
        "image": "",\
        "name": "test",\
        "quantity": 1\
      }\
    ],
    "shipping": {
      "amount": 1,
      "currency": "KWD",
      "description": "test",
      "provider": "ARAMEX",
      "service": "test"
    },
    "tax": [\
      {\
        "description": "test",\
        "name": "VAT",\
        "rate": {\
          "type": "F",\
          "value": 1\
        }\
      }\
    ]
  },
  "payment_methods": [\
    ""\
  ],
  "post": {
    "url": "http://your_website.com/post_url"
  },
  "redirect": {
    "url": "http://your_website.com/redirect_url"
  },
  "reference": {
    "invoice": "INV_00001",
    "order": "ORD_00001"
  }
}

```

## Invoices Response Example   [Skip link to Invoices Response Example](https://developers.tap.company/reference/invoices\#invoices-response-example)

Once Tap has validated the invoice request, it will return the invoice response, which includes a "status" field that defines the current status of the invoice. The possible values for this field are:

SAVED: The invoice has been saved as a draft.

CREATED: The invoice has been successfully created.

CANCELLED: The invoice has been canceled.

EXPIRED: The invoice has expired. Once the expiry date is reached, Tap will automatically change the status to "expired".

PAID: The invoice has been paid.

**Customer** -\> If the customer ID is not provided in the invoice request, Tap will create a new customer and share the customer ID in the invoice response. The merchant can store this ID for future invoice creation.

**Track** -\> The invoice response also includes a Track object, which provides the latest status and full activity details, such as how many times the invoice page has been viewed and the number of payment attempts made.

The possible values for the invoice tracking status are:

**DRAFT,**

**SCHEDULED, DISPATCHED, DELIVERED, VIEWED,**

**CANCELLED, EXPIRED,**

**PAYMENT\_ATTEMPT, PAYMENT\_FAILED,**

**PAYMENT\_AUTHORIZED, PAYMENT\_CAPTURED, PAYMENT\_POSTED,**

**PAYMENT\_REFUNDED, PAYMENT\_PARTIALLY\_REFUNDED,**

**PAYMENT\_ON\_HOLD, PAYMENT\_SETTLED**

**Transactions** -\> The transactions list provides information about the charge attempt made for the invoice.

JSON

```rdmd-code lang-json theme-light

{
  "object": "invoice",
  "live_mode": false,
  "api_version": "V1.1",
  "id": "inv_kN0e13110124xGi527019",
  "method": "GET",
  "savecard": false,
  "status": "PAID",
  "track": "PAYMENT_CAPTURED",
  "amount": 13,
  "currency": "KWD",
  "timezone": "UTC +3:00",
  "created": 1574284348019,
  "url": "http://test.gocollect.io:8082/invoice/inv_kN0e13110124xGi527019",
  "draft": false,
  "due": 1604728943000,
  "expiry": 1604728943000,
  "business": null,
  "notifications": {
    "dispatch": true,
    "channels": [\
      "SMS",\
      "EMAIL"\
    ]
  },
  "mode": "INVOICE",
  "order": {
    "id": "ord_cxrA1311012t6Sz527097",
    "currency": "KWD",
    "amount": 13,
    "items": [\
      {\
        "product_id": "prd_uEZV1311012slxT527098",\
        "name": "TEST",\
        "description": "TEST",\
        "image": "",\
        "currency": "KWD",\
        "amount": 11,\
        "quantity": 1,\
        "discount": {\
          "type": "F",\
          "value": 1\
        },\
        "id": "itm_QsSZ1311012Vu2s527098"\
      }\
    ],
    "tax": [\
      {\
        "id": "tax_bDQN1311012iX76527099",\
        "name": "VAT 001",\
        "description": "VAT",\
        "rate": {\
          "type": "F",\
          "value": 1\
        }\
      }\
    ],
    "shipping": {
      "id": "shp_KV1c1311012BImv527103",
      "currency": "KWD",
      "amount": 1,
      "provider": "TEST",
      "service": "TEST",
      "description": "Shipping"
    },
    "created": 1574284349097
  },
  "reference": {
    "invoice": "INV_00001",
    "order": "ORD_0001",
    "documents": [\
      {\
        "type": "",\
        "number": "",\
        "images": [\
          ""\
        ]\
      }\
    ]
  },
  "customer": {
    "id": "cus_Ms490320190018Yx4a2111171",
    "first_name": "TEST",
    "middle_name": "",
    "last_name": "TEST",
    "email": "test@test.com",
    "phone": {
      "country_code": "965",
      "number": "5000000"
    }
  },
  "post": {
    "url": ""
  },
  "redirect": {
    "url": ""
  },
  "metadata": {
    "udf1": "TEST1",
    "udf2": "TEST2"
  },
  "description": "TEST INVOICE",
  "invoice_number": "20191120211229",
  "frequency": "SINGLE",
  "transactions": [\
    {\
      "id": "chg_Br9b3120190018n5PB2111447",\
      "object": "charge",\
      "status": "CAPTURED",\
      "amount": 13,\
      "currency": "KWD",\
      "transaction": {\
        "timezone": "UTC+03:00",\
        "created": "1574295511494",\
        "authorization_id": "B14367"\
      },\
      "reference": {\
        "track": "tck_Pj2i3120190018Mq2y2111635",\
        "payment": "3121190018116353001",\
        "gateway": "201932557785983",\
        "transaction": "INV_00001",\
        "order": "ORD_0001"\
      },\
      "response": {\
        "code": "000",\
        "message": "Captured"\
      },\
      "receipt": {\
        "id": "203121190018114462",\
        "email": true,\
        "sms": true\
      },\
      "source": {\
        "payment_method": "KNET",\
        "id": "src_kw.knet"\
      }\
    }\
  ],
  "charge": {
    "receipt": {
      "email": true,
      "sms": true
    },
    "source": {
      "id": "tok_xxxxxxx"
    },
    "statement_descriptor": "test"
  },
  "trackable": {
    "id": "tck_PDCQ1311012FCs4527902",
    "status": "PAYMENT_CAPTURED",
    "link": "http://test.gocollect.io:8082/invoice/track/tck_PDCQ1311012FCs4527902",
    "activity": [\
      {\
        "object": "activity",\
        "id": "act_rXka1311012WnIm527902",\
        "type": "CREATED",\
        "created": 1574284349903\
      },\
      {\
        "object": "activity",\
        "id": "act_TgTp1311012M5Tz527501",\
        "type": "VIEWED",\
        "created": 1574284358501\
      },\
      {\
        "object": "activity",\
        "id": "act_GgYo1311012UvAD527029",\
        "type": "PAYMENT_CAPTURED",\
        "created": 1574284402029\
      },\
      {\
        "object": "activity",\
        "id": "act_yrx41311012RUTR527555",\
        "type": "VIEWED",\
        "created": 1574284402555\
      }\
    ]
  },
  "payment_methods": [],
  "currencies": [],
  "note": "TEEST",
  "lang_code": "EN",
  "merchant_id": "599424"
}

```

Updated over 1 year ago

* * *

Did this page help you?

Yes

No

Updated over 1 year ago

* * *

Did this page help you?

Yes

No