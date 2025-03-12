| time | status | user agent |  |
| :-- | :-- | :-- | :-- |
| Make a request to see history. |

#### URL Expired

The URL for this request expired after 30 days.

For every business created, you can add entities, brands, branches, and other related information, granting you access to all features in Tap.

name

object

required

Name object accepts multiple languages. Languages that are accepted ar,en,fr,fa,es,ru,tl,it,nl,de,tr,hi,ml,ur,pa,te,ta,bn and zh

name object

type

string

required

Defaults to corp

The type of business. The accepted values are "ind" or "corp". Use "ind" for individual based businesses (e.g. Instagram businesses, freelancers etc.) and "corp" for registered businesses.

entity

object

required

The entity details of the business.

entity object

contact\_person

object

contact\_person object

brands

array of objects

required

The brand of the business.

brands\*
ADD object

post

object

The url of the webhook.

post object

metadata

object

The used defined "key": "value" pairs to be passed in the business object.

metadata object

idempotent

string

The idempotent string to restrict duplicate creation of business. If the same idempotent string is passed, a new business will not be created, whereas the response of the first business will be returned.

# `` 200      200

object

# `` 400      400

object

Updated 7 days ago

* * *

Did this page help you?

Yes

No

ShellNodeRubyPHPPython

```

xxxxxxxxxx

60

1curl --request POST \

2     --url https://api.tap.company/v2/business/ \

3     --header 'Authorization: Bearer sk_test_BPmcTgEfuK1dHslMaLGY42Ry' \

4     --header 'accept: application/json' \

5     --header 'content-type: application/json' \

6     --data '

7{

8  "name": {

9    "en": "Brand Name"

10  },

11  "type": "corp",

12  "entity": {

13    "license": {

14      "number": "2134342SE"

15    },

16    "country": "KW"

17  },

18  "contact_person": {

19    "name": {

20      "title": "Mr",

21      "first": "Test",

22      "middle": "Test",

23      "last": "Test"

24    },

25    "contact_info": {

26      "primary": {

```

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

`` 200 - Result`` 400 - Result

Updated 7 days ago

* * *

Did this page help you?

Yes

No