| time | status | user agent |  |
| :-- | :-- | :-- | :-- |
| Make a request to see history. |

#### URL Expired

The URL for this request expired after 30 days.

period

object

Retrieve charges for a selected period

period object

status

string

Retrieve the selected list of charges info by charge status. Values can be: INITIATED, IN\_PROGRESS, ABANDONED, CANCELLED, FAILED, DECLINED, RESTRICTED, CAPTURED, VOID, TIMEDOUT or UNKNOWN

sources

array of strings

Array of sources (you can specify the list of Source ID's to retrieve).

sources
ADD string

payment\_methods

array of strings

Array of payment methods (you can specify the list of payment method Source ID's to retrieve).

payment\_methods
ADD string

customers

array of strings

Array of customers (you can specify the list of Customer ID's to retrieve).

customers
ADD string

charges

array of strings

Array of charges (you can specify the list of Source ID's to retrieve).

charges
ADD string

starting\_after

string

A cursor for use in pagination. The starting\_after parameter takes a charge ID that determines your position in the list. For example, if your list request returns 50 charges that end with cus\_foo, you can use starting\_after=cus\_foo in your next call to retrieve the next page of the list.

charge\_created

string

Created date (charge created date), Measured in Unix Epoch Timestamp (milliseconds).

mobile

string

Filter the results based on customer mobile number

email

string

filter the results based on customer email

limit

string

Defaults to 25

The maximum number of charges to return in a single call. Default: 25; Maximum: 50.

order

string

Sort the results Ascending or Descending by date

chronologicalreverse\_chronological

order\_by

string

Defaults to date

Applying the sorting based on

metadata

string

Filter the results based on meta data values

currency

string

Filter the charges based on charge currency

payouts

object

Retrieve charges based on payouts

payouts object

reference

object

reference object

# `` 200      200

object

object\_type

string

live\_mode

boolean

Defaults to true

count

integer

Defaults to 0

has\_more

boolean

Defaults to true

api\_version

string

charges

array of objects

charges

object

id

string

object

string

live\_mode

boolean

Defaults to true

api\_version

string

status

string

amount

integer

Defaults to 0

currency

string

threeDSecure

boolean

Defaults to true

save\_card

boolean

Defaults to true

statement\_descriptor

string

transaction

object

transaction object

reference

object

reference object

response

object

response object

security

object

security object

acquirer

object

acquirer object

card

object

card object

receipt

object

receipt object

customer

object

customer object

source

object

source object

redirect

object

redirect object

post

object

post object

description

string

metadata

object

metadata object

payout

object

payout object

# `` 400      400

object

Updated about 1 year ago

* * *

Did this page help you?

Yes

No

ShellNodeRubyPHPPython

```

xxxxxxxxxx

18

1curl --request POST \

2     --url https://api.tap.company/v2/charges/list \

3     --header 'Authorization: Bearer sk_test_XKokBfNWv6FIYuTMg5sLPjhJ' \

4     --header 'accept: application/json' \

5     --header 'content-type: application/json' \

6     --data '

7{

8  "period": {

9    "date": {

10      "from": "1662190768000",

11      "to": "1662536368000"

12    },

13    "type": "1"

14  },

15  "limit": "25",

16  "order_by": "date"

17}

18'

```

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated about 1 year ago

* * *

Did this page help you?

Yes

No