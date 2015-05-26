# Video API
The Video API automatically extracts detailed video information—including most metadata, thumbnail images, direct video URL and embed code—from nearly any video page or video platform on the web.

## Request

> Definition

``` 
GET http://api.diffbot.com/v3/video
```

> Example Request

```shell
curl "http://api.diffbot.com/v3/video?token={token}&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DVNv3EZEUgok"
```

To use the Video API, perform a HTTP GET request on the following endpoint:




`GET http://api.diffbot.com/v3/video`
<aside class="notice">Remember to url-encode all querystring parameters!</aside>


<table class="controls table table-bordered" border="0" cellpadding="5">
  <thead><tr><th>Argument</th><th>Description</th></tr></thead>

    <tbody><tr>
        <td class="">token</td>
        <td class=" default"><div>Developer token</div></td>
    </tr>
    <tr>
        <td class="">url</td>
        <td class=" default"><div>Web page URL of the video to process (URL encoded)</div></td>
    </tr>

    <tr>
        <td colspan="2" class="header">Optional arguments</td>
    </tr>
    <tr>
        <td class="">fields</td>
        <td class=" optional"><div>Used to specify optional fields to be returned by the Video API. See the <a href="#the-fields-argument54">Fields</a> section below.</div></td>
    </tr>
    <tr>
        <td class="">timeout</td>
        <td class=" optional"><div>Set a value in milliseconds to terminate the response. By default the Video API has a 30-second (30000) timeout.</div></td>
    </tr>
    <tr>
        <td class="">callback</td>
        <td class=" optional"><div>Use for jsonp requests. Needed for cross-domain ajax.</div></td>
    </tr></tbody></table>



### The Fields Argument

Use the `fields` argument to return optional fields in the JSON response. The default fields will always be returned. For nested arrays, use parentheses to retrieve specific fields, or `*` to return all sub-fields.

For example, to return `breadcrumb` and `links` (in addition to the default fields), your &fields argument would be:

`&fields=breadcrumb,links`


## Response 


> If successful, you'll receive this response:

```json
{
  "request": {
    "pageUrl": "https://www.youtube.com/watch?v=VNv3EZEUgok",
    "api": "video",
    "version": 3
  },
  {
  "objects": [
    {
      "type": "video",
      "title": "Create a Custom API Using Diffbot's Custom API Toolkit",
      "text": "This demonstration shows how to create a completely custom API using Diffbot's Custom API Toolkit. In it we show how to extract the \"What's Hot\" / Trending links from http://www.mashable.com.",
      "pageUrl": "https://www.youtube.com/watch?v=VNv3EZEUgok",
      "embedUrl": "http://www.youtube.com/v/VNv3EZEUgok?autohide=1&version=3",
      "humanLanguage": "en",
      "date": "Fri, 02 Aug 2013 07:00:00 GMT",
      "url": "https://r5---sn-qxo7sn7r.googlevideo.com/videoplayback?signature=3F99256DF92E9095B47FAC373A4BAADC5DBF3D36.D840BFEA083EE15085D0FE1F2F4C724551E7A4D7&sver=3&fexp=911305%2C912108%2C916944%2C930666%2C932404%2C940000%2C947209%2C947215%2C948124%2C948900%2C952302%2C952901%2C953912%2C957103%2C957201%2C958603&ratebypass=yes&requiressl=yes&ipbits=0&sparams=id%2Cip%2Cipbits%2Citag%2Cmm%2Cms%2Cmv%2Cratebypass%2Crequiressl%2Csource%2Cupn%2Cexpire&key=yt5&ip=146.148.32.139&itag=22&source=youtube&mv=u&ms=au&mm=31&mt=1415157849&id=o-AJ5iG1T6_yn-_qUHjcNok6XqTznNX6LXeagB6-mm8XQM&expire=1415179514&upn=wMziid6h3DY",
      "author": "Diffbot",
      "html": "<iframe width=\"459\" height=\"344\" src=\"http://www.youtube.com/embed/VNv3EZEUgok?feature=oembed\" frameborder=\"0\" allowfullscreen></iframe>",
      "mime": "video/mp4",
      "duration": 343,
      "naturalWidth": 1280,
      "naturalHeight": 720,
      "viewCount": 1000
      "images": [
        {
          "title": "Create a Custom API Using Diffbot's Custom API Toolkit",
          "url": "http://i.ytimg.com/vi/VNv3EZEUgok/hqdefault.jpg",
        }
      ]
      "diffbotUri": "video|3|566075164",
    }
  ],
}
```




Diffbot's V3 APIs return information about **all** identified objects on a submitted page.

Each V3 response includes a `request` object (which returns request-specific metadata), and an `objects` array, which will include the extracted information for all objects on a submitted page.

Objects in the Video API's `objects` array will include the following fields:
<table class="controls table table-bordered" id="fields" border="0" cellpadding="5">
  <thead><tr><th>Field</th><th>Description</th></tr></thead>

      <tbody><tr>
          <td class="">type</td>
          <td class=" default"><div>Type of object (always <code>video</code>).</div></td>
      </tr>
      <tr>
          <td class="">pageUrl</td>
          <td class=" default"><div>URL of submitted page / page from which the video is extracted.</div></td>
      </tr>
      <tr>
          <td class="">resolvedPageUrl</td>
          <td class=" default"><div>Returned if the <code>pageUrl</code> redirects to another URL.</div></td>
      </tr>
      <tr>
          <td class="">title</td>
          <td class=" default"><div>Title of the video.</div></td>
      </tr>
      <tr>
          <td class="">text</td>
          <td class=" default"><div>Text description, if available, of the video.</div></td>
      </tr>
      <tr>
          <td class="">url</td>
          <td class=" default"><div>Direct link to source video file, if available.</div></td>
      </tr>
      <tr>
          <td class="">html</td>
          <td class=" default"><div>Embeddable HTML of the video (if available), typically an <code>IFRAME</code> or <code>VIDEO</code> object.</div></td>
      </tr>
      <tr>
          <td class="">embedUrl</td>
          <td class=" default"><div>Embeddable URL, if available.</div></td>
      </tr>
      <tr>
          <td class="">author</td>
          <td class=" default"><div>Video uploader or creator, if available.</div></td>
      </tr>
      <tr>
          <td class="">date</td>
          <td class=" default"><div>Date of extracted video, normalized in most cases to <a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec3.html#sec3.3">RFC 1123 (HTTP/1.1)</a>.</div></td>
      </tr>
      <tr>
          <td class="">duration</td>
          <td class=" default"><div>Duration in seconds of the Video.</div></td>
      </tr>
      <tr>
          <td class="">viewCount</td>
          <td class=" default"><div>Number of Video views, if available on the page.</div></td>
      </tr>
      <tr>
          <td class="">naturalHeight</td>
          <td class=" default"><div>Raw video height, if available, in pixels.</div></td>
      </tr>
      <tr>
          <td class="">naturalWidth</td>
          <td class=" default"><div>Raw video width, if available, in pixels.</div></td>
      </tr>
      <tr>
          <td class="parent">images</td>
          <td class="parent default"><div>Array of images, if present within the video.</div></td>
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
          <td class="">mime</td>
          <td class=" default"><div>MIME type, if available, as specified by the Video's "Content-Type."</div></td>
      </tr>
      <tr>
          <td class="">humanLanguage</td>
          <td class=" default"><div>Returns the (spoken/human) language of the submitted page, using two-letter <a href="http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes" target="_blank">ISO 639-1 nomenclature</a>.</div></td>
      </tr>
      <tr>
          <td class="">diffbotUri</td>
          <td class=" default"><div>Unique object ID. The <code>diffbotUri</code> is generated from the values of various Video fields and uniquely identifies the object. This can be used for deduplication.</div></td>
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

If your content is not publicly available (e.g., behind a firewall), you can POST markup directly to the Video API endpoint for analysis:

`http://api.diffbot.com/v3/video?token={token}&url={url}`

Please note that the `url` argument is still required, and will be used to resolve any relative links contained in the markup.

Provide the content to analyze as your POST body, and specify the `Content-Type` header as `text/html`.