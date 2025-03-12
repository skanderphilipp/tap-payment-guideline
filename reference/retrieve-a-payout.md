| time | status | user agent |  |
| :-- | :-- | :-- | :-- |
| Retrieving recent requests… |

LoadingLoading…

#### URL Expired

The URL for this request expired after 30 days.

payouts

object

Filter criteria for the payout to retrieve

payouts object

merchants

array of strings

Defaults to 599242

merchant ID for which the payout is being queried

merchants
string

ADD string

# `` 200      200

object

object

string

live\_mode

boolean

Defaults to true

api\_version

string

count

integer

Defaults to 0

has\_more

boolean

Defaults to true

payouts

array of objects

payouts

object

id

string

status

string

date

integer

Defaults to 0

amount

integer

Defaults to 0

currency

string

merchant\_id

string

wallet

object

wallet object

settlements\_available

boolean

Defaults to true

bank\_reference

string

# `` 400      400

object

Updated 7 months ago

* * *

Did this page help you?

Yes

No

ShellNodeRubyPHPPython

```

xxxxxxxxxx

17

1curl --request POST \

2     --url https://api.tap.company/v2/payouts/list/ \

3     --header 'Authorization: Bearer sk_test_GM34ihbYXa8wcKjqenoQFHS2' \

4     --header 'accept: application/json' \

5     --header 'content-type: application/json' \

6     --data '

7{

8  "payouts": {

9    "payout_id": [\
\
10      "payout_xxxx"\
\
11    ]

12  },

13  "merchants": [\
\
14    "599242"\
\
15  ]

16}

17'

```

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated 7 months ago

* * *

Did this page help you?

Yes

No