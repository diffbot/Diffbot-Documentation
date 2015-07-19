# Article API
The Article API is used to extract clean article text and other data from news articles, blog posts and other text-heavy pages. Retrieves the full-text, cleaned and normalized HTML, related images and videos, author, date, tags and more - automatically, from any article on any site.

## Request

```shell
curl "http://api.diffbot.com/v3/article?token={token}&url=http%3A%2F%2Fblog.diffbot.com%2Fdiffbots-new-product-api-teaches-robots-to-shop-online"
```

To use the Article API, perform an HTTP GET request on the following endpoint:

`GET http://api.diffbot.com/v3/article`
<aside class="notice">Remember to url-encode all querystring parameters when using cURL! In all other instances, consult the client documentation - most of the good ones handle this for you.</aside>

### Required Arguments

```php
<?php

$diffbot = new Diffbot('my_token');
$url = 'http://techcrunch.com/2012/05/31/diffbot-raises-2-million-seed-round-for-web-content-extraction-technology/';
$articleApi = $diffbot->createArticleAPI($url);
```

| Argument           | Description    |
| ------------------ | --------------------------------------------------------------- |
| token              | Developer token|
| url                | Web page URL of the article to process (URL encoded)                           |

### Optional Arguments
```php
<?php

$articleApi->setMeta(true);
 
// setters can also be chained

$articleApi
            ->setBreadcrumb(true)
            ->setQuerystring(true)
            ->setLinks(true);
            
$articleApi
            ->setDiscussion(false)
            ->setPaging(false)
            ->setSentiment(true)
            ->setTimeout(30000);
```


| Argument           | Description    |
| ------------------ | --------------------------------------------------------------- |
| fields             | Used to specify optional fields to be returned by the Article API. See the [Fields](#the-fields-argument) section below.         |
| paging             | Pass paging=false to disable automatic concatenation of multiple-page articles. (By default, Diffbot will concatenate up to 20 pages of a single article.) [More on automatic concatenation](http://support.diffbot.com/automatic-apis/handling-multiple-page-articles). |
| maxTags            | Set the maximum number of automatically-generated tags to return. By default a maximum of five tags will be returned.           |
| discussion         | Pass discussion=false to disable automatic extraction of article comments. See [below](#comment-extraction).      |
| timeout            | Set a value in milliseconds to terminate the response. By default the Article API has a 30-second (30000) timeout.     |
| callback           | Use for jsonp requests. Needed for cross-domain ajax.                          |

       


### The Fields Argument

Use the `fields` argument to return optional fields in the JSON response. The default fields will always be returned (see [table below](#response20)). 

For example, to return `links` and `meta` (in addition to the default fields), your `&fields` argument would be:

`&fields=links,meta`

For nested arrays, use parentheses to retrieve specific fields, or * to return all sub-fields. For example, if the field `tags` were optional, you could tell Diffbot to only return `uri` sub-fields with `&fields=tags(uri)`.

Note that most clients will abstract this into setters or something equally simple to use (see `PHP` example to the right).

## Response 

> Example: processing the link http://blog.diffbot.com/diffbots-new-product-api-teaches-robots-to-shop-online

```php
<?php

echo $result->author; // prints out "John Davi"
echo $result->type; // prints out "article"
echo $result->text; // prints the text version of the article's body
echo $result->tags[0]['uri']; // prints out http://dbpedia.org/resource/Diffbot

// or, get the whole json dump with
$dump = $result->getResponse()->getBody();

// or as a PHP array
$dump = $result->getResponse()->json();
```

```shell
curl 'http://api.diffbot.com/v3/article?token={token}&url=http://blog.diffbot.com/diffbots-new-product-api-teaches-robots-to-shop-online'
```


> The full json dump will look something like this:

```json
{
    "request": {
        "pageUrl": "http://blog.diffbot.com/diffbots-new-product-api-teaches-robots-to-shop-online",
        "api": "article",
        "resolvedPageUrl": "http://blog.diffbot.com/diffbots-new-product-api-teaches-robots-to-shop-online/",
        "version": 3,
        "fields": "meta"
    },
    "objects": [
        {
            "tags": [
                {
                    "id": 4715031,
                    "count": 2,
                    "prevalence": 0.6666666666666666,
                    "label": "Diffbot",
                    "type": "organization",
                    "uri": "http://dbpedia.org/resource/Diffbot"
                },
                {
                    "id": 205322,
                    "count": 5,
                    "prevalence": 1.6666666666666667,
                    "label": "Application programming interface",
                    "uri": "http://dbpedia.org/resource/Application_programming_interface"
                },
                {
                    "id": 4268885,
                    "count": 1,
                    "prevalence": 0.3333333333333333,
                    "label": "Stock keeping unit",
                    "uri": "http://dbpedia.org/resource/Stock_keeping_unit"
                }
            ],
            "text": "Diffbot’s human wranglers are proud today to announce the release of our newest product: an API for… products!\nThe Product API can be used for extracting clean, structured data from any e-commerce product page. It automatically makes available all the product data you’d expect: price, discount/savings amount, shipping cost, product description, any relevant product images, SKU and/or other product IDs.\nEven cooler: pair the Product API with Crawlbot, our intelligent site-spidering tool, and let Diffbot determine which pages are products, then automatically structure the entire catalog. Here’s a quick demonstration of Crawlbot at work:\nWe’ve developed the Product API over the course of two years, building upon our core vision technology that’s extracted structured data from billions of web pages, and training our machine learning systems using data from tens of thousands of unique shopping sites. We can’t wait for you to try it out.\nWhat are you waiting for? Check out the Product API documentation and dive on in! If you need a token, check out our pricing and plans (including our Free plan).\nQuestions? Hit us up at support@diffbot.com.",
            "publisherRegion": "North America",
            "pageUrl": "http://blog.diffbot.com/diffbots-new-product-api-teaches-robots-to-shop-online",
            "videos": [
                {
                    "diffbotUri": "video|3|-761237582",
                    "primary": true,
                    "url": "http://www.youtube.com/embed/lfcri5ungRo?feature=oembed"
                }
            ],
            "publisherCountry": "Diffbot HQ",
            "humanLanguage": "en",
            "type": "article",
            "date": "Wed, 31 Jul 2013 00:00:00 GMT",
            "resolvedPageUrl": "http://blog.diffbot.com/diffbots-new-product-api-teaches-robots-to-shop-online/",
            "meta": {
                "viewport": "width=device-width",
                "microdata": {
                    "author": "John Davi"
                },
                "title": "Diffbot’s New Product API Teaches Robots to Shop Online | Diffblog",
                "generator": "WordPress 3.5"
            },
            "estimatedDate": "Wed, 31 Jul 2013 00:00:00 GMT",
            "author": "John Davi",
            "title": "Diffbot’s New Product API Teaches Robots to Shop Online",
            "diffbotUri": "article|3|-820542508",
            "authorUrl": "http://blog.diffbot.com/author/johndavi/",
            "html": "<p>Diffbot&rsquo;s human wranglers are proud today to announce the release of our newest product: an API for&hellip; products!</p>\n<p>The <a href=\"http://www.diffbot.com/products/automatic/product\">Product API</a> can be used for extracting clean, structured data from any e-commerce product page. It automatically makes available all the product data you&rsquo;d expect: price, discount/savings amount, shipping cost, product description, any relevant product images, SKU and/or other product IDs.</p>\n<p>Even cooler: pair the Product API with <a href=\"http://www.diffbot.com/products/crawlbot\">Crawlbot</a>, our intelligent site-spidering tool, and let Diffbot determine which pages are products, then automatically structure the entire catalog. Here&rsquo;s a quick demonstration of Crawlbot at work:</p>\n<figure><iframe frameborder=\"0\" src=\"http://www.youtube.com/embed/lfcri5ungRo?feature=oembed\"></iframe></figure>\n<p>We&rsquo;ve developed the Product API over the course of two years, building upon our core vision technology that&rsquo;s extracted structured data from billions of web pages, and training our machine learning systems using data from tens of thousands of unique shopping sites. We can&rsquo;t wait for you to try it out.</p>\n<p>What are you waiting for? Check out the <a href=\"http://www.diffbot.com/products/automatic/product\">Product API documentation</a> and dive on in! If you need a token, check out our <a href=\"http://www.diffbot.com/pricing\">pricing and plans</a> (including our Free plan).</p>\n<p>Questions? Hit us up at <a href=\"mailto:support@diffbot.com\">support@diffbot.com</a>.</p>",
            "siteName": "Diffbot"
        }
    ]
}
```

Diffbot's V3 APIs return information about **all** identified objects on a submitted page.

Each V3 response includes a `request` object (which returns request-specific metadata), and an `objects` array, which will include the extracted information for all objects on a submitted page. At the moment, **only a single object** will be returned for Article API requests.

Objects in the Article API's `objects` array will include the following:

---

**Default Fields**

| Field             | Description                         |
| ------------------------------------------------- | -------------------------------------------- |
| type              | Type of object (always `article`).    |
| pageUrl           | URL of submitted page / page from which the article is extracted.   |
| resolvedPageUrl   | Returned if the `pageUrl` redirects to another URL.                   |
| title             | Title of the article.               |
| siteName             | Assumed title of the site. Often matches name of the company owning the site.              |
| text              | Full text of the article.           |
| html              | Diffbot-normalized HTML of the extracted article. Please see the [HTML Specification](#html-field-specification) for a breakdown of elements and attributes returned.        |
| date              | Date of extracted article, normalized in most cases to RFC 1123 (HTTP/1.1).                         |
| estimatedDate              | Normalized in most cases to [RFC 1123 (HTTP/1.1)](http://www.w3.org/Protocols/rfc2616/rfc2616-sec3.html#sec3.3).                         |
| author            | Article author.                     |
| authorUrl         | URL of the author profile page, if available.                       |
| publisherCountry         | Country of publisher's origin, if determined. This can sometimes be nonsense, like "Diffbot HQ".                       |
| publisherRegion| Global region of publisher's origin, if determined (e.g. North America).                       |
| discussion        | Article comments, as extracted by the Diffbot [Discussion API](#discussion-api).                            |
| tags              | Array of tags/entities, generated from analysis of the extracted `text` and cross-referenced with [DBpedia](http://wiki.dbpedia.org/About).|
| tags.label             | Name of the automatically-generated entity or tag. Tags are based on analysis of the text field and cross-referenced with DBpedia.              |
| tags.type              | Link to the entity type, if identified, at [DBpedia](http://wiki.dbpedia.org/About).                 |
| tags.uri               | Link to the entity at DBpedia.      |
| metaTags               | Array of source extracted meta tags, as found in `article:tag` meta fields. Each element is an object with a single `name` property; i.e. a tag such as `<meta property="article:tag" content="Artificial Intelligence" />` gets parsed as `{"name": "Artificial Intelligence"}`      |
| humanLanguage     | Returns the (spoken/human) language of the submitted page, using two-letter [ISO 639-1 nomenclature](http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). |
| numPages          | Number of pages automatically concatenated to form the text or html response. (By default, Diffbot will concatenate up to 20 pages of a single article.) [More on automatic concatenation](http://support.diffbot.com/automatic-apis/handling-multiple-page-articles).                |
| nextPages         | Array of all page URLs concatenated in a multipage article.       |
| nextPage           | If discussion spans multiple pages, nextPage will return the subsequent page URL.                           |
| images            | Array of images, if present within the article body.                |
| images.url               | Fully resolved link to image.       |
| images.title             | Description or caption of the image.|
| images.height            | Height of image as (re-)sized via browser/CSS.                      |
| images.width             | Width of image as (re-)sized via browser/CSS.                       |
| images.naturalHeight     | Raw image height, in pixels.        |
| images.naturalWidth      | Raw image width, in pixels.         |
| images.primary           | Returns `true` if image is identified as primary based on visual analysis.                            |
| images.diffbotUri        | Internal ID used for indexing.      |
| videos            | Array of videos, if present within the article body.                |
| videos.url               | Fully resolved link to source video content.                        |
| videos.naturalHeight     | Source video height, in pixels, if available.                       |
| videos.naturalWidth      | Source video width, in pixels, if available.                        |
| videos.primary           | Returns `true` if video is identified as primary based on visual analysis.                            |
| videos.diffbotUri        | Internal ID used for indexing.      |
| diffbotUri        | Unique object ID. The `diffbotUri` is generated from the values of various Article fields and uniquely identifies the object. This can be used for deduplication.                 |

---

**Optional fields, available using the `fields=` argument**

| Field             | Description                         |
| ------------------------------------------------- | -------------------------------------------- |
| sentiment         | Returns the sentiment score of the analyzed article text, a value randing from -1.0 (very negative) to 1.0 (very positive).                     |
html
---

###HTML Field Specification

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
Diffbot's `html` field returns normalized HTML maintaining the structure and layout of the source article, while standardizing its elements and attributes for reliable parsing and processing. Content will be normalized into the following elements and attributes:


| Element         | Attributes       | Description|
| --------------- | ---------------- | ------------------ |
| p               | —                | Unless returned within a more specific element below, all text will be returned within `p` elements at the top-level of the HTML response.          |
| h1 - h5         | —                | Headers will be maintained if originally provided.                         |
| blockquote      | —                | Returned at top-level of HTML response.    |
| code, pre       | —                | Returned at top-level of HTML response.    |
| ul, ol          | —                | Returned at top-level of HTML response.    |
| li              | —                |            |
| table           |                  | Original content within table elements will be largely retained, including images and other media items.          |
| tbody           | —                |            |
| tr              | —                |            |
| td              | valign, colspan  |            |
| dl              | —                | Returned at top-level of HTML response.    |
| dt              | —                |            |
| dd              | —                |            |
| br              | —                | Single linebreaks entities will be maintained in markup and returned as `<br>`. Double-linebreaks will be removed and surrounding content will be returned within p block elements. |
| b, strong       | —                | Inline emphasis tags will be retained inside of other elements.            |
| i, em           | —                |            |
| u               | —                |            |
| a               | href             | Anchor tags and their href values will be retained.                        |
| Media           |                  |            |
| figure          | —                | Media elements will be returned at the top-level of the HTML content and contained within figure tags.            |
| img             | src, alt         | Image layout specifics (floats, etc.) and CSS-specified widths/heights will be discarded.                         |
| video/audio     | src              | The child source elements within video and audio elements will be retained along with the type attribute, if provided.                            |
| source          | src, type        |            |
| figcaption      | —                | If present, media captions will be returned as figcaption elements within the figure container.                   |
| iframe          | src, frameborder |            |
| embed, object   | src, type        |            |


## Options

### Comment Extraction

By default the Article API will attempt to extract comments from article pages, using integrated functionality from the Diffbot [Discussion API](#discussion-api) (This behavior can be disabled using the argument `discussion=false`).

Comment data will be returned in the `discussion` object (nested within the primary article object). The full syntax for discussion data is [available in the Discussion API documentation](#discussion-api).


### Advanced Text Analysis Powered by Semantria

Our [native integration with Semantria](http://support.diffbot.com/automatic-apis/semantria-powered-sentiment-entity-extraction-and-other-text-analysis-features/) optionally allows extracted article content to be fully processed for categorization, entity and keyword extraction, and sentiment analysis. [Contact us](mailto:support@diffbot.com) if you are interested in adding this functionality to your paid Diffbot plan.




### Authentication

You can supply Diffbot with basic authentication credentials or custom HTTP headers (see below) to access intranet pages or other sites that require a login.

### Basic Authentication
To access pages that require a login/password ([using basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication)), include the username and password in your `url` parameter, e.g.: `url=http%3A%2F%2FUSERNAME:PASSWORD@www.diffbot.com`.

### Custom HTTP Headers

You can supply Diffbot APIs with custom values for the user-agent, _referer_, cookie, or accept-language values in the HTTP request. These will be used in place of the Diffbot default values.

To provide custom headers, pass in the following values in your own headers when calling the Diffbot API:

Header | Description
--------- | -----------
X-Forward-User-Agent | Will be used as Diffbot's `User-Agent` header when making your request.
X-Forward-Referer | Will be used as Diffbot's `Referer` header when making your request.
X-Forward-Cookie | Will be used as Diffbot's `Cookie` header when making your request.
X-Forward-Accept-Language | Will be used as Diffbot's `Accept-Language` header when making your request.


### Posting Content

> HTML Post Sample:

```shell
curl 'http://api.diffbot.com/v3/article?token={token}&url=http%3A%2F%2Fblog.diffbot.com' -H "Content-Type: text/html" -d '<html><body><p>Now is the time for all good robots to come to the aid of their-- oh never mind, run!</p></body></html>'
```

```php
<?php

// coming soon
```

> Plaintext Post Sample:


```shell
curl 'http://api.diffbot.com/v3/article?token={token}' -H "Content-Type: text/plain" -d 'Now is the time for all good robots to come to the aid of their-- oh never mind, run!'
```

```php
<?php

// coming soon
```

If your content is not publicly available (e.g., behind a firewall), you can POST markup or plain text directly to the Article API endpoint for analysis:

`http://api.diffbot.com/v3/article?token={token}&url={url}`

Provide the content to analyze as your POST body, and specify the `Content-Type` header as `text/html` (for full markup) or `text/plain` (for text-only).

Please note that if you submit HTML (default, if `Content-Type` is missing), the `url` argument is still required, and will be used to resolve any relative links contained in the markup.