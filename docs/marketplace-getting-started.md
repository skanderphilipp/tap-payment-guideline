## Before you begin   [Skip link to Before you begin](https://developers.tap.company/docs/marketplace-getting-started\#before-you-begin)

1. Contact Tap team to confirm if you are eligible to use Tap’s Marketplace solution.
2. Follow our [Get started](https://developers.tap.company/docs/get-started-1) guide to set up your test account and get your API keys.
3. When confirmed that Tap’s Marketplace solution is a good fit for your use case, we will provide you with Marketplace keys to be used for onboarding.

> ## 📘
>
> You will receive two sets of keys:
>
> 1. **Marketplace Keys**: to be used for onboarding Businesses.
> 2. **Merchant Keys**: to be used for payment processing.

* * *

## Step 1: Onboarding Businesses   [Skip link to Step 1: Onboarding Businesses](https://developers.tap.company/docs/marketplace-getting-started\#step-1-onboarding-businesses)

Each Business has to be onboarded on Tap. An account will be created, and Tap will carry out the KYC verification process before the final account approval.

Onboarding your Businesses requires two steps:

1. Uploading the Business KYC documents.
2. Creating a `destination_id` for the Business using Business API.

* * *

## Step 2: Accepting payments   [Skip link to Step 2: Accepting payments](https://developers.tap.company/docs/marketplace-getting-started\#step-2-accepting-payments)

Once Business have been onboarded, you can instantly start accepting payments for the newly created Business.

> ## 👍
>
> You can accept payments for your Businesses immediately after onboarding, but payouts will not be available while the Business's account is pending approval.
>
> It is recommended to wait until the KYC process is completed, and the account is approved by Tap.

You can split the payment's amount between multiple Businesses, simply by adding the `destinations` object in the transaction request. For example, when a payment is done on your Marketplace, you can split the amount so that a portion goes to your Marketplace account as a fee or commission, and the remaining of the payment amount goes to the Business's account.

JSON

```rdmd-code lang-json theme-light
"destinations": {
    "destination": [\
      {\
        "id": "480593",\
        "amount": 2,\
        "currency": "KWD"\
      },\
      {\
        "id": "486374",\
        "amount": 3,\
        "currency": "KWD"\
      }\
    ]
  }

```

* * *

## Step 3: Payouts   [Skip link to Step 3: Payouts](https://developers.tap.company/docs/marketplace-getting-started\#step-3-payouts)

After a Business account successfully passes required KYC checks, payouts will be available. Payouts can be initiated automatically by Tap to the Business's bank account, or you can initiate manually from Tap's dashboard.

> ## 📘
>
> If you want to initiate the payouts manually, contact our team to disable the auto settlement for the Business's account. Once disabled, you'll have the option to initiate the payout from the dashboard.

* * *

## Step 4: Reconciliation   [Skip link to Step 4: Reconciliation](https://developers.tap.company/docs/marketplace-getting-started\#step-4-reconciliation)

* * *

## See also   [Skip link to See also](https://developers.tap.company/docs/marketplace-getting-started\#see-also)

[**Onboarding Businesses** \\
Onboard your Businesses](https://developers.tap.company/docs/onboarding)

[**Split Payments** \\
Split the amount at the time of the transaction](https://developers.tap.company/docs/split-payments)

[**After Payments**](https://developers.tap.company/docs/)

Updated28 days ago

* * *