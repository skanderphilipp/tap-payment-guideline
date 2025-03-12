# Integration   [Skip link to Integration](https://developers.tap.company/docs/recommendations-best-practices\#integration)

1. For Acceptance, ensure that the charge ID is passed in the [Charges API](https://developers.tap.company/reference/create-a-charge) based on the type of policy
2. For Reconciliation purposes, ensure that the `reference.order` and `reference.transaction` are passed via API/SDK
3. For handling Duplicate charges, use `reference.idempotent`
4. For [Webhook](https://developers.tap.company/docs/webhook) Notification, use `post.url` within the API endpioints
5. For securing the Webhook Notification, use the [hashstring calculation](https://developers.tap.company/docs/webhook)
6. For finding the status of the payment for displaying on the confirmation screen, use Retrieve a Charge at the point of [redirection](https://developers.tap.company/docs/redirect)
7. Please process all refunds via [API](https://developers.tap.company/reference/refunds) or [Enterprise Dashboard](https://report.payments.tap.company/en)
8. For customized [user access](https://developers.tap.company/docs/user-access-permissions) management write to [integrations@tap.company](mailto:integrations@tap.company) with required access
9. For faster checkout experience use the card sdk v1/v2 instead of charge API

# Before going live   [Skip link to Before going live](https://developers.tap.company/docs/recommendations-best-practices\#before-going-live)

1. Ensure that your integration is thoroughly tested in sandbox and production
2. Request an Integration Review call with the [Developer Experience](https://www.tap.company/en-kw/support) team at tap
3. Ensure that the `sk_live` and `pk_live` keys are used
4. Ensure that the `POST.URL` and `REDIRECT.URL` are pointed to your production urls
5. Ensure that one live transaction is done for every payment method for all your integration channels (Web/Mob)
6. Ensure that you are able to view the transactions in the Enterprise Dashboard as well in your system

# Post go live   [Skip link to Post go live](https://developers.tap.company/docs/recommendations-best-practices\#post-go-live)

1. Monitor the transactions using the Enterprise Dashboard
2. For Payout reports, use the [payout API](https://developers.tap.company/reference/webhook-api) or [Enterprise Dashboard](https://report.payments.tap.company/en)

Updated10 months ago

* * *