# Discussion API

The Discussion API automatically structures and extracts entire threads or lists of reviews/comments from most discussion pages, forums, and similarly structured web 
 pages. It is also a part of the [Product API](#product-api) and the [Article API](#article-api) - it will detect reviews/comments on those automatically unless disabled, and return them as an array inside the main `objects` array. See the respective API docs for more information and examples.

## Request

```shell
curl "http://api.diffbot.com/v3/discussion?token={token}&url=http%3A%2F%2Fblog.diffbot.com%2Fdiffbots-new-product-api-teaches-robots-to-shop-online"
```

To use the Discussion API, perform an HTTP GET request on the following endpoint:


`GET http://api.diffbot.com/v3/discussion`

<aside class="notice">Remember to url-encode all querystring parameters when using cURL! In all other instances, consult the client documentation - most of the good ones handle this for you.</aside>


### Required Arguments

```php
<?php

$diffbot = new Diffbot('my_token');
$url = 'https://news.ycombinator.com/item?id=5608988';
$discussionApi = $diffbot->createDiscussionAPI($url);
```

| Argument           | Description    |
| ------------------ | --------------------------------------------------------------- |
| token              | Developer token|
| url                | Web page URL of the discussion to process (URL encoded)                   |

### Optional Arguments

```php
<?php

$discussionApi->setMeta(true);
 
// setters can also be chained

$discussionApi
            ->setBreadcrumb(true)
            ->setQuerystring(true)
            ->setLinks(true);
            
$discussionApi
            ->setSentiment(true)
            ->setMaxPages('all')
            ->setTimeout(30000);
```


| Argument           | Description    |
| ------------------ | --------------------------------------------------------------- |
| fields             | Used to specify optional fields to be returned by the Discussion API. See the [Fields](#the-fields-argument33) section below.         |
| timeout            | Set a value in milliseconds to terminate the response. By default the Article API has a 30-second (30000) timeout.     |
| callback           | Use for jsonp requests. Needed for cross-domain ajax.                          |
| maxPages           | Set the maximum number of pages in a thread to automatically concatenate in a single response. Default = 1 (no concatenation). Set maxPages=all to retrieve all pages of a thread regardless of length. Each individual page will count as a separate API call. |

### The Fields Argument

Use the `fields` argument to return optional fields in the JSON response. The default fields will always be returned (see [table below](#response31)). 

For example, to return `links` and `meta` (in addition to the default fields), your `&fields` argument would be:

`&fields=links,meta`

For nested arrays, use parentheses to retrieve specific fields, or * to return all sub-fields. For example, if the field `tags` were optional, you could tell Diffbot to only return `uri` sub-fields with `&fields=tags(uri)`.

Note that most clients will abstract this into setters or something equally simple to use (see `PHP` example to the right).

## Response 

> Example: processing the link https://news.ycombinator.com/item?id=5608988

```php
<?php

echo $result->numPosts; // prints out 8
echo $result->getPosts()[0]->getAuthor; // prints out "miket"

// or, get the whole json dump with
$dump = $result->getResponse()->getBody();

// or as a PHP array
$dump = $result->getResponse()->json();

```

```shell
curl 'http://api.diffbot.com/v3/discussion?token={token}&url=https%3A%2F%2Fnews.ycombinator.com%2Fitem%3Fid%3D5608988&mentos&fields=links,meta,querystring,breadcrumb'
```

> The full json dump will look something like this:

```json
{
  "request": {
    "pageUrl": "https://news.ycombinator.com/item?id=5608988",
    "api": "discussion",
    "version": 3,
    "fields": "links,meta,querystring,breadcrumb"
  },
  "objects": [
    {
      "tags": [
        {
          "id": 4715031,
          "count": 8,
          "prevalence": 0.5714285714285714,
          "label": "Diffbot",
          "type": "organization",
          "uri": "http://dbpedia.org/resource/Diffbot"
        },
        {
          "id": 881745,
          "count": 1,
          "prevalence": 0.07142857142857142,
          "label": "Domain name",
          "uri": "http://dbpedia.org/resource/Domain_name"
        },
        {
          "id": 874863,
          "count": 1,
          "prevalence": 0.07142857142857142,
          "label": "Open source",
          "uri": "http://dbpedia.org/resource/Open_source"
        },
        {
          "id": 868337,
          "count": 1,
          "prevalence": 0.07142857142857142,
          "label": "Android (operating system)",
          "type": "Http://wikidata.dbpedia.org/resource/Q386724",
          "uri": "http://dbpedia.org/resource/Android_(operating_system)"
        },
        {
          "id": 419727,
          "count": 1,
          "prevalence": 0.07142857142857142,
          "label": "Catcher",
          "uri": "http://dbpedia.org/resource/Catcher"
        }
      ],
      "querystring": {
        "id": "5608988"
      },
      "numPosts": 8,
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
          "html": "<p>(diffbot.com)<\\/p>",
          "humanLanguage": "en",
          "date": "Thu, 05 Feb 2015 00:00:00 GMT",
          "type": "post"
        },
        {
          "tags": [
            {
              "id": 4715031,
              "count": 4,
              "label": "Diffbot",
              "type": "organization",
              "uri": "http://dbpedia.org/resource/Diffbot"
            },
            {
              "id": 874863,
              "count": 1,
              "label": "Open source",
              "uri": "http://dbpedia.org/resource/Open_source"
            }
          ],
          "id": 1,
          "author": "johncoogan",
          "text": "Huge fan of DiffBot and awesome projects like this. Really cool analysis, thanks for posting.\\\n\\\nWould be possible for you to post / send me the original data? I have been very interested in working on more longitudinal analysis using DiffBot data and this seems like a fun and interesting place to start. I'm happy to open-source / clearly attribute DiffBot's contribution to whatever I find / hack together, and would feel a lot more comfortable about integrating DiffBot into larger projects in the future.\\\nPlease email me (in my profile) if this is a possibility. Thanks!\\\n\\\n\\\n-----",
          "pageUrl": "https://news.ycombinator.com/item?id=5608988",
          "diffbotUri": "post|3|-1972390462",
          "authorUrl": "https://news.ycombinator.com/user?id=johncoogan",
          "html": "<p>Huge fan of DiffBot and awesome projects like this. Really cool analysis, thanks for posting.<\\/p>\\\n<p>Would be possible for you to post / send me the original data? I have been very interested in working on more longitudinal analysis using DiffBot data and this seems like a fun and interesting place to start. I'm happy to open-source / clearly attribute DiffBot's contribution to whatever I find / hack together, and would feel a lot more comfortable about integrating DiffBot into larger projects in the future.<\\/p>\\\n<p>Please email me (in my profile) if this is a possibility. Thanks!<\\/p>\\\n<p>----- <\\/p>",
          "humanLanguage": "en",
          "type": "post"
        },
        {
          "tags": [
            {
              "id": 4715031,
              "count": 2,
              "label": "Diffbot",
              "type": "organization",
              "uri": "http://dbpedia.org/resource/Diffbot"
            },
            {
              "id": 1793183,
              "count": 1,
              "label": "Access token",
              "uri": "http://dbpedia.org/resource/Access_token"
            }
          ],
          "id": 2,
          "author": "tswaterman",
          "parentId": 1,
          "text": "Great idea! We'd be happy to share/help. If more people are interested, we'll figure out a good way to distribute the dataset generally. But in fact, you can extract the same data set, and add whatever other smart things you want along with it, using the Diffbot APIs. Everything we did to get this information is explained on our blog at\\\nhttp://blog.diffbot.com/diffbots-hackernews-trend-analyzer/ Sounds like you're already using the Diffbot service, but for anyone who's not, they can sign up for a free access token on our 'pricing' page at \\\nhttp://www.diffbot.com/ It's a few hundred thousand pages you'd need to analyze to get this, which doesn't quite fit under the free plan. You might not want to analyze as many years worth of stuff as we did for this demo, though.\\\n\\\nAll the pieces and services we used for this, including all the text extraction, topic detection, and crawling, are available to any user.\\\nHave fun with it, and keep us informed about whatever cool stuff you build with it, and of course tell us about any features or capabilities you wish Diffbot can provide.\\\n\\\n\\\n-----",
          "pageUrl": "https://news.ycombinator.com/item?id=5608988",
          "diffbotUri": "post|3|-1080445506",
          "authorUrl": "https://news.ycombinator.com/user?id=tswaterman",
          "html": "<p>Great idea! We'd be happy to share/help. If more people are interested, we'll figure out a good way to distribute the dataset generally. But in fact, you can extract the same data set, and add whatever other smart things you want along with it, using the Diffbot APIs. Everything we did to get this information is explained on our blog at<\\/p>\\\n<pre><code>    http://blog.diffbot.com/diffbots-hackernews-trend-analyzer/\\\n<\\/code><\\/pre>\\\n<p>Sounds like you're already using the Diffbot service, but for anyone who's not, they can sign up for a free access token on our 'pricing' page at <a href=\"http://www.diffbot.com/\">http://www.diffbot.com/<\\/a> It's a few hundred thousand pages you'd need to analyze to get this, which doesn't quite fit under the free plan. You might not want to analyze as many years worth of stuff as we did for this demo, though.<\\/p>\\\n<p>All the pieces and services we used for this, including all the text extraction, topic detection, and crawling, are available to any user.<\\/p>\\\n<p>Have fun with it, and keep us informed about whatever cool stuff you build with it, and of course tell us about any features or capabilities you wish Diffbot can provide.<\\/p>\\\n<p>----- <\\/p>",
          "humanLanguage": "en",
          "type": "post"
        },
        {
          "tags": [
            {
              "id": 4715031,
              "count": 2,
              "label": "Diffbot",
              "type": "organization",
              "uri": "http://dbpedia.org/resource/Diffbot"
            },
            {
              "id": 419727,
              "count": 1,
              "label": "Catcher",
              "uri": "http://dbpedia.org/resource/Catcher"
            },
            {
              "id": 205322,
              "count": 1,
              "label": "Application programming interface",
              "uri": "http://dbpedia.org/resource/Application_programming_interface"
            }
          ],
          "id": 3,
          "author": "mayank",
          "text": "Funny, I just built a HN article catcher that uses Diffbot to collect and classify submissions from the /new page [1]. I've been a Diffbot fan for quite a while now (although their entity recognition/tag classifier needs a bit of work as you can see from the categorization on my catcher page below).\\\n\\\n[1] http://lahiri.me/more\\\nI should add that their API is fantastic, and far better than using BeautifulSoup/NLTK for extracting textual content from webpages.\\\n\\\n\\\n-----",
          "pageUrl": "https://news.ycombinator.com/item?id=5608988",
          "diffbotUri": "post|3|-398235096",
          "authorUrl": "https://news.ycombinator.com/user?id=mayank",
          "html": "<p>Funny, I just built a HN article catcher that uses Diffbot to collect and classify submissions from the /new page [1]. I've been a Diffbot fan for quite a while now (although their entity recognition/tag classifier needs a bit of work as you can see from the categorization on my catcher page below).<\\/p>\\\n<p>[1] <a href=\"http://lahiri.me/more\">http://lahiri.me/more<\\/a><\\/p>\\\n<p>I should add that their API is fantastic, and far better than using BeautifulSoup/NLTK for extracting textual content from webpages.<\\/p>\\\n<p>----- <\\/p>",
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
          "html": "<p>Cool! How many articles, or what time period, did you use for this? It looks like you're using only a subset of the topic tags -- did you make a list of 'interesting stuff' to filter against?<\\/p>",
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
          "html": "<p>It's been running for about a week I think, and I'm just taking the top 80 or so tags by article count. Glad you like it :)<\\/p>",
          "humanLanguage": "en",
          "type": "post"
        },
        {
          "tags": [
            {
              "id": 868337,
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
          "html": "<p>Had to figure out how to use it ... but interesting once you do! Android vs IPhone on Hackernews frontpage shows spike in iphone on launch dates, but mediocre to no activity for android. is it because android is less interesting and not as innovative? or not as fun to talk/read about?<\\/p>",
          "humanLanguage": "en",
          "type": "post"
        },
        {
          "tags": [
            {
              "id": 881745,
              "count": 1,
              "label": "Domain name",
              "uri": "http://dbpedia.org/resource/Domain_name"
            }
          ],
          "id": 7,
          "author": "minimax",
          "text": "Neat! Wish I could select by just domain name (i.e. just nytimes.com rather than dozen or so whatever.nytimes.com subdomains).",
          "pageUrl": "https://news.ycombinator.com/item?id=5608988",
          "diffbotUri": "post|3|-869746168",
          "authorUrl": "https://news.ycombinator.com/user?id=minimax",
          "html": "<p>Neat! Wish I could select by just domain name (i.e. just nytimes.com rather than dozen or so whatever.nytimes.com subdomains).<\\/p>",
          "humanLanguage": "en",
          "type": "post"
        }
      ],
      "links": [
        "http://www.ycombinator.com",
        "https://news.ycombinator.com/news",
        "https://news.ycombinator.com/newest",
        "https://news.ycombinator.com/newcomments",
        "https://news.ycombinator.com/show",
        "https://news.ycombinator.com/ask",
        "https://news.ycombinator.com/jobs",
        "https://news.ycombinator.com/submit",
        "https://news.ycombinator.com/login?goto=item%3Fid%3D5608988",
        "https://news.ycombinator.com/vote?for=5608988&dir=up&goto=item%3Fid%3D5608988",
        "http://diffbot.com/robotlab/hackernews/",
        "https://news.ycombinator.com/user?id=miket",
        "https://news.ycombinator.com/item?id=5608988",
        "https://news.ycombinator.com/vote?for=5609164&dir=up&goto=item%3Fid%3D5608988",
        "https://news.ycombinator.com/user?id=johncoogan",
        "https://news.ycombinator.com/item?id=5609164",
        "https://news.ycombinator.com/vote?for=5609252&dir=up&goto=item%3Fid%3D5608988",
        "https://news.ycombinator.com/user?id=tswaterman",
        "https://news.ycombinator.com/item?id=5609252",
        "http://www.diffbot.com",
        "https://news.ycombinator.com/vote?for=5609116&dir=up&goto=item%3Fid%3D5608988",
        "https://news.ycombinator.com/user?id=mayank",
        "https://news.ycombinator.com/item?id=5609116",
        "http://lahiri.me/more",
        "https://news.ycombinator.com/vote?for=5609278&dir=up&goto=item%3Fid%3D5608988",
        "https://news.ycombinator.com/item?id=5609278",
        "https://news.ycombinator.com/vote?for=5609731&dir=up&goto=item%3Fid%3D5608988",
        "https://news.ycombinator.com/item?id=5609731",
        "https://news.ycombinator.com/vote?for=5609057&dir=up&goto=item%3Fid%3D5608988",
        "https://news.ycombinator.com/user?id=tliou",
        "https://news.ycombinator.com/item?id=5609057",
        "https://news.ycombinator.com/vote?for=5609100&dir=up&goto=item%3Fid%3D5608988",
        "https://news.ycombinator.com/user?id=minimax",
        "https://news.ycombinator.com/item?id=5609100",
        "https://news.ycombinator.com/newsguidelines.html",
        "https://news.ycombinator.com/newsfaq.html",
        "http://ycombinator.com",
        "https://github.com/HackerNews/API",
        "https://news.ycombinator.com/security.html",
        "https://news.ycombinator.com/lists",
        "https://news.ycombinator.com/bookmarklet.html",
        "https://news.ycombinator.com/dmca.html",
        "http://www.ycombinator.com/apply/"
      ],
      "humanLanguage": "en",
      "confidence": 0.05271753612809388,
      "type": "discussion",
      "participants": 6,
      "meta": {
        "title": "Show HN: Analysis of 2.5 Years of Frontpage Articles | Hacker News",
        "referrer": "origin"
      },
      "title": "Show HN: Analysis of 2.5 Years of Frontpage Articles",
      "diffbotUri": "discussion|3|-110040828",
      "numPages": 1
    }
  ]
}
```

Diffbot's V3 APIs return information about **all** identified objects on a submitted page.

Each V3 response includes a `request` object (which returns request-specific metadata), and an `objects` array, which will include the extracted information for all objects on a submitted page. The Discussion API returns all post data in a single object within the `objects` array.

Within the Article and Product APIs (to extract comments or review data), discussion data will be returned within the nested `discussion` object.

The Discussion API `objects` / `discussion` response will include the following fields:

---

**Default Fields**


| Field              | Description                |
| ------------------------------------------------- | --------------------------------------------------------------- |
| type               | Type of object (always `discussion`).                       |
| pageUrl            | URL of submitted page / page from which the discussion is extracted.         |
| resolvedPageUrl    | Returned if the `pageUrl` redirects to another URL.         |
| title              | Title of the discussion.   |
| numPosts           | Number of individual posts in the thread.                 |
| posts              | Array of individual posts. |
| posts.type               | Type of element (always `post`).                            |
| posts.id                 | ID of the individual post. The first post of a thread will have an ID of 0.  |
| posts.parentId           | ID of the parent, if the post is a reply or response.     |
| posts.text               | Full text of the extracted post.                          |
| posts.html               | Diffbot-normalized HTML of the extracted post. Please see the [HTML Specification](#html-field-specification) for a breakdown of elements and attributes returned.                         |
| posts.tags               | If the post is long enough, an array of tags generated from its specific content.                           |
| posts.humanLanguage     | Spoken/human language of the post, using two-letter [ISO 639-1 nomenclature](http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). |
| posts.images             | If any images are detected within post content, they will be returned in a separate array. Individual array fields are the same as the [Article API](#article-api)'s images array.               |
| posts.date               | Date of post, normalized in most cases to [RFC 1123 (HTTP/1.1)](http://www.w3.org/Protocols/rfc2616/rfc2616-sec3.html#sec3.3).               |
| posts.author             | Name/username of the post author.                         |
| posts.authorUrl          | URL of the author profile page, if available.             |
| posts.pageUrl            | URL of the page on which the post was found.              |
| posts.diffbotUri         | Internal ID used for indexing.                            |
| tags              | Array of tags/entities, generated from analysis of the extracted `text` and cross-referenced with [DBpedia](http://wiki.dbpedia.org/About).|
| participants       | Number of unique participants in the discussion thread or comments.          |
| numPages          | Number of pages automatically concatenated to form the text or html response. (By default, Diffbot will concatenate up to 20 pages of a single article.) [More on automatic concatenation](http://support.diffbot.com/automatic-apis/handling-multiple-page-articles).                |
| nextPages         | Array of all page URLs concatenated in a multipage article.       |
| nextPage           | If discussion spans multiple pages, nextPage will return the subsequent page URL.                           |
| provider           | Discussion service provider (e.g., Disqus, Facebook), if known.              |
| humanLanguage     | Returns the (spoken/human) language of the submitted page, using two-letter [ISO 639-1 nomenclature](http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). |
| rssUrl             | URL of the discussion's RSS feed, if available.           |
| diffbotUri         | Unique object ID. The diffbotUri is generated from the values of various Discussion fields and uniquely identifies the object. This can be used for deduplication.|

---

**Optional fields, available using the `fields=` argument**


| Field              | Description                |
| ------------------------------------------------- | --------------------------------------------------------------- |
| sentiment          | Returns a sentiment score of each individual post, a value ranging from -1.0 (very negative) to 1.0 (very positive).           |
| links             | Returns a top-level object (`links`) containing all hyperlinks found on the page.                     |
| meta              | Returns a top-level object (meta) containing the full contents of page meta tags, including sub-arrays for <a href="http://ogp.me/" target="_new">OpenGraph</a> tags, <a href="https://dev.twitter.com/docs/cards/markup-reference" target="_new">Twitter Card</a> metadata, <a href="http://www.schema.org" target="_new">schema.org</a> microdata, and -- if available -- <a href="http://www.oembed.com" target="_new">oEmbed</a> metadata. See example JSON output to the right. |
| querystring       | Returns any key/value pairs present in the URL querystring. Items without a discrete value will be returned as `true`.                            |
| breadcrumb        | Returns a top-level array (`breadcrumb`) of URLs and link text from page breadcrumbs.                 |
                                |

## Options

### Comment Extraction

By default the Article API will attempt to extract comments from article pages, using integrated functionality from the Diffbot [Discussion API](#discussion-api) (This behavior can be disabled using the argument `discussion=false`). The same goes for reviews on Product API calls.

Comment / review data will be returned in the `discussion` object (nested within the primary article / product object). 

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

If your content is not publicly available (e.g., behind a firewall), you can POST markup or plain text directly to the Article API endpoint for analysis:

`http://api.diffbot.com/v3/article?token={token}&url={url}`

Provide the content to analyze as your POST body, and specify the `Content-Type` header as `text/html` (for full markup) or `text/plain` (for text-only).

Please note that if you submit HTML (default, if `Content-Type` is missing), the `url` argument is still required, and will be used to resolve any relative links contained in the markup.