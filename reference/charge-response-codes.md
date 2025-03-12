| Code | Message |
| --- | --- |
| 000 | Captured |
| 001 | Authorized |
| 100 | Initiated |
| 200 | In Progress |
| 301 | Abandoned |
| 302 | Canceled |
| 303 | Deferred |
| 304 | Expired |
| 401 | Failed |
| 402 | Failed, Invalid Parameter |
| 403 | Failed, Duplicate |
| 404 | Failed, Locked |
| 405 | Failed, Invalid Card No |
| 406 | Failed, Invalid Expiry |
| 407 | Failed, Expired Card |
| 408 | Failed, Unspecified Failure |
| 501 | Declined |
| 502 | Declined, Incorrect CSC/CVV |
| 503 | Declined, 3D Security - Incorrect |
| 504 | Declined, 3D Security - Card not Enrolled |
| 505 | Declined, Insufficient Funds |
| 506 | Declined, Transaction Type Not Supported |
| 507 | Declined, Card Issuer |
| 508 | Declined, Card Issuer - No Reply |
| 509 | Declined, Card Issuer - Do not Contact |
| 510 | Declined, Card Issuer - Referral Response |
| 511 | Declined, Card Issuer - Error |
| 512 | Declined, Not Authenticated |
| 513 | Declined, Card Acquirer - Error |
| 514 | Declined, Card Issuer - Risk Check |
| 515 | Declined, Tap |
| 516 | Declined, Authentication Failed |
| 601 | Void |
| 701 | Restricted |
| 702 | Restricted, Retry Limit Exceeded |
| 703 | Restricted, Bank |
| 704 | Restricted, Tap |
| 801 | Timed Out |
| 901 | Unknown |

# Refunds Response Codes   [Skip link to Refunds Response Codes](https://developers.tap.company/reference/charge-response-codes\#refunds-response-codes)

| Code | Message |
| --- | --- |
| 000 | Refunded |
| 100 | Pending |
| 200 | In Progress |
| 301 | Canceled |
| 401 | Failed |
| 402 | Failed, Invalid Parameter |
| 403 | Failed, Duplicate |
| 501 | Declined |
| 502 | Declined, Insufficient Balance |
| 503 | Declined, Refund not Supported |
| 504 | Declined, Partial Refund not Supported |
| 601 | Restricted |
| 602 | Restricted, Bank |
| 701 | Timed Out |
| 801 | Unknown |

# HTTP Response Codes   [Skip link to HTTP Response Codes](https://developers.tap.company/reference/charge-response-codes\#http-response-codes)

| Code | Description |
| --- | --- |
| 200 - OK | Everything worked as expected. |
| 400 - Bad Request | The request was unacceptable, often due to missing a required parameter. |
| 401 - Unauthorized | No Valid API key was provided. |
| 402 - Request Failed | The parameters were valid but the request failed. |
| 403 - Forbidden | Access is denied. |
| 404 - Not Found | The requested resource does not exist. |
| 409 - Conflict | The request conflicts with another request. |
| 429 - Too Many Requests | Too many requests hit the API quickly. We recommend an exponential backoff of your requests. |
| 500, 502, 503, 504 - Server Errors | Something went wrong on Tap's end. |

# Error Codes 'Bad Requests'   [Skip link to Error Codes 'Bad Requests'](https://developers.tap.company/reference/charge-response-codes\#error-codes-bad-requests)

If the API request fails, Tap returns an appropriate error code

| Code | Description |
| --- | --- |
| 1100 | Header values are missing |
| 1101 | Secret API Key and Environment are mismatched |
| 1102 | Request values are empty |
| 1103 | Required inputs are invalid |
| 1104 | Customer id is missing |
| 1105 | Customer id is invalid |
| 1106 | Customer not found |
| 1107 | Customer id is not matching with existing customer |
| 1108 | Save card features are not enabled |
| 1109 | Non-3D secure transactions are not allowed |
| 1110 | Redirect URL is missing |
| 1111 | Redirect URL is invalid |
| 1112 | Authorize id is missing |
| 1113 | Authorize id is invalid |
| 1114 | Please check the Authorize status |
| 1115 | Authorize not found |
| 1116 | Save card feature not supported for this transaction |
| 1117 | Amount is invalid |
| 1118 | Currency code is invalid |
| 1119 | Currency code not supported |
| 1120 | Statement descriptor is invalid or length should be less than 60 characters |
| 1121 | The 'description' should be less than 1000 characters |
| 1122 | Merchant order reference length should be less than 100 characters |
| 1123 | Merchant transaction reference length should be less than 100 characters |
| 1124 | Source id is missing |
| 1125 | Source id is invalid |
| 1126 | Source already used, Please create the new source |
| 1127 | The metadata key length should be less than 250 characters |
| 1128 | Metadata value length should be less than 1000 characters |
| 1129 | Customer id or Customer information is required |
| 1130 | Customer's first name is required |
| 1131 | Customer's first name length should be less than 150 characters |
| 1132 | Customer last name is required |
| 1133 | Customer last name length should be less than 150 characters |
| 1134 | Customer middle name length should be less than 150 characters |
| 1135 | Phone number is required |
| 1136 | Phone number country code is invalid |
| 1137 | Phone number is invalid |
| 1138 | Email Address is invalid |
| 1139 | Customer phone number or email address is required |
| 1140 | Card number is invalid |
| 1141 | Card expiry is invalid |
| 1142 | Charge id is missing |
| 1143 | Charge id is invalid |
| 1144 | Charge id not found |
| 1145 | Authenticate type is missing |
| 1146 | Authenticate type is invalid |
| 1147 | Confirmation code is missing |
| 1148 | Confirmation code is invalid |
| 1149 | Currency code is not matching with existing currency code |
| 1150 | Capture amount exceeds with the outstanding authorized amount |
| 1151 | Gateway timed out |
| 1152 | Invalid authorize auto schedule type |
| 1153 | Invalid authorize auto schedule time |
| 1154 | BIN is missing |
| 1155 | BIN is invalid |
| 1156 | Refund reason is missing |
| 1157 | Refund reason length should be less than 250 characters |
| 1158 | Refund id is missing |
| 1159 | Refund id is invalid |
| 1160 | Refund not found |
| 1161 | Requested refund amount exceeds |
| 1162 | Invalid row count should be less than or equal to 50 |
| 1163 | Provided card is not supported, Please try with another card |
| 1164 | Merchant id is invalid |
| 1165 | Transfer id is missing |
| 1166 | Transfer id is invalid |
| 1167 | Transfer not found |
| 1168 | Requested transfer amount exceeds with charge amount |
| 1169 | Destination and Application cannot be applied in the same charge request |
| 1170 | Transfer Currency code is invalid |
| 1171 | Destination id cannot be duplicated |
| 1172 | Destination id invalid |
| 2100 | Invalid JSON request |
| 2101 | The server is currently unavailable (overloaded or down) |
| 2102 | Request not found |
| 2103 | Application Required |
| 2104 | Invalid API Key |
| 2105 | API credentials are required |
| 2106 | Please use the secret key, the public key given |
| 2107 | Authorization Required |
| 2108 | It is likely that you need to grant permission\_name |
| 4100 | Card validation failed - card name can only have 10 integer values |
| 4101 | Card validation failed - Card has expired |
| 4102 | Card validation failed - cvc is too short/long |
| 9998 | Required inputs are invalid. Please check the currency or amount |
| 9999 | Internal server error |

# Standard Errors   [Skip link to Standard Errors](https://developers.tap.company/reference/charge-response-codes\#standard-errors)

Each error has a unique error code and description, errors are returned in an array of error objects. below is the schema and example of an error.

Example

```rdmd-code lang-Text theme-light
{
  "errors": [\
    {\
      "code": "1144",\
      "description": "Charge not found"\
    }\
  ]
}

```

/