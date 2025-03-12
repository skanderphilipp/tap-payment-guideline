Introducing Tap Payment's Card JavaScript library, a powerful tool designed for crafting seamless payment experiences. This library empowers you to construct secure payment flows embedded within your web applications, enabling the collection of sensitive card information from users.

In this guide, we will walk you through the step-by-step creation of a dynamic payment form using the TAP JavaScript library, unlocking the potential for secure and user-friendly payment processing on your website.

# Requirements   [Skip link to Requirements](https://developers.tap.company/docs/card-sdk-web-v1\#requirements)

Using Elements for payment submissions requires a secure HTTPS connection. This is essential to guard against potential attacks and avoid mixed content warnings on modern browsers. Importantly, if the payment form is served over HTTP, the Elements SDK won't function correctly, compromising both security and functionality by preventing the generation of essential tokens for payment processing. In summary, maintaining an HTTPS connection is crucial for the secure and effective operation of your payment system.

> ## 🚧  For optimal security and functionality, the Card JS library must be utilized over an HTTPS connection, both in sandbox and production environments.

# Card JS Elements Features   [Skip link to Card JS Elements Features](https://developers.tap.company/docs/card-sdk-web-v1\#card-js-elements-features)

This library being our first embedded experience for accepting card payments like Visa, Mastercard and mada. This library is not just a tool; it's a comprehensive solution that enhances the security and user experience in online transactions. Here are its key features that set it apart:

1. A prebuilt UI component that not only efficiently gathers card details from customers but also tokenizes this sensitive information within the element, all without requiring interaction with your server.
2. Automatic formatting which formats card details as they are entered, streamlining the data entry process and reducing user errors.
3. Currency validation to ensuring compatibility with various global payment options, making it a versatile tool for international transactions.
4. Robust input validation with error response handling, ensuring customers are guided correctly through the payment process.
5. Real-time BIN (Bank Identification Number) response, that helps you gain immediate insights into the card type and issuing bank, adding an extra layer of verification.
6. Responsive design catering to various screen sizes and devices to ensures a seamless user experience.
7. Customizable style of the payment form that tailor the payment form's appearance, including font styles, sizes, and colors, particularly for the submit button, ensuring the form aligns perfectly with your brand's aesthetic.

# What to Expect   [Skip link to What to Expect](https://developers.tap.company/docs/card-sdk-web-v1\#what-to-expect)

Here you can see how the payment form will look like when implementing the Card JS library into your website, giving you an embedded form without requiring a redirection to Tap's hosted environment to tokenize the card and complete a payment. Moreover, in addition to having this form, you can also customize your own submit button to submit the card details once entered and then allowing you to get a token as a response which you need to use to complete the payment.

In order to see and test and fully working demo of the Card JS library, please follow this [link](https://jselements.tap.company/tapdocumentation/public/).

Tap Payment

Loading interface...

# Card JS Integration   [Skip link to Card JS Integration](https://developers.tap.company/docs/card-sdk-web-v1\#card-js-integration)

We have streamlined the process of implementing the Card JS library, by providing the integration code in HTML, CSS, and JavaScript, ensuring a straightforward and user-friendly setup. To effectively integrate this library into your website, simply follow the steps outlined below.

## Initialize and Setup Card Library   [Skip link to Initialize and Setup Card Library](https://developers.tap.company/docs/card-sdk-web-v1\#initialize-and-setup-card-library)

To begin integrating the TAP JS library, it's essential to load the SDK correctly and to provide a better experience for all screen sizes. Here is how to complete that.

### Import the Library Scripts   [Skip link to Import the Library Scripts](https://developers.tap.company/docs/card-sdk-web-v1\#import-the-library-scripts)

You can initialize the library by including a specific script in the header of your HTML webpage. This step is crucial and should be the starting point of your integration process.

HTML

```rdmd-code lang-json theme-light

<script src="https://cdnjs.cloudflare.com/ajax/libs/bluebird/3.3.4/bluebird.min.js"></script>
<script src="https://secure.gosell.io/js/sdk/tap.min.js"></script>

```

### Responsive Dimension   [Skip link to Responsive Dimension](https://developers.tap.company/docs/card-sdk-web-v1\#responsive-dimension)

To make JS element scale to dimensions of the device, You should include the following meta tag in your html header, noting that this an optional step but will provide a better user-experience when the website is accessed from different screen sizes.

HTML

```rdmd-code lang-c theme-light

<meta name="viewport" content="width=device-width, initial-scale=1.0">

```

### Referrer Policy   [Skip link to Referrer Policy](https://developers.tap.company/docs/card-sdk-web-v1\#referrer-policy)

To control the information sent in the Referer header when navigating from your site to another, you should include the following meta tag in your HTML header. This is an optional step, but it will enhance security and privacy by limiting the referrer information shared with external sites.

```rdmd-code lang- theme-light
<meta name="referrer" content="origin-when-crossorigin">

```

## Create the Payment Form   [Skip link to Create the Payment Form](https://developers.tap.company/docs/card-sdk-web-v1\#create-the-payment-form)

To securely collect card details from your customers, Elements creates UI components for you that are hosted by Tap payments. They are then placed into your payment form, rather than you creating them directly. To determine where to insert these components, create empty DOM elements (containers) with unique IDs within your payment form.

HTML

```rdmd-code lang-json theme-light

<form id="form-container" method="post" action="/charge">
  <!-- Tap element will be here -->
  <div id="element-container"></div>
  <div id="error-handler" role="alert"></div>
  <div id="success" style=" display: none;;position: relative;float: left;">
        Success! Your token is <span id="token"></span>
  </div>
  <!-- Tap pay button -->
  <button id="tap-btn">Submit</button>
</form>

```

## Style the Payment Form   [Skip link to Style the Payment Form](https://developers.tap.company/docs/card-sdk-web-v1\#style-the-payment-form)

To style the payment form and also the submit button, you need to add some CSS into your code. It is worth noting that the styling of the form is up to you, and below is an example to start with.

CSS

```rdmd-code lang-css theme-light

.form-row {
    width: 70%;
    float: left;
    background-color: #ededed;
}
#card-element {
background-color: transparent;
height: 40px;
border-radius: 4px;
border: 1px solid transparent;
box-shadow: 0 1px 3px 0 #e6ebf1;
-webkit-transition: box-shadow 150ms ease;
transition: box-shadow 150ms ease;
}

#card-element--focus {
  box-shadow: 0 1px 3px 0 #cfd7df;
}

#card-element--invalid {
  border-color: #fa755a;
}

#card-element--webkit-autofill {
  background-color: #fefde5 !important;
}

#submitbutton,#tap-btn{
align-items:flex-start;
background-attachment:scroll;background-clip:border-box;
background-color:rgb(50, 50, 93);background-image:none;
background-origin:padding-box;
background-position-x:0%;
background-position-y:0%;
background-size:auto;
border-bottom-color:rgb(255, 255, 255);
border-bottom-left-radius:4px;
border-bottom-right-radius:4px;border-bottom-style:none;
border-bottom-width:0px;border-image-outset:0px;
border-image-repeat:stretch;border-image-slice:100%;
border-image-source:none;border-image-width:1;
border-left-color:rgb(255, 255, 255);
border-left-style:none;
border-left-width:0px;
border-right-color:rgb(255, 255, 255);
border-right-style:none;
border-right-width:0px;
border-top-color:rgb(255, 255, 255);
border-top-left-radius:4px;
border-top-right-radius:4px;
border-top-style:none;
border-top-width:0px;
box-shadow:rgba(50, 50, 93, 0.11) 0px 4px 6px 0px, rgba(0, 0, 0, 0.08) 0px 1px 3px 0px;
box-sizing:border-box;color:rgb(255, 255, 255);
cursor:pointer;
display:block;
float:left;
font-family:"Helvetica Neue", Helvetica, sans-serif;
font-size:15px;
font-stretch:100%;
font-style:normal;
font-variant-caps:normal;
font-variant-east-asian:normal;
font-variant-ligatures:normal;
font-variant-numeric:normal;
font-weight:600;
height:35px;
letter-spacing:0.375px;
line-height:35px;
margin-bottom:0px;
margin-left:12px;
margin-right:0px;
margin-top:28px;
outline-color:rgb(255, 255, 255);
outline-style:none;
outline-width:0px;
overflow-x:visible;
overflow-y:visible;
padding-bottom:0px;
padding-left:14px;
padding-right:14px;
padding-top:0px;
text-align:center;
text-decoration-color:rgb(255, 255, 255);
text-decoration-line:none;
text-decoration-style:solid;
text-indent:0px;
text-rendering:auto;
text-shadow:none;
text-size-adjust:100%;
text-transform:none;
transition-delay:0s;
transition-duration:0.15s;
transition-property:all;
transition-timing-function:ease;
white-space:nowrap;
width:150.781px;
word-spacing:0px;
writing-mode:horizontal-tb;
-webkit-appearance:none;
-webkit-font-smoothing:antialiased;
-webkit-tap-highlight-color:rgba(0, 0, 0, 0);
-webkit-border-image:none;

}

```

## Load the Library using JavaScript   [Skip link to Load the Library using JavaScript](https://developers.tap.company/docs/card-sdk-web-v1\#load-the-library-using-javascript)

To effectively utilize the Card JS library, begin by creating an instance of an Element in JavaScript once your form is loaded. This instance should be mounted onto the Element container you've previously set up. The main action of this process is the use of a public key provided by Tap, which grants access to the JS library and links it to your specific TAP account. Ensure you pass this public key as a parameter when calling `Tapjsli()`.

Once you pass your account's public key in the `Tapjsli()`, and the payment form loads, it will show you to the left all the card payments logos that are enabled on your account. Add the below JavaScript code to complete this step.

JavaScript

```rdmd-code lang-json theme-light

//pass your public key from tap's dashboard
var tap = Tapjsli('pk_test_EtHFV4BuPQokJT6jiROls87Y');

var elements = tap.elements({});

var style = {
  base: {
    color: '#535353',
    lineHeight: '18px',
    fontFamily: 'sans-serif',
    fontSmoothing: 'antialiased',
    fontSize: '16px',
    '::placeholder': {
      color: 'rgba(0, 0, 0, 0.26)',
      fontSize:'15px'
    }
  },
  invalid: {
    color: 'red'
  }
};
// input labels/placeholders
var labels = {
    cardNumber:"Card Number",
    expirationDate:"MM/YY",
    cvv:"CVV",
    cardHolder:"Card Holder Name"
  };
//payment options
var paymentOptions = {
  currencyCode:["KWD","USD","SAR"], //change the currency array as per your requirement
  labels : labels,
  TextDirection:'ltr', //only two values valid (rtl, ltr)
  paymentAllowed: ['VISA', 'MASTERCARD', 'AMERICAN_EXPRESS', 'MADA'] //default string 'all' to show all payment methods enabled on your account
}
//create element, pass style and payment options
var card = elements.create('card', {style: style},paymentOptions);
//mount element
card.mount('#element-container');
//card change event listener
card.addEventListener('change', function(event) {
  if(event.loaded){ //If ‘true’, js library is loaded
    console.log("UI loaded :"+event.loaded);
    console.log("current currency is :"+card.getCurrency())
  }
  var displayError = document.getElementById('error-handler');
  if (event.error) {
    displayError.textContent = event.error.message;
  } else {
    displayError.textContent = '';
  }
});

```

### Get Card BIN Details   [Skip link to Get Card BIN Details](https://developers.tap.company/docs/card-sdk-web-v1\#get-card-bin-details)

The first six digits of a credit or debit card number are known as the "Bank Identification Number (BIN)," which are essential for identifying the card's issuing bank and other related details. The TAP JS Card library is equipped to retrieve this BIN information in real-time. To leverage this feature in your application, ensure that your code includes the below specific condition that should be added in the code that was shared in the previous step in `card.addEventListener() ` as below, that triggers the retrieval of BIN details.

The condition stating if(event.BIN) {} shown in the JavaScript tab will display in the console of your website the card details related to the BIN added in the card form as shown in tab BIN Result.

JavaScriptBIN Result

```rdmd-code lang-groovy theme-light

card.addEventListener('change', function(event) {
  if(event.BIN){
    console.log(event.BIN)
  }
  var displayError = document.getElementById('card-errors');
  if (event.error) {
    displayError.textContent = event.error.message;
  } else {
    displayError.textContent = '';
  }
});

```

```rdmd-code lang-json theme-light

{
   "bin":"424242",
   "bank":"",
   "card_brand":"VISA",
   "card_type":"CREDIT",
   "card_category":"",
   "card_scheme":"VISA",
   "country_name":"UNITED KINGDOM",
   "country":"GB",
   "website":"",
   "phone":"",
   "address_required":false,
   "api_version":"V2"
}

```

## Tokenize the Card Details   [Skip link to Tokenize the Card Details](https://developers.tap.company/docs/card-sdk-web-v1\#tokenize-the-card-details)

Transforming the payment details collected through Elements into a token is an essential step in the process. To accomplish this, set up an event handler that manages the submit event on the form. This handler is responsible for transmitting the fields to TAP for tokenization and strategically prevents the form's default submission. The form submission is done through JavaScript in the subsequent step, ensuring a controlled and secure process of token generation for your payment transactions.

As you can see in the below step, the function `tap.createToken()` provides a Promise, offering a straightforward outcome:

1. **result.id**: Successful creation of a Token.
2. **result.error**: An indication of an error, including any client-side validation issues.

JavaScript

```rdmd-code lang-json theme-light

// Handle form submission
var form = document.getElementById('form-container');
form.addEventListener('submit', function(event) {
  event.preventDefault();

  tap.createToken(card).then(function(result) {
    console.log(result);
    if (result.error) {
      // Inform the user if there was an error
      var errorElement = document.getElementById('error-handler');
      errorElement.textContent = result.error.message;
    } else {
      // Send the token to your server
      var errorElement = document.getElementById('success');
      errorElement.style.display = "block";
      var tokenElement = document.getElementById('token');
      tokenElement.textContent = result.id;
    tapTokenHandler(token)

    }
  });
});

```

## Submit the Token to your Server   [Skip link to Submit the Token to your Server](https://developers.tap.company/docs/card-sdk-web-v1\#submit-the-token-to-your-server)

To conclude the integration of the Card JS library, the last step is to submit the generated token, along with any additional collected information, to your server. In the previous step, you can see in the code the function `tapTokenHandler()` has been called to handle the submission of the token, and below is the code used to complete this functionalitiy.

JavaScript

```rdmd-code lang-less theme-light

function tapTokenHandler(token) {
  // Insert the token ID into the form so it gets submitted to the server
  var form = document.getElementById('payment-form');
  var hiddenInput = document.createElement('input');
  hiddenInput.setAttribute('type', 'hidden');
  hiddenInput.setAttribute('name', 'tapToken');
  hiddenInput.setAttribute('value', token.id);
  form.appendChild(hiddenInput);

  // Submit the form
  form.submit();
}

```

Updated5 months ago

* * *

Did this page help you?

Yes

No