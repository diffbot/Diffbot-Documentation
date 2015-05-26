# Image API
The Image API identifies the primary image(s) of a submitted web page and returns comprehensive information and metadata for each image.

## Request

> Definition

``` 
GET http://api.diffbot.com/v3/image
```

> Example Request

```shell
curl "http://api.diffbot.com/v3/image?token={token}&url=http%3A%2F%2Fwww.diffbot.com%2Fproducts%2F"
```

To use the Image API, perform a HTTP GET request on the following endpoint:



`GET http://api.diffbot.com/v3/image`
<aside class="notice">Remember to url-encode all querystring parameters!</aside>


<table class="controls table table-bordered" border="0" cellpadding="5">
  <thead><tr><th>Argument</th><th>Description</th></tr></thead>

    <tbody><tr>
        <td class="">token</td>
        <td class=" default"><div>Developer token</div></td>
    </tr>
    <tr>
        <td class="">url</td>
        <td class=" default"><div>Web page URL of the image to process (URL encoded)</div></td>
    </tr>

    <tr>
        <td colspan="2" class="header">Optional arguments</td>
    </tr>
    <tr>
        <td class="">fields</td>
        <td class=" optional"><div>Used to specify optional fields to be returned by the Image API. See the <a href="#the-fields-argument45">Fields</a> section below.</div></td>
    </tr>
    <tr>
        <td class="">timeout</td>
        <td class=" optional"><div>Set a value in milliseconds to terminate the response. By default the Image API has a 30-second (30000) timeout.</div></td>
    </tr>
    <tr>
        <td class="">callback</td>
        <td class=" optional"><div>Use for jsonp requests. Needed for cross-domain ajax.</div></td>
    </tr></tbody></table>



### The Fields Argument

Use the `fields` argument to return optional fields in the JSON response. The default fields will always be returned. For nested arrays, use parentheses to retrieve specific fields, or `*` to return all sub-fields.

For example, to return `mime` and `colors` (in addition to the default fields), your &fields argument would be:

`&fields=mime,colors`


## Response 


> If successful, you'll receive this response:

```json
{
  "request": {
    "pageUrl": "http://www.diffbot.com/products",
    "api": "image",
    "options": [],
    "fields": "",
    "version": 3
  },
  {
  "objects": [
    {
      "title": "Diffy, climbing a mountain",
      "pixelHeight": 1158,
      "diffbotUri": "image|3|-1897071612",
      "pageUrl": "http://www.diffbot.com/products",
      "humanLanguage": "en",
      "pixelWidth": 950,
      "date": "Oct 19, 2013",
      "type": "image",
      "url": "http://www.diffbot.com/images/image_diffy_sample.png",
      "size": 21625,
      "xpath": "/HTML/BODY/DIV[@class='main']/DIV[@id='primaryImage']/IMG"
    },
    {
      "title": "Diffy atop said mountain",
      "pixelHeight": 1120,
      "diffbotUri": "image|3|-1221792290",
      "pageUrl": "http://www.diffbot.com/products",
      "humanLanguage": "en",
      "pixelWidth": 920,
      "anchorUrl": "http://www.diffbot.com",
      "date": "Oct 21, 2013",
      "type": "image",
      "url": "http://www.diffbot.com/images/image_atopmountain_sample.png",
      "size": 24611,
      "xpath": "/HTML/BODY/DIV[@class='main']/DIV[@id='secondaryImage']/A/IMG"
    },
  ],
}
```




Diffbot's V3 APIs return information about **all** identified objects on a submitted page.

Each V3 response includes a `request` object (which returns request-specific metadata), and an `objects` array, which will include the extracted information for all objects on a submitted page.

Objects in the Image API's `objects` array will include the following fields:

<table class="controls table table-bordered" id="fields" border="0" cellpadding="5">
  <thead><tr><th>Field</th><th>Description</th></tr></thead>

    <tbody><tr>
        <td class="">type</td>
        <td class=" default"><div>Type of object (always <code>image</code>).</div></td>
    </tr>
    <tr>
        <td class="">url</td>
        <td class=" default"><div>Direct link to image file.</div></td>
    </tr>
    <tr>
        <td class="">title</td>
        <td class=" default"><div>Title or caption of the image, if available.</div></td>
    </tr>
    <tr>
        <td class="">height</td>
        <td class=" default"><div>Height of image as (re-)sized via browser/CSS.</div></td>
    </tr>
    <tr>
        <td class="">width</td>
        <td class=" default"><div>Width of image as (re-)sized via browser/CSS.</div></td>
    </tr>
    <tr>
        <td class="">naturalHeight</td>
        <td class=" default"><div>Raw image height, in pixels.</div></td>
    </tr>
    <tr>
        <td class="">naturalWidth</td>
        <td class=" default"><div>Raw image width, in pixels.</div></td>
    </tr>
    <tr>
        <td class="">humanLanguage</td>
        <td class=" default"><div>Returns the (spoken/human) language of the submitted page, using two-letter <a href="http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes" target="_blank">ISO 639-1 nomenclature</a>.</div></td>
    </tr>
    <tr>
        <td class="">anchorUrl</td>
        <td class=" default"><div>If the image is hyperlinked, returns the destination URL.</div></td>
    </tr>
    <tr>
        <td class="">pageUrl</td>
        <td class=" default"><div>URL of submitted page / page from which the image is extracted.</div></td>
    </tr>
    <tr>
        <td class="">resolvedPageUrl</td>
        <td class=" default"><div>Returned if the <code>pageUrl</code> redirects to another URL.</div></td>
    </tr>
    <tr>
        <td class="">xpath</td>
        <td class=" default"><div>XPath expression identifying the image node.</div></td>
    </tr>
    <tr>
        <td class="">diffbotUri</td>
        <td class=" default"><div>Unique object ID. The diffbotUri is generated from the values of various Image fields and uniquely identifies the object. This can be used for deduplication.</div></td>
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
        <td class=" optional"><div>Comma-separated list of image-embedded metadata (e.g., EXIF, XMP, ICC Profile), if available within the image file.</div></td>
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
        <td class="">mentions</td>
        <td class=" experimental"><div>Array of articles upon which the same or similar image may be found.</div></td>
    </tr>
    <tr>
        <td class="">ocr</td>
        <td class=" experimental"><div>If text is identified within the image, we will attempt to recognize the text string.</div></td>
    </tr>
    <tr>
        <td class="">faces</td>
        <td class=" experimental"><div>The x, y, height and width of coordinates of human faces. Returns null if no faces are found.</div></td>
    </tr></tbody></table>

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
curl http://api.diffbot.com/v3/image?token={token}&url=http%3A%2F%2Fwww.diffbot.com \

-H "Content-Type: text/html" \
-d '<html><body><h2>Diffy the Robot</h2><div><img src="diffy-b.png"></div></body></html>' 
```

If your content is not publicly available (e.g., behind a firewall), you can POST markup directly to the Image API endpoint for analysis:

`http://api.diffbot.com/v3/image?token={token}&url={url}`

Please note that the `url` argument is still required, and will be used to resolve any relative links contained in the markup.

Provide the content to analyze as your POST body, and specify the `Content-Type` header as `text/html`.