Please use the following test card number to simulate the charging process as your customer.

Note: To enter the KNET test card number on the KNET page, select KNET Test Card \[KNET1\] option from the Bank drop-down list.

## Local Payment Methods   [Skip link to Local Payment Methods](https://developers.tap.company/reference/testing-cards\#local-payment-methods)

| Payment Method | Card Number | Expiry Date | PIN | Status |
| --- | --- | --- | --- | --- |
| KNET | 8888880000000001 | 09/25 | 1234 | CAPTURED |
| KNET | 8888880000000002 | 09/25 | 1234 | CAPTURED |
| KNET | 8888880000000001 | 05/21 | 1234 | NOT CAPTURED |
| Benefit | 4600410123456789 | 12/27 | 1234 | CAPTURED |
| Benefit | 7777770123456789 | 12/27 | 1234 | NOT CAPTURED |
| Benefit | 1111110123456789 | 12/27 | 1234 | DECLINED |
| Naps/QPay | 4215375500883243 | 12/25 | 944 (OTP 1234) | CAPTURED |

## Credit/Debit Cards   [Skip link to Credit/Debit Cards](https://developers.tap.company/reference/testing-cards\#creditdebit-cards)

| Payment Method | Card Number | 3D Secure Enrolled |
| --- | --- | --- |
| MasterCard | 5123450000000008 | Yes |
| MasterCard | 5111111111111118 | No |
| VISA | 4508750015741019 | Yes |
| VISA | 4012000033330026 | No |
| American Express | 345678901234564 | Yes |
| American Express | 371449635398431 | No |
| mada | 4464040000000007 | Yes |
| mada | 5588480000000003 | No |
| OmanNet | 4228230000000001 | Yes |

## Expiry Dates   [Skip link to Expiry Dates](https://developers.tap.company/reference/testing-cards\#expiry-dates)

| Expiry Date | Transaction Response |
| --- | --- |
| 01/39 | APPROVED |
| 05/22 | DECLINED |
| 04/27 | EXPIRED\_CARD |
| 08/28 | TIMED\_OUT |
| 01/37 | ACQUIRER\_SYSTEM\_ERROR |
| 02/37 | UNSPECIFIED\_FAILURE |
| 05/37 | UNKNOWN |

## CSC/CVV   [Skip link to CSC/CVV](https://developers.tap.company/reference/testing-cards\#csccvv)

|  | CSC/CVV | Response Gateway Code for MasterCard & Visa Cards |
| --- | --- | --- |
| MasterCard & Visa Cards | 100 | MATCH |
| MasterCard & Visa Cards | 101 | NOT\_PROCESSED |
| MasterCard & Visa Cards | 102 | NO\_MATCH |
| American Express | 1000 | MATCH |
| American Express | 1010 | NOT\_PROCESSED |
| American Express | 1020 | NO\_MATCH |
| OmanNet | 123 (OTP is 9999) | MATCH |

## STC Pay Phone Numbers   [Skip link to STC Pay Phone Numbers](https://developers.tap.company/reference/testing-cards\#stc-pay-phone-numbers)

| Country Code | Phone Number |
| --- | --- |
| 966 | 557877988 |
| 966 | 506027231 |
| 966 | 537974429 |
| 966 | 558646150 |