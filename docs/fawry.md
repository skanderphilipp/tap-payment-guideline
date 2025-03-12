Fawry payment method accept only EGP currency.

Fawry source id value is "src\_eg.fawry". This source id, can be only used in the charge request.

It's an asynchronous payment method. It can take up to several days to confirm whether the payment has been successful. During this time, the payment cannot be guaranteed. The status of the payment’s charge object is initially set to IN\_PROGRESS, until the payment has been confirmed as successful or failed.

Post: If merchant provided the post.url in the charge request, Tap will post the charge response, when the charge status got updated.

If merchant provide the customer phone number, fawry order number and fawry store locations will be shared by SMS. Also it will be available in the charge response (charge.transaction.order)

Updatedover 1 year ago

* * *