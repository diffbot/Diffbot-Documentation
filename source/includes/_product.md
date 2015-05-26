# Product API
The Product API automatically extracts complete data from any shopping or e-commerce product page. Retrieve full pricing information, product IDs (SKU, UPC, MPN), images, product specifications, brand and more.

## Request

> Definition

``` 
GET http://api.diffbot.com/v3/product
```

> Example Request

```shell
curl "http://api.diffbot.com/v3/product?token={token}&url=http%3A%2F%2Fus.levi.com%2Fproduct%2Findex.jsp%3FproductId%3D2076855"
```

To use the Product API, perform a HTTP GET request on the following endpoint:


`GET http://api.diffbot.com/v3/product`
<aside class="notice">Remember to url-encode all querystring parameters!</aside>


<table class="controls table table-bordered" border="0" cellpadding="5">
    <thead><tr><th>Argument</th><th>Description</th></tr></thead>

        <tbody><tr>
            <td class="">token</td>
            <td class=" default"><div>Developer token</div></td>
        </tr>
        <tr>
            <td class="">url</td>
            <td class=" default"><div>Web page URL of the article to process (URL encoded)</div></td>
        </tr>

        <tr>
            <td colspan="2" class="header">Optional arguments</td>
        </tr>
        <tr>
            <td class="">fields</td>
            <td class=" optional"><div>Used to specify optional fields to be returned by the Product API. See the <a href="#the-fields-argument34">Fields</a> section below.</div></td>
        </tr>
        <tr>
            <td class="">discussion</td>
            <td class=" optional"><div>Pass <code>discussion=false</code> to disable automatic extraction of article comments. See <a href="#discussion">below</a>.</div></td>
        </tr>
        <tr>
            <td class="">timeout</td>
            <td class=" optional"><div>Set a value in milliseconds to terminate the response. By default the Product API has a 30-second (30000) timeout.</div></td>
        </tr>
        <tr>
            <td class="">callback</td>
            <td class=" optional"><div>Use for jsonp requests. Needed for cross-domain ajax.</div></td>
        </tr></tbody></table>


### The Fields Argument

Use the `fields` argument to return optional fields in the JSON response. The default fields will always be returned. For nested arrays, use parentheses to retrieve specific fields, or * to return all sub-fields.

For example, to return `links` and `meta` (in addition to the default fields), your &fields argument would be:

`&fields=links,meta`


## Response 


> If successful, you'll receive this response:

```json
{
  "request": {
    "pageUrl": "http://store.livrada.com/collections/all/products/before-i-go-to-sleep",
    "api": "product",
    "options": [],
    "fields": "title,text,offerPrice,regularPrice,saveAmount,pageUrl,images",
    "version": 3
  },
  {
  "objects": [
    {
      "type": "product",
      "title": "Before I Go To Sleep",
      "text": "Memories define us. So what if you lost yours every time you went to sleep? Your name, your identity, your past, even the people you love -- all forgotten overnight. And the one person you trust may be telling you only half the story. Before I Go To Sleep is a disturbing psychological thriller in which an amnesiac desperately tries to uncover the truth about who she is and who she can trust.",
      "offerPrice": "$7.99",
      "regularPrice": "$9.99",
      "saveAmount": "$2.00",
      "pageUrl": "http://store.livrada.com/collections/all/products/before-i-go-to-sleep",
      "images": [
        {
          "title": "Before I Go to Sleep cover",
          "url": "http://cdn.shopify.com/s/files/1/0184/6296/products/BeforeIGoToSleep_large.png?946",
          "xpath": "/HTML[@class='no-js']/BODY[@id='page-product']/DIV[@class='content-frame']/DIV[@class='content']/DIV[@class='content-shop']/DIV[@class='row']/DIV[@class='span5']/DIV[@class='product-thumbs']/UL/LI[@class='first-image']/A[@class='single_image']/IMG",
          "diffbotUri": "image|1|768070723"
        }
      ]
      "diffbotUri": "product|1|937176621"
    }
  ],
}
```

Diffbot's V3 APIs return information about **all** identified objects on a submitted page.

Each V3 response includes a `request` object (which returns request-specific metadata), and an `objects` array, which will include the extracted information for all objects on a submitted page. 

Objects in the Product API's `objects` array will include the following fields:
<table class="controls table table-bordered" id="fields" border="0" cellpadding="5">
  <thead><tr><th>Field</th><th>Description</th></tr></thead>

        <tbody><tr>
            <td class="">type</td>
            <td class=" default"><div>Type of <code>object</code> (always product).</div></td>
        </tr>
        <tr>
            <td class="">pageUrl</td>
            <td class=" default"><div>URL of submitted page / page from which the product is extracted.</div></td>
        </tr>
        <tr>
            <td class="">resolvedPageUrl</td>
            <td class=" default"><div>Returned if the <code>pageUrl</code> redirects to another URL.</div></td>
        </tr>
        <tr>
            <td class="">title</td>
            <td class=" default"><div>Title of the product.</div></td>
        </tr>
        <tr>
            <td class="">text</td>
            <td class=" default"><div>Text description, if available, of the product.</div></td>
        </tr>
        <tr>
            <td class="">brand</td>
            <td class=" default"><div>Item's brand name.</div></td>
        </tr>
        <tr>
            <td class="">offerPrice</td>
            <td class=" default"><div>Offer or actual/final price of the product.</div></td>
        </tr>
        <tr>
            <td class="">regularPrice</td>
            <td class=" default"><div>Regular or original price of the product, if available.</div></td>
        </tr>
        <tr>
            <td class="">shippingAmount</td>
            <td class=" default"><div>Shipping price.</div></td>
        </tr>
        <tr>
            <td class="">saveAmount</td>
            <td class=" default"><div>Discount or amount saved off the regular price.</div></td>
        </tr>
        <tr>
            <td class="parent">priceRange</td>
            <td class="parent default"><div>If the product is available in a range of prices, the minimum and maximum values will be returned. The lowest price will also be returned as the <code>offerPrice</code>.</div></td>
        </tr>
        <tr>
            <td class="priceRange indent">minPrice</td>
            <td class="priceRange indent default"><div>The minimum price for the offered item.</div></td>
        </tr>
        <tr>
            <td class="priceRange indent">maxPrice</td>
            <td class="priceRange indent default"><div>The maximum price for the offered item.</div></td>
        </tr>
        <tr>
            <td class="parent">quantityPrices</td>
            <td class="parent default"><div>If the product is available with quantity-based discounts, all identifiable price points will be returned. The lowest price will also be returned as the <code>offerPrice</code>.</div></td>
        </tr>
        <tr>
            <td class="quantityPrices indent">minQuantity</td>
            <td class="quantityPrices indent default"><div>The minimum quantity required to purchase for the associated price.</div></td>
        </tr>
        <tr>
            <td class="quantityPrices indent">price</td>
            <td class="quantityPrices indent default"><div>Price of the specific quantity level.</div></td>
        </tr>
        <tr>
            <td class="">offerPriceDetails</td>
            <td class=" default"><div><code>offerPrice</code> separated into its constituent parts: <code>amount</code>, <code>symbol</code>, and full <code>text</code>.</div></td>
        </tr>
        <tr>
            <td class="">regularPriceDetails</td>
            <td class=" default"><div><code>regularPrice</code> separated into its constituent parts: <code>amount</code>, <code>symbol</code>, and full <code>text</code>.</div></td>
        </tr>
        <tr>
            <td class="">saveAmountDetails</td>
            <td class=" default"><div><code>saveAmount</code> separated into its constituent parts: <code>amount</code>, <code>symbol</code>, full <code>text</code>, and whether or not it is a <code>percentage</code> value.</div></td>
        </tr>
        <tr>
            <td class="">productId</td>
            <td class=" default"><div>Diffbot-determined unique product ID. If <code>upc</code>, <code>isbn</code>, <code>mpn</code> or <code>sku</code> are identified on the page, productId will select from these values in the above order.</div></td>
        </tr>
        <tr>
            <td class="">upc</td>
            <td class=" default"><div>Universal Product Code (UPC/EAN), if available.</div></td>
        </tr>
        <tr>
            <td class="">sku</td>
            <td class=" default"><div>Stock Keeping Unit -- store/vendor inventory number or identifier.</div></td>
        </tr>
        <tr>
            <td class="">mpn</td>
            <td class=" default"><div>Manufacturer's Product Number.</div></td>
        </tr>
        <tr>
            <td class="">isbn</td>
            <td class=" default"><div>International Standard Book Number (ISBN), if available.</div></td>
        </tr>
        <tr>
            <td class="">specs</td>
            <td class=" default"><div>If a specifications table or similar data is available on the product page, individual specifications will be returned in the <code>specs</code> object as name/value pairs. Names will be normalized to lowercase with spaces replaced by underscores, e.g. <code>display_resolution</code>.</div></td>
        </tr>
        <tr>
            <td class="parent">images</td>
            <td class="parent default"><div>Array of images, if present within the product.</div></td>
        </tr>
        <tr>
            <td class="images indent">url</td>
            <td class="images indent default"><div>Fully resolved link to image.</div></td>
        </tr>
        <tr>
            <td class="images indent">title</td>
            <td class="images indent default"><div>Description or caption of the image.</div></td>
        </tr>
        <tr>
            <td class="images indent">naturalHeight</td>
            <td class="images indent default"><div>Raw image height, in pixels.</div></td>
        </tr>
        <tr>
            <td class="images indent">naturalWidth</td>
            <td class="images indent default"><div>Raw image width, in pixels.</div></td>
        </tr>
        <tr>
            <td class="images indent">primary</td>
            <td class="images indent default"><div>Returns <code>true</code> if image is identified as primary based on visual analysis.</div></td>
        </tr>
        <tr>
            <td class="images indent">xpath</td>
            <td class="images indent default"><div>XPath expression identifying the image node.</div></td>
        </tr>
        <tr>
            <td class="images indent">diffbotUri</td>
            <td class="images indent default"><div>Internal ID used for indexing.</div></td>
        </tr>
        <tr>
            <td class="">discussion</td>
            <td class=" default"><div>Product reviews, as extracted by the Diffbot Discussion API. See <a href="#discussion">below</a>.</div></td>
        </tr>
        <tr>
            <td class="">prefixCode</td>
            <td class=" default"><div>Country of origin as identified by UPC/ISBN.</div></td>
        </tr>
        <tr>
            <td class="">productOrigin</td>
            <td class=" default"><div>If available, two-character ISO country code where the product was produced.</div></td>
        </tr>
        <tr>
            <td class="">humanLanguage</td>
            <td class=" default"><div>Returns the (spoken/human) language of the submitted page, using two-letter <a href="http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes" target="_blank">ISO 639-1 nomenclature</a>.</div></td>
        </tr>
        <tr>
            <td class="">diffbotUri</td>
            <td class=" default"><div>Unique object ID. The <code>diffbotUri</code> is generated from the values of various Product fields and uniquely identifies the object. This can be used for deduplication.</div></td>
        </tr>

        <tr>
            <td colspan="2" class="header">Optional fields, available using <code>fields=</code> argument</td>
        </tr>
        <tr>
            <td class="">links</td>
            <td class=" optional"><div>Returns a top-level object (<code>links</code>) containing all hyperlinks found on the page.</div></td>
        </tr>
        <tr>
            <td class="">meta</td>
            <td class=" optional"><div>Returns a top-level object (<code>meta</code>) containing the full contents of page <code>meta</code> tags, including sub-arrays for <a href="http://ogp.me/" target="_new">OpenGraph</a> tags, <a href="https://dev.twitter.com/docs/cards/markup-reference" target="_new">Twitter Card</a> metadata, <a href="http://www.schema.org" target="_new">schema.org</a> microdata, and -- if available -- <a href="http://www.oembed.com" target="_new">oEmbed</a> metadata.</div></td>
        </tr>
        <tr>
            <td class="">querystring</td>
            <td class=" optional"><div>Returns any key/value pairs present in the URL querystring. Items without a discrete value will be returned as <code>true</code>.</div></td>
        </tr>
        <tr>
            <td class="">breadcrumb</td>
            <td class=" optional"><div>Returns a top-level array (<code>breadcrumb</code>) of URLs and link text from page breadcrumbs.</div></td>
        </tr>

        <tr>
            <td colspan="2" class="header">The following fields are in an early beta stage:</td>
        </tr>
        <tr>
            <td class="">availability</td>
            <td class=" experimental"><div>Item's availability, either <code>true</code> or <code>false</code>.</div></td>
        </tr>
        <tr>
            <td class="">colors</td>
            <td class=" experimental"><div>Returns array of product color options.</div></td>
        </tr>
        <tr>
            <td class="">size</td>
            <td class=" experimental"><div>Size(s) available, if identified on the page.</div></td>
        </tr></tbody></table>




<aside class="success">
Remember — a happy robot is an authenticated robot!
</aside>

### Review Extraction

By default the Product API will attempt to extract user reviews from product pages, using integrated functionality from the Diffbot Discussion API. (This behavior can be disabled using the argument `discussion=false`.)

Comment data will be returned in the `discussion` object (nested within the primary product object). The full syntax for discussion data is [available in the Discussion API documentation](#discussion-api).
                                                 

## Options


### Authentication

You can supply Diffbot with basic authentication credentials or custom HTTP headers (see below) to access intranet pages or other sites that require a login.

### Basic Authentication
To access pages that require a login/password ([using basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication)), include the username and password in your `url` parameter, e.g.: `url=http%3A%2F%2FUSERNAME:PASSWORD@www.diffbot.com`.

### Custom HTTP Headers

You can supply Diffbot APIs with custom values for the user-agent, referer, cookie, or accept-language values in the HTTP request. These will be used in place of the Diffbot default values.

To provide custom headers, pass in the following values in your own headers when calling the Diffbot API:

Header | Description
--------- | -----------
X-Forward-User-Agent | Will be used as Diffbot's `User-Agent` header when making your request.
X-Forward-Referer | Will be used as Diffbot's `Referer` header when making your request.
X-Forward-Cookie | Will be used as Diffbot's `Cookie` header when making your request.
X-Forward-Accept-Language | Will be used as Diffbot's `Accept-Language` header when making your request.


### Posting Content


> HTML Post Sample:

```
curl http://api.diffbot.com/v3/product?token={}&url=http%3A%2F%2Fstore.diffbot.com \

-H "Content-Type: text/html" \
-d '<html><head><title>Something to Buy</title></head><body><h2>A Pair of Jeans</h2><div>Price: $31.99</div></body></html>' 

    
```



If your content is not publicly available (e.g., behind a firewall), you can POST markup or plain text directly to the Product API endpoint for analysis:

`http://api.diffbot.com/v3/product?token={token}&url={url}`

Please note that if you submit HTML, the `url` argument is still required, and will be used to resolve any relative links contained in the markup.

Provide the content to analyze as your POST body, and specify the `Content-Type` header as `text/html` (for full markup) or `text/plain` (for text-only).

