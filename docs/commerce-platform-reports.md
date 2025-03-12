# Download Reports for Merchants on Commerce Platforms   [Skip link to Download Reports for Merchants on Commerce Platforms](https://developers.tap.company/docs/commerce-platform-reports\#download-reports-for-merchants-on-commerce-platforms)

Merchants operating under commerce platforms or payment technology solutions have multiple ways to generate charge, authorize, refund, or payout reports through our APIs. These methods are outlined below:

In this document, we will guide you through the available ways the merchants can generate reports programmatically through our APIs. For all the APIs mentioned below, merchants must use their own **MID** (Merchant ID) and **Secret Keys**. These credentials can be found inside the business dashboard, which can be accessed here:

[Business Dashboard](https://businesses.tap.company/)

Once merchants have the required credentials, they can use the following APIs:

## 1 List API   [Skip link to 1 List API](https://developers.tap.company/docs/commerce-platform-reports\#1-list-api)

The List API allows merchants to retrieve all charges, authorizations, refunds, or payouts within a specified period (maximum 30 days). The response will be in JSON format and will include all transactions for the provided MID within the given date range.

### API Documentation:   [Skip link to API Documentation:](https://developers.tap.company/docs/commerce-platform-reports\#api-documentation)

- [List Charges](https://developers.tap.company/reference/list-all-charges)
- [List Authorizes](https://developers.tap.company/reference/list-all-authorize)
- [List Refunds](https://developers.tap.company/reference/list-all-refunds)
- [List Payouts](https://developers.tap.company/reference/list-payouts)

## 2 Download API   [Skip link to 2 Download API](https://developers.tap.company/docs/commerce-platform-reports\#2-download-api)

The Download API provides transaction data in CSV format. Merchants need to specify the date period to retrieve charges, refunds, or authorizations for that timeframe.

### API Documentation:   [Skip link to API Documentation:](https://developers.tap.company/docs/commerce-platform-reports\#api-documentation-1)

- [Download Charges](https://developers.tap.company/reference/download-charges)
- [Download Authorizes](https://developers.tap.company/reference/download-authorize)
- [Download Refunds](https://developers.tap.company/reference/download-refunds)
- [Download Payouts](https://developers.tap.company/reference/download-payouts)

> Note that **Download Payouts** is only meant to be used in the **Live Mode**, any downlaod payout requests in the sandbox mode will not go through.

## 3 Retrieve API   [Skip link to 3 Retrieve API](https://developers.tap.company/docs/commerce-platform-reports\#3-retrieve-api)

The Retrieve API is a GET request used to fetch details of a single charge, authorization, refund, or payout. Merchants must provide the transaction ID in the request parameters. The response will include a JSON object containing the transaction’s details.

### API Documentation:   [Skip link to API Documentation:](https://developers.tap.company/docs/commerce-platform-reports\#api-documentation-2)

- [Retrieve Charges](https://developers.tap.company/reference/retrieve-a-charges)
- [Retrieve Authorizes](https://developers.tap.company/reference/retrieve-an-authorize)
- [Retrieve Refunds](https://developers.tap.company/reference/retrieve-a-refund)
- [Retrieve Payout](https://developers.tap.company/reference/retrieve-a-payout)

Updatedabout 1 month ago

* * *