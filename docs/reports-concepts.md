When merchants require customized reports, such as retrieving all the charges paid out during a specific period like June, Tap Payments' APIs offer a streamlined way to gather this data.

# Use Case   [Skip link to Use Case](https://developers.tap.company/docs/reports-concepts\#use-case)

This use case is to generate all paid out charges during a specific month

## Step 1: List All Payouts during a specific month   [Skip link to Step 1: List All Payouts during a specific month](https://developers.tap.company/docs/reports-concepts\#step-1-list-all-payouts-during-a-specific-month)

Use the 'List All Payouts' API:

- Send a request to the 'List All Payouts' API.
- Specify the date range for this specific month in your request parameters. This will filter the payouts to only include those processed within this period.
- The API response will include all payout IDs for the specified date range.

## Step 2: Retrieve individual Payouts   [Skip link to Step 2: Retrieve individual Payouts](https://developers.tap.company/docs/reports-concepts\#step-2-retrieve-individual-payouts)

From the API response in step 1, extract the payout IDs.

Use the download Payout API:

- Add the payout IDs to the request body of the download payout API
- This API will return detailed information on each payout, including all charges paid out in the specified month.

## Step 3: Compile and Review the Data   [Skip link to Step 3: Compile and Review the Data](https://developers.tap.company/docs/reports-concepts\#step-3-compile-and-review-the-data)

Organize Data:

- Compile the information from the individual payout downloads into a single report.
- This report will include all the charges processed and paid out in the specified month.

Review:

- Verify that all relevant data has been included.
- Ensure the report meets your customization requirements.

Updated6 months ago

* * *