To place a hold on a card, use the Authorize API. You can later capture the payment or release the hold. To authorize a card, create an authorization request. If in test mode, the card won't be authorized, but everything else will occur as if in live mode.

To automatically capture the authorized payment after a defined number of hours, you can use the `auto` object and set the `type` to `AUTO`. Alternatively if the `type` is `VOID`, the authorization hold will be released after the predefined `time`.

To capture an authorized payment, you can use [Charges API](http://google.com/). You can pass the `authorize_id` within the `source_id` of the charges request.

Please review the Authorization Request and Authorization Response Model to get more information.

ShellNodeRubyPHPPython

Click `Try It!` to start a request and see the response here!