Tap provides the common **TEST API credentials** to start the integration.

However, we recommend using your own test API keys, which are available under your dashboard.

## Test API Keys   [Skip link to Test API Keys](https://developers.tap.company/reference/testing-keys\#test-api-keys)

Secret KeyPublishable KeyEncryption Key

```rdmd-code lang-json theme-light
sk_test_XKokBfNWv6FIYuTMg5sLPjhJ

```

```rdmd-code lang-json theme-light
pk_test_EtHFV4BuPQokJT6jiROls87Y

```

```rdmd-code lang-json theme-light
\-----BEGIN PUBLIC KEY----- MIIBIDANBgkqhkiG9w0BAQEFAAOCAQ0AMIIBCAKCAQEA21z7Vcrrraiksj31If5K f7XGv6QNoHP7SRPjxxbxAnPrrI597NI683pHIaIgb0UNaOUggU6FYN+w+tBc1Mwk 1aOBsM8Ok6W0SsFxpa+Jt3VdOfF4iBw7k4sdd+EP5PfaiFdbrndRcCmV32mb87+I cuzDRxyqgl1Bx0dCPqmw0YCCWTuM+LXN60MHr56M5WO7J64AXn5YVzspZkon4Leg d9QbycUC77e/MUmhZL5QcGvXaBYWS5Lw5ROhjMYrLK15f4gWoYLtDcUTtMEEEtef EF4tus0Vx7XTrHa9vGbH9qUmH5F9HUkYOUX+UaFj7qVdfaR/VecB5xCwrt5ixV6y 3QIBEQ== -----END PUBLIC KEY-----

```

| Secret API key | Publishable API Key | Encryption Key |
| --- | --- | --- |
| The Secret API key is used for all the API calls on the server side. | The Publishable API key is used in the JS Elements to create the Token id and used in the JS<br>Checkout page. | This key is used for the encryption of sensitive card data before calling the Token API. |