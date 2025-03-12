Mada supports SAR currency only.

Mada cards can be accepted on Tap's hosted solutions. It doesn't require any further redirection.

Mada payment option/logo appears automatically on our hosted solutions, along with other payment options.

**Sample Popup window**

![](https://files.readme.io/cbf9673-image_257.png)

OR, to only accept Mada cards on our hosted Payment page.

You can pass the mada source id in the payment request. "It will restrict the page for Mada only"

**Sample request**

JSON

```rdmd-code lang-json theme-light
{
...
"currency": "SAR",
"source": {
    "id": "src_sa.mada"
     },
...
}

```

Updatedover 1 year ago

* * *