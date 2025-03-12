This step-by-step documentation will guide you through the process of integrating Tabby with tap Payments. Tabby is a buy now, pay later service that allows customers to make purchases and pay in installments. By integrating Tabby with tap Payments, you can offer flexible payment options to your customers. This documentation provides detailed instructions on how to integrate Tabby using Tabby Installment Source ID, sending a sample request to Tabby, and handling the response.

## Set the Tabby Installment Source ID as follows   [Skip link to Set the Tabby Installment Source ID as follows](https://developers.tap.company/docs/tabby\#set-the-tabby-installment-source-id-as-follows)

**src\_tabby.installement**

## Send a Sample Request to Tabby for Installment   [Skip link to Send a Sample Request to Tabby for Installment](https://developers.tap.company/docs/tabby\#send-a-sample-request-to-tabby-for-installment)

Make a POST request to [Charges API](https://developers.tap.company/docs/create-a-charge) with a sample request payload. This payload should include the necessary information such as amount, currency, customer details, and other relevant data. See the sample request provided in the documentation.

JSON

```rdmd-code lang-json theme-light
	"source": {
		"id": "src_tabby.installement"
	},

```

## Receive the Sample Response from Tabby   [Skip link to Receive the Sample Response from Tabby](https://developers.tap.company/docs/tabby\#receive-the-sample-response-from-tabby)

Tabby will respond with a JSON object containing the information about the transaction. This response includes details like transaction status, URL, and other relevant data. Refer to the sample response provided in the documentation.

> ## 📘  The minimum amount for Tabby is 10 SAR,AED or 1 KD

## Redirect Customer and Complete Payment Process   [Skip link to Redirect Customer and Complete Payment Process](https://developers.tap.company/docs/tabby\#redirect-customer-and-complete-payment-process)

The merchant needs to redirect the customer to the transaction URL provided in the tap response. The customer will be directed to a payment page where they can complete the payment using Tabby. Once the customer completes the payment, they will be redirected to the redirect URL specified in the Tabby response.

Additionally, the tap response will be sent to the webhook URL, which is the post URL provided in the Tabby request. You can handle the tap response at the webhook URL to perform any necessary actions in your application.

> ## ❗️  You have to pass the valid mobile number with the country code as for Tabby, valid mobile number is required.

Updated12 months ago

* * *