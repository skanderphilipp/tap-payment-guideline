Tap's Encrypted Card Token endpoint provides a secure and simple way to store sensitive credit card information. The RSA algorithm is utilized for encryption and decryption, which is an asymmetric cryptographic algorithm.

To protect the customer's card information, it's encrypted using a public key and decrypted using a secret key. Please note that these tokens can only be used once, and they can be utilized in place of a source in the Charges, Authorize, or Card API.

Apple Pay can also use this endpoint by encrypting the "decrypted Apple payment data" to generate the token.

A test encryption key is available in the Test API Keys section for experimentation. However, please be aware that a PCI compliance certificate is required to access this endpoint. For more information, please contact our team. Alternatively, you can also create tokens using our JS Elements without the need to meet PCI compliance requirements.

This is the format to encrypt the card data

Text

```rdmd-code lang-text theme-light
{"number": “5123450000000008”, "exp_month": “01”, "exp_year": “2039”, "cvc": “100”, "name": "test user"}

```

ShellNodeRubyPHPPython

Click `Try It!` to start a request and see the response here!