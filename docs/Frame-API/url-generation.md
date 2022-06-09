---
title: URL Generation
---

# URL Generation

Frame API is an `<iframe>` solution for merchants. 

## Frame Validation

All generated URLs are valid for 20 minutes. Then you need to create it again.

## Supported browsers

Frame API is a critical payment service, which requires up-to-date security. For this reason, we support all major browsers that are still officially maintained and receiving security updates.

We support:

* Internet Explorer (IE11+) and Edge
* Chrome, Safari and Firefox on all devices

| Browser                              | Version | Release date |         |        |      Usage |
| ------------------------------------ | ------: | -----------: | ------: | -----: | ---------: |
|                                      |         |              | desktop | mobile |    overall |
| Chrome   |     49+ |      03/2016 | 25.65%  | 38.33% |     63.98% |
|  Safari   |     10+ |      09/2016 |  4.63%  | 14.96% |     19.59% |
|  Edge       |     79+ |      01/2020 |  3.95%  |    n/a |      3.95% |
|  Firefox |     53+ |      04/2017 |  3.40%  |   .30% |      3.70% |
|      |     36+ |      03/2016 |  1.44%  |   .01% |      1.45% |
|                                      |         |              |         |        | __92.67%__ |

If you discover any issues with the supported browsers, or would like to report a bug, please get in touch

## Create URL

Creating a URL with the Frame API is extremely simple. To get this URL, you need to request your own back-end. For your security, you should **not** share the API Key with end users.

```http
POST /v1/frame/generate/url HTTP/1.1
Host: sandbox.paybin.io
Content-Type: application/json
X-Api-Key: YOUR_API_KEY

Body:
{
      "PublicKey": "82be6167-6c31-4255-b58e-6a16aac1e4bf",
      "PaymentReference": "YOUR_MEMBER_IDENTIFIER or ORDER_ID",
      "RedirectUri": "https://mymerchantsite.com"
      "Amount": "100.00",
      "Currency": "GBP",
      "Language": "en",
      "IPAddress": "86.134.31.33"
}
```

This is a sample response. You can set it as a DOM object parameter (button, div, anchor) with the `data-url` key. For more detail check our sample NextJS repository on GitHub.


```json
{ 
   "apiVersion": "1.0.0.0", 
   "data": { 
         "url": "https://sandbox.paybin.io/payments?q=2ZP9E4Jc3YczXiKVciyxFr..." 
   },
   "statusCode": 200
}
```

### HTML and JavaScript

To construct an iframe URL, you must include two parameters. `data-reference` and `data-url` The member identifier can be a string, an integer, or anything else. When a member deposit is successful, the member value will be served on your callback endpoint.



=== "HTML"


    ``` html
    <button id="paybin" data-url={json.data.url}
            data-reference={json.data.reference}>
                  <h3>Pay with PayBin</h3>
      </button> <!--(1)-->
    ```

    1.  These values `data-url` and `data-reference` should populate on your backend. You can use your member id or order id as `data-reference`. DOM object can be anchor, button or anything else.

    

=== "JavaScript"

    If you want to use auto iframe action  add this in header or footer 

    ``` html
    <script src="https://static.paybin.io/js/paybin.min.js"></script> <!--(1)--> 
    ``` 

    1.  If you don't want to embed this javascript you should open the iframe url manually.


