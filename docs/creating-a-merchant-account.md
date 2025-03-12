After successfully creating a lead, the next crucial step in onboarding a merchant with Tap is to convert the lead into an actual merchant account. This guide outlines the process and parameters involved in creating a merchant account.

## Lead Conversion   [Skip link to Lead Conversion](https://developers.tap.company/docs/creating-a-merchant-account\#lead-conversion)

The lead you've created serves as the foundation for the merchant account. Once the lead is established, it can be transformed into a full-fledged merchant account with more detailed information.

## Connect API   [Skip link to Connect API](https://developers.tap.company/docs/creating-a-merchant-account\#connect-api)

In order for the lead created to be converted, you must use the connect API in order to finish all the missing onboarding data. The connect API will return a URL that you should direct the lead to in order to complete the onboarding process.

## Merchant Response   [Skip link to Merchant Response](https://developers.tap.company/docs/creating-a-merchant-account\#merchant-response)

Upon successful conversion of a lead into a merchant account, you will receive a response that includes a unique Merchant ID and other relevant details.

Here's a sample response:

```rdmd-code lang- theme-light
{
	"id": "merchant_o8qS51***oval",
	"created": 1697989672632,
	"object": "merchant",
	"live_mode": true,
	"api_version": "v2",
	"feature_version": "v1",
	"display_name": "Qlub Test",
	"business_id": "bus_vVK7272315466x6F227o96535",
	"business_entity_id": "ent_TDErA39231547lWuu22UM96707",
	"brand_id": "brd_JGdE27231546Cg3T22pE92674",
	"wallet_id": "wal_IDErA51231547zLsT221o9c345",
	"base_currency": "AED",
	"charge_currenices": [\
		"AED"\
	],
	"country": "AE",
	"operator": {
		"id": "opr_LGRb45231537***22rF94882",
		"status": "Active",
		"created": 1697989082565,
		"object": "operator",
		"live_mode": true,
		"api_version": "v2",
		"feature_version": "v1",
		"name": "DEFAULT",
		"business_id": "bus_15yt4223153***V227x9k56",
		"business_entity_id": "ent_bLErA2***537Zcbg22KK9e383",
		"developer_id": "dev_fsfj162315***u22a89q180",
		"wallet_id": "wal_lcErA40231***BR322EB9L829",
		"is_merchant": true,
		"api_credentials": {
			"test": {
				"secret": "sk_test_h4Vi9k***7PwGcjCy81FJo",
				"public": "pk_test_5Xog9zk***I4c1SJ6nGP"
			},
			"live": {
				"secret": "sk_live_hfql0U***mR5H9S8aGZz",
				"public": "pk_live_1MnRXPjZUk***8du9c7eyVC6"
			}
		}
	},
	"is_acceptance_allowed": false,
	"is_payout_allowed": false,
	"legacy_id": "266**88",
	"marketplace": false,
	"data_status": {
		"base_currency": "editable",
		"charge_currenices": "editable",
		"acceptance_status": "editable",
		"segment": "editable",
		"country": "editable"
	},
	"data_verification": {
		"base_currency": "entered",
		"charge_currenices": "entered",
		"acceptance_status": "entered",
		"segment": "entered",
		"country": "entered"
	},
	"data_state": "incomplete",
	"terminal_id": "terminal_yPTR522***RC4O22yc9O998",
	"payment_provider": {
		"technology_id": "technology_EqJf462***g7GN84113",
		"settlement_by": "payment_facilitator_OFRE***610zDPQ160Y9I72"
	},
	"payout_status": "disabled",
	"acceptance_status": "disabled",
	"retailplatform": {
		"id": "retail_platform_Qx1X56***0lIxm10ZS9C477",
		"name": {
			"en": "ABC"
		},
		"logo": "file_1078315669600903168"
	}
}

```

The provided `merchant_o8qS51***oval` is the unique Merchant ID for this merchant account.

With the merchant account created, you can now initiate transactions and further configure the merchant's payment options.

Updated7 months ago

* * *