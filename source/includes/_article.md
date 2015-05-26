# Article API
The Article API is used to extract clean article text and other data from news articles, blog posts and other text-heavy pages. Retrieve the full-text, cleaned and normalized HTML, related images and videos, author, date, tags—automatically, from any article on any site.

## Request

> Definition

``` 
GET http://api.diffbot.com/v3/article
```

> Example Request

```shell
curl "http://api.diffbot.com/v3/article?token={token}&url=http%3A%2F%2Fblog.diffbot.com%2Fdiffbots-new-product-api-teaches-robots-to-shop-online"
```

To use the Article API, perform a HTTP GET request on the following endpoint:


`GET http://api.diffbot.com/v3/article`
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
            <td class=" optional"><div>Used to specify optional fields to be returned by the Article API. See the <a href="#the-fields-argument">Fields</a> section below.</div></td>
        </tr>
        <tr>
            <td class="">paging</td>
            <td class=" optional"><div>Pass <code>paging=false</code> to disable automatic concatenation of multiple-page articles. (By default, Diffbot will concatenate up to 20 pages of a single article.) <a href="http://support.diffbot.com/automatic-apis/handling-multiple-page-articles">More on automatic concatenation</a>.</div></td>
        </tr>
        <tr>
            <td class="">maxTags</td>
            <td class=" optional"><div>Set the maximum number of automatically-generated tags to return. By default a maximum of five tags will be returned.</div></td>
        </tr>
        <tr>
            <td class="">discussion</td>
            <td class=" optional"><div>Pass <code>discussion=false</code> to disable automatic extraction of article comments. See <a href="#discussion">below</a>.</div></td>
        </tr>
        <tr>
            <td class="">timeout</td>
            <td class=" optional"><div>Set a value in milliseconds to terminate the response. By default the Article API has a 30-second (30000) timeout.</div></td>
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
    "pageUrl": "http://blog.diffbot.com/diffbots-new-product-api-teaches-robots-to-shop-online", 
    "api": "article", 
    "resolvedPageUrl": "http://blog.diffbot.com/diffbots-new-product-api-teaches-robots-to-shop-online/", 
    "version": 3
  }, 
  "objects": [
    {
      "tags": [
        {
          "id": 4688313, 
          "count": 2, 
          "prevalence": 0.6666666666666666, 
          "label": "Diffbot", 
          "type": "organization", 
          "uri": "http://dbpedia.org/resource/Diffbot"
        }, 
        {
          "id": 178604, 
          "count": 5, 
          "prevalence": 1.6666666666666667, 
          "label": "Application programming interface", 
          "uri": "http://dbpedia.org/resource/Application_programming_interface"
        }, 
        {
          "id": 4242167, 
          "count": 1, 
          "prevalence": 0.3333333333333333, 
          "label": "Stock keeping unit", 
          "uri": "http://dbpedia.org/resource/Stock_keeping_unit"
        }
      ], 
      "author": "John Davi", 
      "text": "Diffbot's human wranglers are proud today to announce the release of our newest product: an API for\u2026 products!\nThe Product API can be used for extracting clean, structured data from any e-commerce product page. It automatically makes available all the product data you'd expect: price, discount/savings amount, shipping cost, product description, any relevant product images, SKU and/or other product IDs.\nEven cooler: pair the Product API with Crawlbot, our intelligent site-spidering tool, and let Diffbot determine which pages are products, then automatically structure the entire catalog. Here's a quick demonstration of Crawlbot at work:\nWe've developed the Product API over the course of two years, building upon our core vision technology that's extracted structured data from billions of web pages, and training our machine learning systems using data from tens of thousands of unique shopping sites. We can't wait for you to try it out.\nWhat are you waiting for? Check out the Product API documentation and dive on in! If you need a token, check out our pricing and plans (including our Free plan).\nQuestions? Hit us up at support@diffbot.com.", 
      "title": "Diffbot's New Product API Teaches Robots to Shop Online", 
      "diffbotUri": "article|3|-820542508", 
      "pageUrl": "http://blog.diffbot.com/diffbots-new-product-api-teaches-robots-to-shop-online", 
      "videos": [
        {
          "diffbotUri": "video|3|-761237582", 
          "primary": true, 
          "url": "http://www.youtube.com/embed/lfcri5ungRo?feature=oembed"
        }
      ], 
      "authorUrl": "http://blog.diffbot.com/author/johndavi/", 
      "humanLanguage": "en", 
      "html": "<p>Diffbot&rsquo;s human wranglers are proud today to announce the release of our newest product: an API for&hellip; products!</p>\n<p>The&nbsp;<a href=\"http://www.diffbot.com/products/automatic/product\">Product API</a>&nbsp;can be used for extracting clean, structured data from any e-commerce product page. It&nbsp;automatically makes available all the product data you&rsquo;d expect: price, discount/savings amount, shipping cost, product description, any relevant product images, SKU and/or other product IDs.</p>\n<p>Even cooler: pair the Product API with <a href=\"http://www.diffbot.com/products/crawlbot\">Crawlbot</a>, our intelligent site-spidering tool, and let Diffbot determine which pages are products, then automatically structure the entire catalog. Here&rsquo;s a quick demonstration of Crawlbot at work:</p>\n<figure><iframe frameborder=\"0\" src=\"http://www.youtube.com/embed/lfcri5ungRo?feature=oembed\"></iframe></figure>\n<p>We&rsquo;ve developed the Product API over the course of two years, building upon our core vision technology that&rsquo;s extracted structured data from billions of web pages, and training our machine learning systems using data from tens of thousands of unique shopping sites. We can&rsquo;t wait for you to try it out.</p>\n<p>What are you waiting for? Check out the <a href=\"http://www.diffbot.com/products/automatic/product\">Product API documentation</a>&nbsp;and dive on in! If you need a token, check out our <a href=\"http://www.diffbot.com/pricing\">pricing and plans</a> (including our Free plan).</p>\n<p>Questions? Hit us up at <a href=\"mailto:support@diffbot.com\">support@diffbot.com</a>.</p>", 
      "date": "Wed, 31 Jul 2013 00:00:00 GMT", 
      "type": "article", 
      "resolvedPageUrl": "http://blog.diffbot.com/diffbots-new-product-api-teaches-robots-to-shop-online/"
    }
  ]
}
```

Diffbot's V3 APIs return information about **all** identified objects on a submitted page.

Each V3 response includes a `request` object (which returns request-specific metadata), and an `objects` array, which will include the extracted information for all objects on a submitted page. At the moment, **only a single object** will be returned for Article API requests.

Objects in the Article API's `objects` array will include the following fields:

<table class="controls table table-bordered" border="0" cellpadding="5">
    <thead><tr><th>Field</th><th>Description</th></tr></thead>

        <tbody><tr>
            <td class="">type</td>
            <td class=" default"><div>Type of object (always <code>article</code>).</div></td>
        </tr>
        <tr>
            <td class="">pageUrl</td>
            <td class=" default"><div>URL of submitted page / page from which the article is extracted.</div></td>
        </tr>
        <tr>
            <td class="">resolvedPageUrl</td>
            <td class=" default"><div>Returned if the <code>pageUrl</code> redirects to another URL.</div></td>
        </tr>
        <tr>
            <td class="">title</td>
            <td class=" default"><div>Title of the article.</div></td>
        </tr>
        <tr>
            <td class="">text</td>
            <td class=" default"><div>Full text of the article.</div></td>
        </tr>
        <tr>
            <td class="">html</td>
            <td class=" default"><div>Diffbot-normalized HTML of the extracted article. Please see the <a href="#html-field-specification">HTML Specification</a> for a breakdown of elements and attributes returned.</div></td>
        </tr>
        <tr>
            <td class="">date</td>
            <td class=" default"><div>Date of extracted article, normalized in most cases to <a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec3.html#sec3.3">RFC 1123 (HTTP/1.1)</a>.</div></td>
        </tr>
        <tr>
            <td class="">author</td>
            <td class=" default"><div>Article author.</div></td>
        </tr>
        <tr>
            <td class="">authorUrl</td>
            <td class=" default"><div>URL of the author profile page, if available.</div></td>
        </tr>
        <tr>
            <td class="">discussion</td>
            <td class=" default"><div>Article comments, as extracted by the Diffbot Discussion API. See <a href="#discussion">below</a>.</div></td>
        </tr>
        <tr>
            <td class="parent">tags</td>
            <td class="parent default"><div>Array of tags/entities, generated from analysis of the extracted <code>text</code> and cross-referenced with <a href="http://wiki.dbpedia.org/About" target="_new">DBpedia</a>.</div></td>
        </tr>
        <tr>
            <td class="tags indent">label</td>
            <td class="tags indent default"><div>Name of the automatically-generated entity or tag. Tags are based on analysis of the <code>text</code> field and cross-referenced with <a href="http://wiki.dbpedia.org/About" target="_new">DBpedia</a>.</div></td>
        </tr>
        <tr>
            <td class="tags indent">type</td>
            <td class="tags indent default"><div>Link to the entity type, if identified, at DBpedia.</div></td>
        </tr>
        <tr>
            <td class="tags indent">uri</td>
            <td class="tags indent default"><div>Link to the entity at DBpedia.</div></td>
        </tr>
        <tr>
            <td class="">humanLanguage</td>
            <td class=" default"><div>Returns the (spoken/human) language of the submitted page, using two-letter <a href="http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes" target="_blank">ISO 639-1 nomenclature</a>.</div></td>
        </tr>
        <tr>
            <td class="">numPages</td>
            <td class=" default"><div>Number of pages automatically concatenated to form the <code>text</code> or <code>html</code> response. By default, Diffbot will automatically concatenate up to 20 pages of an article. <a href="http://support.diffbot.com/automatic-apis/handling-multiple-page-articles/">More on automatic concatenation</a>.</div></td>
        </tr>
        <tr>
            <td class="">nextPages</td>
            <td class=" default"><div>Array of all page URLs concatenated in a multipage article. <a href="http://support.diffbot.com/automatic-apis/handling-multiple-page-articles/">More on automatic concatenation</a>.</div></td>
        </tr>
        <tr>
            <td class="parent">images</td>
            <td class="parent default"><div>Array of images, if present within the article body.</div></td>
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
            <td class="images indent">height</td>
            <td class="images indent default"><div>Height of image as (re-)sized via browser/CSS.</div></td>
        </tr>
        <tr>
            <td class="images indent">width</td>
            <td class="images indent default"><div>Width of image as (re-)sized via browser/CSS.</div></td>
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
            <td class="images indent">diffbotUri</td>
            <td class="images indent default"><div>Internal ID used for indexing.</div></td>
        </tr>
        <tr>
            <td class="parent">videos</td>
            <td class="parent default"><div>Array of videos, if present within the article body.</div></td>
        </tr>
        <tr>
            <td class="videos indent">url</td>
            <td class="videos indent default"><div>Fully resolved link to source video content.</div></td>
        </tr>
        <tr>
            <td class="videos indent">naturalHeight</td>
            <td class="videos indent default"><div>Source video height, in pixels, if available.</div></td>
        </tr>
        <tr>
            <td class="videos indent">naturalWidth</td>
            <td class="videos indent default"><div>Source video width, in pixels, if available.</div></td>
        </tr>
        <tr>
            <td class="videos indent">primary</td>
            <td class="videos indent default"><div>Returns <code>true</code> if video is identified as primary based on visual analysis.</div></td>
        </tr>
        <tr>
            <td class="videos indent">diffbotUri</td>
            <td class="videos indent default"><div>Internal ID used for indexing.</div></td>
        </tr>
        <tr>
            <td class="">diffbotUri</td>
            <td class=" default"><div>Unique object ID. The <code>diffbotUri</code> is generated from the values of various Article fields and uniquely identifies the object. This can be used for deduplication.</div></td>
        </tr>

        <tr>
            <td colspan="2" class="header">Optional fields, available using <code>fields=</code> argument</td>
        </tr>
        <tr>
            <td class="">sentiment</td>
            <td class=" optional"><div>Returns the sentiment score of the analyzed article text, a value randing from -1.0 (very negative) to 1.0 (very positive).</div></td>
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
        </tr></tbody></table>

### HTML Field Specification

> #### Example HTML Returned: 

```html
<p>Diffbot's human wranglers are proud today to announce the release of our newest product: an API for... products!</p>

<p>The <a href="http://www.diffbot.com/products/automatic/product">Product API</a> can be used for extracting clean, structured data from any e-commerce product page. It automatically makes available all the product data you'd expect: price, discount/savings amount, shipping cost, product description, any relevant product images, SKU and/or other product IDs.</p>

<p>Even cooler: pair the Product API with <a href="http://www.diffbot.com/products/crawlbot">Crawlbot</a>, our intelligent site-spidering tool, and let Diffbot determine which pages are products, then automatically structure the entire catalog. Here's a quick demonstration of Crawlbot at work:</p>

<figure>
  <iframe frameborder="0" src="http://www.youtube.com/embed/lfcri5ungRo?feature=oembed"></iframe>
</figure>

<p>We've developed the Product API over the course of two years, building upon our core vision technology that's extracted structured data from billions of web pages, and training our machine learning systems using data from tens of thousands of unique shopping sites. We can't wait for you to try it out.</p>

<p>What are you waiting for? Check out the <a href="http://www.diffbot.com/products/automatic/product">Product API documentation</a> and dive on in! If you need a token, check out our <a href="http://www.diffbot.com/pricing">pricing and plans</a> (including our Free plan).</p>

<p>Questions? Hit us up at <a href="mailto:support@diffbot.com">support@diffbot.com</a>.</p>

```
Diffbot's `html` field returns normalized HTML maintaining the structure and layout of the source article, while standardizing its element and attributes for reliable parsing and processing. Content will be normalized into the following elements and attributes:



<table class="controls table table-bordered" border="0" cellpadding="5">
  <thead>
  <tr>
    <th>Element</th>
    <th>Attributes</th>
    <th>Description</th>
  </tr></thead>
  <tbody>
  <tr>
    <td colspan="3"><em>Block elements</em></td>
  </tr>
  <tr>
    <td>p</td>
    <td class="empty">—</td>
    <td>Unless returned within a more specific element below, all text will be returned within <code>p</code> elements at the top-level of the HTML response.</td>
  </tr>
  <tr>
    <td>h1 - h5</td>
    <td class="empty">—</td>
    <td>Headers will be maintained if originally provided.</td>
  </tr>
  <tr>
    <td>blockquote</td>
    <td class="empty">—</td>
    <td>Returned at top-level of HTML response.</td>
  </tr>
  <tr>
    <td>code, pre</td>
    <td class="empty">—</td>
    <td>Returned at top-level of HTML response.</td>
  </tr>
  <tr>
    <td>ul, ol</td>
    <td class="empty">—</td>
    <td>Returned at top-level of HTML response.</td>
  </tr>
  <tr>
    <td class="indent">li</td>
    <td class="empty">—</td>
    <td></td>
  </tr>
  <tr>
    <td>table</td>
    <td></td>
    <td>Original content within <code>table</code> elements will be largely retained, including images and other media items.</td>
  </tr>
  <tr>
    <td class="indent">tbody</td>
    <td class="empty">—</td>
    <td></td>
  </tr>
   <tr>
    <td class="indent">tr</td>
    <td class="empty">—</td>
    <td></td>
  </tr>
   <tr>
    <td class="indent">td</td>
    <td>valign, colspan</td>
    <td></td>
  </tr>
  <tr>
    <td>dl</td>
    <td class="empty">—</td>
    <td>Returned at top-level of HTML response.</td>
  </tr>
   <tr>
    <td class="indent">dt</td>
    <td class="empty">—</td>
    <td></td>
  </tr>
   <tr>
    <td class="indent">dd</td>
    <td class="empty">—</td>
    <td></td>
  </tr>
  <tr><td colspan="3"><em>Inline elements</em></td></tr>
  <tr>
    <td>br</td>
    <td class="empty">—</td>
    <td>Single linebreaks entities will be maintained in markup and returned as <code>&lt;br&gt;</code>. Double-linebreaks will be removed and surrounding content will be returned within <code>p</code> block elements.</td>
  </tr>
  <tr>
    <td>b, strong</td>
    <td class="empty">—</td>
    <td>Inline emphasis tags will be retained inside of other elements.</td>
  </tr>
  <tr>
    <td>i, em</td>
    <td class="empty">—</td>
    <td></td>
  </tr>
  <tr>
    <td>u</td>
    <td class="empty">—</td>
    <td></td>
  </tr>
  <tr>
    <td>a</td>
    <td>href</td>
    <td>Anchor tags and their <code>href</code> values will be retained.</td>
  </tr>
  <tr><td colspan="3"><em>Media</em></td></tr>
  <tr>
    <td>figure</td>
    <td class="empty">—</td>
    <td>Media elements will be returned at the top-level of the HTML content and contained within <code>figure</code> tags.</td>
  </tr>
  <tr>
    <td>img</td>
    <td>src, alt</td>
    <td>Image layout specifics (floats, etc.) and CSS-specified widths/heights will be discarded.</td>
  </tr>
  <tr>
    <td>video/audio</td>
    <td>src</td>
    <td>The child <code>source</code> elements within <code>video</code> and <code>audio</code> elements will be retained along with the <code>type</code> attribute, if provided.</td>
  </tr>
  <tr>
    <td class="indent">source</td>
    <td>src, type</td>
    <td></td>
  </tr>
  <tr>
    <td>figcaption</td>
    <td class="empty">—</td>
    <td>If present, media captions will be returned as <code>figcaption</code> elements within the <code>figure</code> container.</td>
  </tr>
  <tr>
    <td>iframe</td>
    <td>src, frameborder</td>
    <td></td>
  </tr>
  <tr>
    <td>embed, object</td>
    <td>src, type</td>
    <td></td>
  </tr>
  </tbody>
  </table>

<aside class="success">
Remember — a happy robot is an authenticated robot!
</aside>


## Options
### Comment Extraction

By default the Article API will attempt to extract comments from article pages, using integrated functionality from the Diffbot Discussion API. (This behavior can be disabled using the argument `discussion=false`.)

Comment data will be returned in the `discussion` object (nested within the primary article object). The full syntax for discussion data is [available in the Discussion API documentation](#discussion-api).


### Advanced Text Analysis Powered by Semantria

Our [native integration with Semantria](http://support.diffbot.com/automatic-apis/semantria-powered-sentiment-entity-extraction-and-other-text-analysis-features/) optionally allows extracted article content to be fully processed for categorization, entity and keyword extraction, and sentiment analysis. [Contact us](mailto:support@diffbot.com) if you are interested in adding this functionality to your paid Diffbot plan.




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
curl http://api.diffbot.com/v3/article?token={token}&url=http%3A%2F%2Fblog.diffbot.com \
    -H "Content-Type: text/html" \
    -d '<html><body><p>Now is the time for all good robots to come to the aid of their-- oh never mind, run!</p></body></html>'
    
```

> Plaintext Post Sample:


```
curl http://api.diffbot.com/v3/article?token={token}&fields=tags,text \
    -H "Content-Type: text/plain" \
    -d 'Now is the time for all good robots to come to the aid of their-- oh never mind, run!' 
```


If your content is not publicly available (e.g., behind a firewall), you can POST markup or plain text directly to the Article API endpoint for analysis:

`http://api.diffbot.com/v3/article?token={token}&url={url}`

Please note that if you submit HTML, the `url` argument is still required, and will be used to resolve any relative links contained in the markup.

Provide the content to analyze as your POST body, and specify the `Content-Type` header as `text/html` (for full markup) or `text/plain` (for text-only).

