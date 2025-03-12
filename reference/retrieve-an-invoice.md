#### URL Expired

The URL for this request expired after 30 days.

invoice\_id

string

required

optional

# `` 200      200

object

object

string

live\_mode

boolean

Defaults to true

api\_version

string

id

string

method

string

status

string

amount

integer

Defaults to 0

currency

string

created

integer

Defaults to 0

updated

integer

Defaults to 0

url

string

draft

boolean

Defaults to true

due

integer

Defaults to 0

expiry

integer

Defaults to 0

mode

string

description

string

description\_id

string

invoice\_number

string

frequency

string

lang\_code

string

metadata

object

udf1

string

udf2

string

udf3

string

notifications

object

dispatch

boolean

Defaults to true

channels

array of strings

channels

order

object

object

string

id

string

live\_mode

boolean

Defaults to true

api\_version

string

currency

string

amount

integer

Defaults to 0

status

string

items

array of objects

items

object

id

string

product\_id

string

name

string

description

string

image

string

currency

string

amount

integer

Defaults to 0

quantity

integer

Defaults to 0

discount

object

discount object

merchant\_id

string

tax

array of objects

tax

object

id

string

name

string

description

string

rate

object

rate object

shipping

object

shipping object

itemAmount

integer

Defaults to 0

created

integer

Defaults to 0

merchant\_id

string

reference

object

invoice

string

order

string

customer

object

id

string

first\_name

string

middle\_name

string

last\_name

string

email

string

phone

object

phone object

post

object

url

string

redirect

object

url

string

charge

object

receipt

object

receipt object

statement\_descriptor

string

track

object

id

string

object

string

status

string

updated

integer

Defaults to 0

activity

array of objects

activity

object

id

string

object

string

type

string

created

integer

Defaults to 0

payment\_methods

array of strings

payment\_methods

currencies

array of strings

currencies

savecard

boolean

Defaults to true

note

string

merchant\_id

string

# `` 400      400

object

errors

array of objects

errors

object

code

string

description

string

http\_code

string

Updated over 1 year ago

* * *

Did this page help you?

Yes

No

ShellNodeRubyPHPPython

```

xxxxxxxxxx

1curl --request GET \

2     --url https://api.tap.company/v2/invoices/invoice_id \

3     --header 'Authorization: Bearer sk_test_XKokBfNWv6FIYuTMg5sLPjhJ' \

4     --header 'accept: application/json'

```

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated over 1 year ago

* * *

Did this page help you?

Yes

No