Customers can save the card on the KNET server page. So, they can reuse the saved cards to make any future payments.

It needs to be enabled by the tap side, please contact the tap support team to get it enabled.

**Note** It's not available in Sandbox mode.

* * *

Pass 'cust\_' in the customer object of the [Charges API](https://developers.tap.company/docs/create-a-charge) call instead of full customer details, so the [KNET](https://developers.tap.company/docs/knet) page will show the KFAST logo as well.

JSON

```rdmd-code lang-json theme-light
	"customer": {
		"id": "cus_LV05H542l1DQ0105185"
	},

```

Customers can save the cards by clicking the terms & conditions agreement

(Use **[create a customer](https://developers.tap.company/docs/create-a-customer)** API, to get the cust\_. If no existing customer)

**Sample Page for new customer**

![](https://files.readme.io/c82f704-image_263.png)

* * *

If the same customer returns for any future payment, you can pass the same customer\_id in the payload request, and KFAST will show the saved cards list to choose from. as shown below.

**Sample page with saved cards**

![](https://files.readme.io/c3d67df-image_254.png)

Updated11 months ago

* * *