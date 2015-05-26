# Discussion API
The Discussion API automatically structures and extracts entire threads or lists of reviews/comments from most discussion pages, forums, and similarly structured web pages.




## Request



```shell
curl "http://api.diffbot.com/v3/discussion?token={token}&url=http%3A%2F%2Fblog.diffbot.com%2Fdiffbots-new-product-api-teaches-robots-to-shop-online"
```

To use the Discussion API, perform a HTTP GET request on the following endpoint:


`GET http://api.diffbot.com/v3/discussion`


<aside class="notice">Remember to url-encode all querystring parameters!</aside>

<table class="controls table table-bordered" id="arguments" border="0" cellpadding="5">
    <thead><tr><th>Argument</th><th>Description</th></tr></thead>

        <tbody><tr>
            <td class="">token</td>
            <td class=" default"><div>Developer token</div></td>
        </tr>
        <tr>
            <td class="">url</td>
            <td class=" default"><div>Web page URL of the discussion to process (URL encoded)</div></td>
        </tr>

        <tr>
            <td colspan="2" class="header">Optional arguments</td>
        </tr>
        <tr>
            <td class="">fields</td>
            <td class=" optional"><div>Used to specify optional fields to be returned by the Discussion API. See the <a href="#fields">Fields</a> section below.</div></td>
        </tr>
        <tr>
            <td class="">timeout</td>
            <td class=" optional"><div>Set a value in milliseconds to terminate the response. By default the Discussion API has a 30-second (30000) timeout.</div></td>
        </tr>
        <tr>
            <td class="">callback</td>
            <td class=" optional"><div>Use for jsonp requests. Needed for cross-domain ajax.</div></td>
        </tr>
        <tr>
            <td class="">maxPages</td>
            <td class=" optional"><div>Set the maximum number of pages in a thread to automatically concatenate in a single response. Default = 1 (no concatenation). Set <code>maxPages=all</code> to retrieve all pages of a thread regardless of length. Each individual page will count as a separate API call.</div></td>
        </tr></tbody></table>


## Response 

> If successful, you'll receive this response:

```json
{
  "request": {
    "pageUrl": "https://news.ycombinator.com/item?id=5608988", 
    "api": "discussion", 
    "version": 3
  }, 
  "objects": [
    {
      "tags": [
        {
          "id": 4688313, 
          "count": 8, 
          "prevalence": 0.6666666666666666, 
          "label": "Diffbot", 
          "type": "organization", 
          "uri": "http://dbpedia.org/resource/Diffbot"
        }, 
        {
          "id": 841619, 
          "count": 1, 
          "prevalence": 0.08333333333333333, 
          "label": "Android (operating system)", 
          "type": "Http://wikidata.dbpedia.org/resource/Q386724", 
          "uri": "http://dbpedia.org/resource/Android_(operating_system)"
        }, 
        {
          "id": 393009, 
          "count": 1, 
          "prevalence": 0.08333333333333333, 
          "label": "Catcher", 
          "uri": "http://dbpedia.org/resource/Catcher"
        }, 
        {
          "id": 1766465, 
          "count": 1, 
          "prevalence": 0.08333333333333333, 
          "label": "Access token", 
          "uri": "http://dbpedia.org/resource/Access_token"
        }, 
        {
          "id": 178604, 
          "count": 1, 
          "prevalence": 0.08333333333333333, 
          "label": "Application programming interface", 
          "uri": "http://dbpedia.org/resource/Application_programming_interface"
        }
      ], 
      "title": "Show HN: Analysis of 2.5 Years of Frontpage Articles", 
      "numPosts": 8, 
      "diffbotUri": "discussion|3|-110040828", 
      "pageUrl": "https://news.ycombinator.com/item?id=5608988", 
      "posts": [
        {
          "id": 0, 
          "author": "miket", 
          "text": "(diffbot.com)", 
          "title": "Show HN: Analysis of 2.5 Years of Frontpage Articles", 
          "pageUrl": "https://news.ycombinator.com/item?id=5608988", 
          "diffbotUri": "post|3|593840622", 
          "authorUrl": "https://news.ycombinator.com/user?id=miket", 
          "html": "<p>(diffbot.com)</p>", 
          "humanLanguage": "en", 
          "date": "Thu, 05 Feb 2015 00:00:00 GMT", 
          "type": "post"
        }, 
        {
          "tags": [
            {
              "id": 4688313, 
              "count": 4, 
              "label": "Diffbot", 
              "type": "organization", 
              "uri": "http://dbpedia.org/resource/Diffbot"
            }
          ], 
          "id": 1, 
          "author": "johncoogan", 
          "text": "Huge fan of DiffBot and awesome projects like this. Really cool analysis, thanks for posting.\n\nWould be possible for you to post / send me the original data? I have been very interested in working on more longitudinal analysis using DiffBot data and this seems like a fun and interesting place to start. I'm happy to open-source / clearly attribute DiffBot's contribution to whatever I find / hack together, and would feel a lot more comfortable about integrating DiffBot into larger projects in the future.\nPlease email me (in my profile) if this is a possibility. Thanks!\n\n\n-----", 
          "pageUrl": "https://news.ycombinator.com/item?id=5608988", 
          "diffbotUri": "post|3|-1972390462", 
          "authorUrl": "https://news.ycombinator.com/user?id=johncoogan", 
          "html": "<p>Huge fan of DiffBot and awesome projects like this. Really cool analysis, thanks for posting.</p>\n<p>Would be possible for you to post / send me the original data? I have been very interested in working on more longitudinal analysis using DiffBot data and this seems like a fun and interesting place to start. I'm happy to open-source / clearly attribute DiffBot's contribution to whatever I find / hack together, and would feel a lot more comfortable about integrating DiffBot into larger projects in the future.</p>\n<p>Please email me (in my profile) if this is a possibility. Thanks!</p>\n<p>----- </p>", 
          "humanLanguage": "en", 
          "type": "post"
        }, 
        {
          "tags": [
            {
              "id": 4688313, 
              "count": 2, 
              "label": "Diffbot", 
              "type": "organization", 
              "uri": "http://dbpedia.org/resource/Diffbot"
            }, 
            {
              "id": 1766465, 
              "count": 1, 
              "label": "Access token", 
              "uri": "http://dbpedia.org/resource/Access_token"
            }
          ], 
          "id": 2, 
          "author": "tswaterman", 
          "parentId": 1, 
          "text": "Great idea! We'd be happy to share/help. If more people are interested, we'll figure out a good way to distribute the dataset generally. But in fact, you can extract the same data set, and add whatever other smart things you want along with it, using the Diffbot APIs. Everything we did to get this information is explained on our blog at\nhttp://blog.diffbot.com/diffbots-hackernews-trend-analyzer/ Sounds like you're already using the Diffbot service, but for anyone who's not, they can sign up for a free access token on our 'pricing' page at \nhttp://www.diffbot.com/ It's a few hundred thousand pages you'd need to analyze to get this, which doesn't quite fit under the free plan. You might not want to analyze as many years worth of stuff as we did for this demo, though.\n\nAll the pieces and services we used for this, including all the text extraction, topic detection, and crawling, are available to any user.\nHave fun with it, and keep us informed about whatever cool stuff you build with it, and of course tell us about any features or capabilities you wish Diffbot can provide.\n\n\n-----", 
          "pageUrl": "https://news.ycombinator.com/item?id=5608988", 
          "diffbotUri": "post|3|-1080445506", 
          "authorUrl": "https://news.ycombinator.com/user?id=tswaterman", 
          "html": "<p>Great idea! We'd be happy to share/help. If more people are interested, we'll figure out a good way to distribute the dataset generally. But in fact, you can extract the same data set, and add whatever other smart things you want along with it, using the Diffbot APIs. Everything we did to get this information is explained on our blog at</p>\n<pre><code>    http://blog.diffbot.com/diffbots-hackernews-trend-analyzer/\n</code></pre>\n<p>Sounds like you're already using the Diffbot service, but for anyone who's not, they can sign up for a free access token on our 'pricing' page at <a href=\"http://www.diffbot.com/\">http://www.diffbot.com/</a> It's a few hundred thousand pages you'd need to analyze to get this, which doesn't quite fit under the free plan. You might not want to analyze as many years worth of stuff as we did for this demo, though.</p>\n<p>All the pieces and services we used for this, including all the text extraction, topic detection, and crawling, are available to any user.</p>\n<p>Have fun with it, and keep us informed about whatever cool stuff you build with it, and of course tell us about any features or capabilities you wish Diffbot can provide.</p>\n<p>----- </p>", 
          "humanLanguage": "en", 
          "type": "post"
        }, 
        {
          "tags": [
            {
              "id": 4688313, 
              "count": 2, 
              "label": "Diffbot", 
              "type": "organization", 
              "uri": "http://dbpedia.org/resource/Diffbot"
            }, 
            {
              "id": 393009, 
              "count": 1, 
              "label": "Catcher", 
              "uri": "http://dbpedia.org/resource/Catcher"
            }, 
            {
              "id": 178604, 
              "count": 1, 
              "label": "Application programming interface", 
              "uri": "http://dbpedia.org/resource/Application_programming_interface"
            }
          ], 
          "id": 3, 
          "author": "mayank", 
          "text": "Funny, I just built a HN article catcher that uses Diffbot to collect and classify submissions from the /new page [1]. I've been a Diffbot fan for quite a while now (although their entity recognition/tag classifier needs a bit of work as you can see from the categorization on my catcher page below).\n\n[1] http://lahiri.me/more\nI should add that their API is fantastic, and far better than using BeautifulSoup/NLTK for extracting textual content from webpages.\n\n\n-----", 
          "pageUrl": "https://news.ycombinator.com/item?id=5608988", 
          "diffbotUri": "post|3|-398235096", 
          "authorUrl": "https://news.ycombinator.com/user?id=mayank", 
          "html": "<p>Funny, I just built a HN article catcher that uses Diffbot to collect and classify submissions from the /new page [1]. I've been a Diffbot fan for quite a while now (although their entity recognition/tag classifier needs a bit of work as you can see from the categorization on my catcher page below).</p>\n<p>[1] <a href=\"http://lahiri.me/more\">http://lahiri.me/more</a></p>\n<p>I should add that their API is fantastic, and far better than using BeautifulSoup/NLTK for extracting textual content from webpages.</p>\n<p>----- </p>", 
          "humanLanguage": "en", 
          "type": "post"
        }, 
        {
          "id": 4, 
          "author": "tswaterman", 
          "parentId": 3, 
          "text": "Cool! How many articles, or what time period, did you use for this? It looks like you're using only a subset of the topic tags -- did you make a list of 'interesting stuff' to filter against?", 
          "pageUrl": "https://news.ycombinator.com/item?id=5608988", 
          "diffbotUri": "post|3|-721182853", 
          "authorUrl": "https://news.ycombinator.com/user?id=tswaterman", 
          "html": "<p>Cool! How many articles, or what time period, did you use for this? It looks like you're using only a subset of the topic tags -- did you make a list of 'interesting stuff' to filter against?</p>", 
          "humanLanguage": "en", 
          "type": "post"
        }, 
        {
          "id": 5, 
          "author": "mayank", 
          "parentId": 4, 
          "text": "It's been running for about a week I think, and I'm just taking the top 80 or so tags by article count. Glad you like it :)", 
          "pageUrl": "https://news.ycombinator.com/item?id=5608988", 
          "diffbotUri": "post|3|-1084333819", 
          "authorUrl": "https://news.ycombinator.com/user?id=mayank", 
          "html": "<p>It's been running for about a week I think, and I'm just taking the top 80 or so tags by article count. Glad you like it :)</p>", 
          "humanLanguage": "en", 
          "type": "post"
        }, 
        {
          "tags": [
            {
              "id": 841619, 
              "count": 1, 
              "label": "Android (operating system)", 
              "type": "Http://wikidata.dbpedia.org/resource/Q386724", 
              "uri": "http://dbpedia.org/resource/Android_(operating_system)"
            }
          ], 
          "id": 6, 
          "author": "tliou", 
          "text": "Had to figure out how to use it ... but interesting once you do! Android vs IPhone on Hackernews frontpage shows spike in iphone on launch dates, but mediocre to no activity for android. is it because android is less interesting and not as innovative? or not as fun to talk/read about?", 
          "pageUrl": "https://news.ycombinator.com/item?id=5608988", 
          "diffbotUri": "post|3|-1839689133", 
          "authorUrl": "https://news.ycombinator.com/user?id=tliou", 
          "html": "<p>Had to figure out how to use it ... but interesting once you do! Android vs IPhone on Hackernews frontpage shows spike in iphone on launch dates, but mediocre to no activity for android. is it because android is less interesting and not as innovative? or not as fun to talk/read about?</p>", 
          "humanLanguage": "en", 
          "type": "post"
        }, 
        {
          "id": 7, 
          "author": "minimax", 
          "text": "Neat! Wish I could select by just domain name (i.e. just nytimes.com rather than dozen or so whatever.nytimes.com subdomains).", 
          "pageUrl": "https://news.ycombinator.com/item?id=5608988", 
          "diffbotUri": "post|3|-869746168", 
          "authorUrl": "https://news.ycombinator.com/user?id=minimax", 
          "html": "<p>Neat! Wish I could select by just domain name (i.e. just nytimes.com rather than dozen or so whatever.nytimes.com subdomains).</p>", 
          "humanLanguage": "en", 
          "type": "post"
        }
      ], 
      "humanLanguage": "en", 
      "confidence": 0.05271753612809388, 
      "numPages": 1, 
      "type": "discussion", 
      "participants": 6
    }
  ]
}
```

Diffbot's V3 APIs return information about **all** identified objects on a submitted page.

Each V3 response includes a `request` object (which returns request-specific metadata), and an `objects` array, which will include the extracted information for all objects on a submitted page. The Discussion API returns all post data in a single object within the `objects` array.

Within the Article and Product APIs (to extract comments or review data), discussion data will be returned within the nested `discussion` object.

The Discussion API `objects` / `discussion` response will include the following fields:

<table class="controls table table-bordered" id="fields" border="0" cellpadding="5">
    <thead><tr><th>Field</th><th>Description</th></tr></thead>

        <tbody><tr>
            <td class="">type</td>
            <td class=" default"><div>Type of object (always <code>discussion</code>).</div></td>
        </tr>
        <tr>
            <td class="">pageUrl</td>
            <td class=" default"><div>URL of submitted page / page from which the discussion is extracted.</div></td>
        </tr>
        <tr>
            <td class="">resolvedPageUrl</td>
            <td class=" default"><div>Returned if the <code>pageUrl</code> redirects to another URL.</div></td>
        </tr>
        <tr>
            <td class="">title</td>
            <td class=" default"><div>Title of the discussion.</div></td>
        </tr>
        <tr>
            <td class="">numPosts</td>
            <td class=" default"><div>Number of individual posts in the thread.</div></td>
        </tr>
        <tr>
            <td class="parent">posts</td>
            <td class="parent default"><div>Array of individual posts.</div></td>
        </tr>
        <tr>
            <td class="posts indent">type</td>
            <td class="posts indent default"><div>Type of element (always <code>post</code>).</div></td>
        </tr>
        <tr>
            <td class="posts indent">id</td>
            <td class="posts indent default"><div>ID of the individual post. The first post of a thread will have an ID of 0.</div></td>
        </tr>
        <tr>
            <td class="posts indent">parentId</td>
            <td class="posts indent default"><div>ID of the parent, if the post is a reply or response.</div></td>
        </tr>
        <tr>
            <td class="posts indent">text</td>
            <td class="posts indent default"><div>Full text of the extracted post.</div></td>
        </tr>
        <tr>
            <td class="posts indent">html</td>
            <td class="posts indent default"><div>Diffbot-normalized HTML of the extracted post. Please see the <a href="#the-fields-argument">HTML Specification</a> for a breakdown of elements and attributes returned.</div></td>
        </tr>
        <tr>
            <td class="posts indent">tags</td>
            <td class="posts indent default"><div>If the post is long enough, an array of tags generated from its specific content.</div></td>
        </tr>
        <tr>
            <td class="posts indent">humanLanguage</td>
            <td class="posts indent default"><div>Spoken/human language of the post, using two-letter <a href="http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes" target="_blank">ISO 639-1 nomenclature</a>.</div></td>
        </tr>
        <tr>
            <td class="posts indent">images</td>
            <td class="posts indent default"><div>If any images are detected within post content, they will be returned in a separate array. Individual array fields are the same as the <a href="/dev/docs/article">Article API's</a> <code>images</code> array.</div></td>
        </tr>
        <tr>
            <td class="posts indent">date</td>
            <td class="posts indent default"><div>Date of post, normalized in most cases to <a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec3.html#sec3.3">RFC 1123 (HTTP/1.1)</a>.</div></td>
        </tr>
        <tr>
            <td class="posts indent">author</td>
            <td class="posts indent default"><div>Name/username of the post author.</div></td>
        </tr>
        <tr>
            <td class="posts indent">authorUrl</td>
            <td class="posts indent default"><div>URL of the author profile page, if available.</div></td>
        </tr>
        <tr>
            <td class="posts indent">pageUrl</td>
            <td class="posts indent default"><div>URL of the page on which the post was found.</div></td>
        </tr>
        <tr>
            <td class="posts indent">diffbotUri</td>
            <td class="posts indent default"><div>Internal ID used for indexing.</div></td>
        </tr>
        <tr>
            <td class="">tags</td>
            <td class=" default"><div>Array of tags/entities as generated from analysis of all extracted <code>posts</code> and cross-referenced with <a href="http://wiki.dbpedia.org/About" target="_new">DBpedia</a>.</div></td>
        </tr>
        <tr>
            <td class="">participants</td>
            <td class=" default"><div>Number of unique participants in the discussion thread or comments.</div></td>
        </tr>
        <tr>
            <td class="">numPages</td>
            <td class=" default"><div>Number of pages in the thread concatenated to form the <code>posts</code> response. Use <code>maxPages</code> to define how many pages to concatenate. <a href="http://support.diffbot.com/automatic-apis/handling-multiple-page-articles/">More on automatic concatenation</a>.</div></td>
        </tr>
        <tr>
            <td class="">nextPage</td>
            <td class=" default"><div>If discussion spans multiple pages, <code>nextPage</code> will return the subsequent page URL.</div></td>
        </tr>
        <tr>
            <td class="">nextPages</td>
            <td class=" default"><div>Array of all page URLs concatenated in a multipage discussion. <a href="http://support.diffbot.com/automatic-apis/handling-multiple-page-articles/">More on automatic concatenation</a>.</div></td>
        </tr>
        <tr>
            <td class="">provider</td>
            <td class=" default"><div>Discussion service provider (e.g., Disqus, Facebook), if known.</div></td>
        </tr>
        <tr>
            <td class="">humanLanguage</td>
            <td class=" default"><div>Spoken/human language of the discussion / comment thread, using two-letter <a href="http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes" target="_blank">ISO 639-1 nomenclature</a>.</div></td>
        </tr>
        <tr>
            <td class="">rssUrl</td>
            <td class=" default"><div>URL of the discussion's RSS feed, if available.</div></td>
        </tr>
        <tr>
            <td class="">diffbotUri</td>
            <td class=" default"><div>Unique object ID. The <code>diffbotUri</code> is generated from the values of various Discussion fields and uniquely identifies the object. This can be used for deduplication.</div></td>
        </tr>

        <tr>
            <td colspan="2" class="header">Optional fields, available using <code>fields=</code> argument</td>
        </tr>
        <tr>
            <td class="">sentiment</td>
            <td class=" optional"><div>Returns a sentiment score of each individual post, a value ranging from -1.0 (very negative) to 1.0 (very positive).</div></td>
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
Remember — a happy robot is an authenticated robot!
</aside>

## Options
### Comment Extraction

By default the Article API will attempt to extract comments from article pages, using integrated functionality from the Diffbot Discussion API. (This behavior can be disabled using the argument `discussion=false`.)

Comment data will be returned in the `discussion` object (nested within the primary article object). The full syntax for discussion data is [available in the Discussion API documentation](#discussion-api).




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

If your content is not publicly available (e.g., behind a firewall), you can POST markup directly to the Discussion API endpoint for analysis:

`http://api.diffbot.com/v3/discussion?token={token}&url={url}`

Please note that the `url` argument is still required, and will be used to resolve any relative links contained in the markup.

Provide the content to analyze as your POST body, and specify the `Content-Type` header as `text/html`.

