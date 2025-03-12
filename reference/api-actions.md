## Capture a payment   [Skip link to Capture a payment](https://developers.tap.company/reference/api-actions\#capture-a-payment)

If your transaction is AUTHORIZED using the [Authorize API](https://tappayments.readme.io/reference/create-an-authorize), and you want to CAPTURE it, you can use the [Create a Charge API](https://tappayments.readme.io/reference/create-a-charge) and provide the Authorize ID

## Retrieve the details of a payment   [Skip link to Retrieve the details of a payment](https://developers.tap.company/reference/api-actions\#retrieve-the-details-of-a-payment)

If you would like to retrieve the details of a payment at any stage of the payment transaction life cycle, use [Retrieve a Charge](https://developers.dev.tap.company/reference/retrieve-a-charges). This API allows you to retrieve information about a specific charge, such as its status, amount, currency, and customer details. You will need to provide the Charge ID of the payment you want to retrieve in the API request.

## Retrieve the details of all payments   [Skip link to Retrieve the details of all payments](https://developers.tap.company/reference/api-actions\#retrieve-the-details-of-all-payments)

If you would like to retrieve all the payments performed on your account, you can use [List All Charges](https://tappayments.readme.io/reference/getting-started-with-your-api-2). This endpoint allows you to list the payments based on various parameters such as Date Range, Status, Payment Method, Customer, and Charge ID.

## Update a payment   [Skip link to Update a payment](https://developers.tap.company/reference/api-actions\#update-a-payment)

To update the description, email and SMS notifications, or metadata of a charge, you can use the [Update a Charge API](https://developers.dev.tap.company/reference/update-a-charge). This API allows you to modify these properties of an existing charge.