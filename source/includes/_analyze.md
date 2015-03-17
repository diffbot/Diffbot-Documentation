# Analyze API
The Diffbot Analyze API visually analyzes a web page, identifies its "page-type," and determines which Diffbot extraction API (if any) is appropriate. Pages that match a supported extraction API -- articles, discussions, images, products or videos -- will be automatically extracted and returned in the Analyze API response.

Pages not currently supported by an extraction API will return "other."
## Request



```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://api.diffbot.com/v3/analyze?token=...&url=..."
```

To use the Analyze API, perform a HTTP GET request on the following endpoint:

`GET http://api.diffbot.com/v3/analyze`
<aside class="warning">If you don't URL encode the url, Diffbot returns error code 500.</aside>


<table class="controls table table-bordered" id="arguments" border="0" cellpadding="5">
	<thead><tr><th>Argument</th><th>Description</th></tr></thead>

        <tbody><tr>
            <td class="">token</td>
            <td class=" default"><div>Developer token</div></td>
        </tr>
        <tr>
            <td class="">url</td>
            <td class=" default"><div>Web page URL of the analyze to process (URL encoded)</div></td>
        </tr>

        <tr>
            <td colspan="2" class="header">Optional arguments</td>
        </tr>
        <tr>
            <td class="">fields</td>
            <td class=" optional"><div>Specify optional fields to be returned from any fully-extracted pages, e.g.: <code>&amp;fields=querystring,links</code>.<br><br>See available fields within each API's individual documentation pages.</div></td>
        </tr>
        <tr>
            <td class="">mode</td>
            <td class=" optional"><div>By default the Analyze API will fully extract all pages that match an existing Automatic API -- articles, products or image pages. Set <code>mode</code> to a specific page-type (e.g., <code>mode=article</code>) to extract content only from that specific page-type. All other pages will simply return the default Analyze fields.</div></td>
        </tr>
        <tr>
            <td class="">discussion</td>
            <td class=" optional"><div>Pass <code>discussion=false</code> to disable automatic extraction of comments or reviews from pages identified as articles or products. This will not affect pages identified as discussions.</div></td>
        </tr>
        <tr>
            <td class="">timeout</td>
            <td class=" optional"><div>Set a value in milliseconds to terminate the response. By default the Analyze API has a 30-second (30000) timeout.</div></td>
        </tr>
        <tr>
            <td class="">callback</td>
            <td class=" optional"><div>Use for jsonp requests. Needed for cross-domain ajax.</div></td>
        </tr></tbody></table>

## Response 
```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/3"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
    "title": "Diffbot Raises $2 Million Angel Round For Web Content Extraction Technology  |  TechCrunch",
    "request": {
        "pageUrl": "http://techcrunch.com/2012/05/31/diffbot-raises-2-million-seed-round-for-web-content-extraction-technology/",
        "api": "analyze",
        "version": 3
    },
    "humanLanguage": "en",
    "type": "article",
    "objects": [{
        "summary": "Diffbot, the super-geeky/awesome visual learning robot technology which aims to “see” the web the way that people do, is today announcing a new infusion of capital.  Matrix Partners also participated in the round.  Of the new investors, Sky Dayton will be the first to join Diffbot’s board and will be taking an active role in the company, including plans to go hands-on with various Diffbot projects.",
        "tags": [{
            "id": 4585348,
            "count": 11,
            "prevalence": 0.9705882352941178,
            "label": "Diffbot",
            "type": "organization",
            "uri": "http://dbpedia.org/resource/Diffbot"
        }, {
            "id": 175464,
            "count": 4,
            "prevalence": 0.3529411764705882,
            "label": "Application programming interface",
            "uri": "http://dbpedia.org/resource/Application_programming_interface"
        }, {
            "id": 29686,
            "count": 2,
            "prevalence": 0.1764705882352941,
            "label": "AOL",
            "type": "organization",
            "uri": "http://dbpedia.org/resource/AOL"
        }, {
            "id": 998361,
            "count": 2,
            "prevalence": 0.1764705882352941,
            "label": "StartX",
            "type": "organization",
            "uri": "http://dbpedia.org/resource/StartX"
        }, {
            "id": 125012,
            "count": 2,
            "prevalence": 0.1764705882352941,
            "label": "Sky Dayton",
            "type": "person",
            "uri": "http://dbpedia.org/resource/Sky_Dayton"
        }],
        "icon": "https://s0.wp.com/wp-content/themes/vip/techcrunch-2013/assets/images/homescreen_TCIcon_ipad_2x.png",
        "text": "Diffbot, the super-geeky/awesome visual learning robot technology which aims to “see” the web the way that people do, is today announcing a new infusion of capital. The company has closed $2 million in funding from a number of technology veterans, including EarthLink founder Sky Dayton; Andy Bechtolsheim, co-founder of Sun Microsystems; Joi Ito, Director of MIT Media Lab; Brad Garlinghouse, CEO of YouSendIt (and formerly of TechCrunch parent company AOL), Maynard Webb, Chairman of the Board at LiveOps, formerly eBay COO; Elad Gil, VP of Corporate Strategy at Twitter; Jonathan Heiliger, former VP of Technical Operations at Facebook; Redbeacon co-founder Aaron Lee; and founder of VitalSigns Montgomery Kersten.\nMatrix Partners also participated in the round. Of the new investors, Sky Dayton will be the first to join Diffbot’s board and will be taking an active role in the company, including plans to go hands-on with various Diffbot projects.\nLast August, the company publicly debuted its first APIs, which allow developers to build apps that can automatically extract meaning from web pages. For example, the Front Page API is able to analyze site homepages, and understands the difference between article text, headlines, bylines, ads, etc. The Article API can then extract clean article text, images and videos. Another example of Diffbot in action is the “follow API,” which can track the changes made to a website.\nToday, Diffbot has categorized the web into about 20 different page types, including homepages and article pages, which are the first two types it can now identity. Going forward, Diffbot plans train its bots to recognize all the other types of pages, including product pages, social networking profiles, recipe pages, review pages, and more.\nIts APIs have been put to use by AOL (again: disclosure, TC parent) in its news magazine AOL Editions, as well as by companies like Nuance, SocMetrics, and others. Diffbot says it’s now processing 100 million API calls per month on behalf of its customers. Thousands of developers are using the APIs, the company notes, but paying customers are only in the “tens.” Correction: we’re now told they have “a lot more!”\nDiffbot founder and CEO Michael Tung (aka “Diffbot Mike”) says the new funding will be put towards new hires and expanding its resources. “More than that, we’re receiving a huge vote of confidence from veterans who have built massive companies and understand the fine points of building for scale, maintaining uptime and delivering the absolute highest standards of service.”\nTung is a patent attorney and Stanford PhD student who left the doctoral program to pursue Diffbot, thanks to seed funding from Stanford’s incubator, StartX. Diffbot was StartX’s first investment. With today’s funding, Diffbot total raise is $2 million and change.",
        "pageUrl": "http://techcrunch.com/2012/05/31/diffbot-raises-2-million-seed-round-for-web-content-extraction-technology/",
        "humanLanguage": "en",
        "type": "article",
        "date": "Thu, 31 May 2012 00:00:00 GMT",
    		"author": "Sarah Perez",
        "title": "Diffbot Raises $2 Million Angel Round For Web Content Extraction Technology",
        "diffbotUri": "article|3|-407652032",
        "authorUrl": "http://techcrunch.com/author/sarah-perez/",
        "images": [{
            "height": 343,
            "naturalHeight": 341,
            "diffbotUri": "image|3|-1366405470",
            "primary": true,
            "width": 302,
            "naturalWidth": 300,
            "url": "https://tctechcrunch2011.files.wordpress.com/2012/05/diffbot_9.png?w=300"
        }, {
            "height": 688,
            "naturalHeight": 686,
            "diffbotUri": "image|3|-1328981514",
            "width": 642,
            "naturalWidth": 640,
            "url": "http://tctechcrunch2011.files.wordpress.com/2012/05/npr-v3.gif?w=640&h=686"
        }],
        "html": "<figure><img src=\"https://tctechcrunch2011.files.wordpress.com/2012/05/diffbot_9.png?w=300\"></img></figure>\n<p><a href=\"http://www.diffbot.com/\">Diffbot</a>, the super-geeky/awesome visual learning robot technology which aims to &ldquo;see&rdquo; the web the way that people do, is today announcing a new infusion of capital. The company has closed $2 million in funding from a number of technology veterans, including EarthLink founder <a href=\"http://www.crunchbase.com/person/sky-dayton\">Sky Dayton</a>;&nbsp;<a href=\"http://www.crunchbase.com/person/andy-bechtolsheim\">Andy Bechtolsheim</a>, co-founder of Sun Microsystems;&nbsp;<a href=\"http://www.crunchbase.com/person/joi-ito\">Joi Ito</a>, Director of MIT Media Lab;&nbsp;<a href=\"http://www.crunchbase.com/person/brad-garlinghouse\">Brad Garlinghouse</a>, CEO of YouSendIt (<a href=\"http://techcrunch.com/2012/05/15/brad-garlinghouse-becomes-ceo-of-booming-file-sharing-site-yousendit/\">and formerly of TechCrunch parent company AOL</a>), <a href=\"http://www.crunchbase.com/person/maynard-webb\">Maynard Webb</a>, Chairman of the Board at LiveOps, formerly eBay COO; <a href=\"http://www.crunchbase.com/person/elad-gil\">Elad Gil</a>,&nbsp;VP of Corporate Strategy at Twitter;&nbsp;<a href=\"http://www.crunchbase.com/person/jonathan-heiliger\">Jonathan Heiliger</a>, former VP of Technical Operations at Facebook; Redbeacon co-founder&nbsp;<a href=\"http://www.crunchbase.com/person/aaron-lee\">Aaron Lee</a>; and founder of VitalSigns&nbsp;<a href=\"http://www.linkedin.com/pub/montgomery-kersten/16/26a/5b0\">Montgomery Kersten</a>.</p>\n<p><a href=\"http://www.crunchbase.com/financial-organization/matrix-partners\">Matrix Partners</a> also participated in the round. Of the new investors, Sky Dayton will be the first to join Diffbot&rsquo;s board and will be taking an active role in the company, including plans to go hands-on with various Diffbot projects.</p>\n<p>Last August, <a href=\"http://techcrunch.com/2011/08/25/diffbot-sees-the-web-like-people-do-now-free-for-developers/\">the company publicly debuted its first APIs</a>, which allow developers to build apps that can automatically extract meaning from web pages. For example, the &nbsp;Front Page API is able to analyze site homepages, and understands the difference between article text, headlines, bylines, ads, etc. The Article API can then extract clean article text, images and videos.&nbsp;Another example of Diffbot in action is the &ldquo;follow API,&rdquo; which can track the changes made to a website.</p>\n<p>Today, Diffbot has categorized the web into about 20 different page types, including homepages and article pages, which are the first two types it can now identity.&nbsp;Going forward, Diffbot plans train its bots to recognize all the other types of pages, including product pages, social networking profiles, recipe pages, review pages, and more.</p>\n<p>Its APIs have been put to use by AOL (again: disclosure, TC parent) in its news magazine <a href=\"http://editions.com/\">AOL Editions</a>, as well as by companies like&nbsp;<a href=\"http://nuance.com/\">Nuance</a>,&nbsp;<a href=\"http://socmetrics.com/\">SocMetrics</a>, and others. Diffbot says it&rsquo;s now processing 100 million API calls per month on behalf of its customers. Thousands of developers are using the APIs, the company notes, but paying customers are only in the &ldquo;tens.&rdquo; Correction: we&rsquo;re now told they have &ldquo;a lot more!&rdquo;</p>\n<p>Diffbot founder and CEO Michael Tung (aka &ldquo;Diffbot Mike&rdquo;) says the new funding will &nbsp;be put towards new hires and expanding its resources. &ldquo;More than that, we&rsquo;re receiving a huge vote of confidence from veterans who have built massive companies and understand the fine points of building for scale, maintaining uptime and delivering the absolute highest standards of service.&rdquo;</p>\n<p>Tung is a patent attorney and Stanford PhD student who left the doctoral program to pursue Diffbot, thanks to seed funding from Stanford&rsquo;s incubator, <a href=\"http://www.crunchbase.com/company/startx\">StartX</a>. Diffbot was StartX&rsquo;s first investment. With today&rsquo;s funding, Diffbot total raise is $2 million and change.</p>\n<figure><a href=\"http://techcrunch.com/2012/05/31/diffbot-raises-2-million-seed-round-for-web-content-extraction-technology/npr-v3/\"><img alt=\"\" src=\"http://tctechcrunch2011.files.wordpress.com/2012/05/npr-v3.gif?w=640&h=686\"></img></a></figure>"
    }]
}
```

Each V3 response includes a request object (which returns request-specific metadata), and an objects array, which will include the extracted information for all objects on a submitted page.

If the Analyze API identifies the submitted page as an article, discussion thread, product or image, the associated object(s) from the page will be returned automatically in the objects array.

The default fields returned:

<table class="controls table table-bordered" id="fields" border="0" cellpadding="5">
	<thead><tr><th>Field</th><th>Description</th></tr></thead>

        <tbody><tr>
            <td class="">title</td>
            <td class=" default"><div>Title of the page.</div></td>
        </tr>
        <tr>
            <td class="">type</td>
            <td class=" default"><div>Page-type of the submitted URL, either <code>article</code>, <code>image</code>, <code>product</code> or <code>other</code>.</div></td>
        </tr>
        <tr>
            <td class="">humanLanguage</td>
            <td class=" default"><div>Returns the (spoken/human) language of the submitted page, using two-letter <a href="http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes" target="_blank">ISO 639-1 nomenclature</a>.</div></td>
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
        </tr></tbody></table>


<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>
## Authentication

You can supply Diffbot with basic authentication credentials or custom HTTP headers (see below) to access intranet pages or other sites that require a login.

###Basic Authentication
To access pages that require a login/password ([using basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication)), include the username and password in your `url` parameter, e.g.: `url=http%3A%2F%2FUSERNAME:PASSWORD@www.diffbot.com`.

## Custom HTTP Headers

You can supply Diffbot APIs with custom values for the user-agent, referer, cookie, or accept-language values in the HTTP request. These will be used in place of the Diffbot default values.

To provide custom headers, pass in the following values in your own headers when calling the Diffbot API:

Header | Description
--------- | -----------
X-Forward-User-Agent | Will be used as Diffbot's `User-Agent` header when making your request.
X-Forward-Referer	| Will be used as Diffbot's `Referer` header when making your request.
X-Forward-Cookie | Will be used as Diffbot's `Cookie` header when making your request.
X-Forward-Accept-Language | Will be used as Diffbot's `Accept-Language` header when making your request.
