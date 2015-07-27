## Crawlbot API

The Crawlbot API allows you to programmatically manage [Crawlbot](#crawlbot) crawls and retrieve output.


### Creating or Updating a Crawl
To create a crawl, make a GET request to `http://api.diffbot.com/v3/crawl`.

Provide the following data:

<table class="controls table table-bordered" border="0" cellpadding="5">
  <thead><tr><th>Parameter</th><th>Description</th></tr></thead>
  <tbody>
  <tr><td>token</td><td>Developer <a href="/pricing">token</a></td></tr>
  <tr><td>name</td><td>Job name. This should be a unique identifier and can be used to modify your crawl or retrieve its output.</td></tr>
  <tr><td>seeds</td><td>Seed URL(s). Must be <a href="http://en.wikipedia.org/wiki/Percent-encoding" target="_blank">URL encoded</a>. Separate multiple URLs with whitespace to spider multiple sites within the same crawl. By default Crawlbot will restrict spidering to the entire  <strong>domain</strong> ("http://blog.diffbot.com" will include URLs at "http://www.diffbot.com").</td></tr>
   <tr><td>apiUrl</td><td>Full Diffbot API URL through which to process pages. E.g., <code>&amp;apiUrl=http://api.diffbot.com/v3/article</code> to process matching links via the <a href="#article-api">Article API</a>. The Diffbot API URL can include querystring parameters to tailor the output. For example, <code>&amp;apiUrl=http://api.diffbot.com/v3/product?fields=querystring,meta</code> will process matching links using the <a href="#product-api">Product API</a>, and also return the <code>querystring</code> and <code>meta</code> fields.
  <br><br>
  To automatically identify and process content using our <a href="/products/automatic/classifier">Page Classifier API</a> (Smart Processing), pass <code>apiUrl=http://api.diffbot.com/v3/analyze?mode=auto</code> to return all page-types. See full Page Classifier documentation under the <a href="#diffbot's-apis">Automatic APIs documentation</a>.
  <br><br>
  Be sure to <a href="http://en.wikipedia.org/wiki/Percent-encoding" target="_blank">URL encode</a> your Diffbot API actions.</td></tr>
  </tbody>
  </table>

  You can refine your crawl using the following optional controls. [Read more on crawling versus processing.](http://support.diffbot.com/crawlbot/whats-the-difference-between-crawling-and-processing/)


  <table class="controls table table-bordered" border="0" cellpadding="5">
  <thead><tr><th>Parameter</th><th>Description</th></tr></thead>
  <tbody>
  <tr><td><urlCrawlPattern</td><td>Specify ||-separated <strong>strings</strong> to limit pages crawled to those whose URLs contain <em>any</em> of the content strings. You can use the exclamation point to specify a negative string, e.g. <code>!product</code> to exclude URLs containing the string "product," and the <code>^</code> and <code>$</code> characters to limit matches to the beginning or end of the URL.<br><br>The use of a <code>urlCrawlPattern</code> will allow Crawlbot to spider outside of the seed domain; it will follow all matching URLs regardless of domain.</td></tr>
  <tr><td>urlCrawlRegEx</td><td>Specify a regular expression to limit pages <strong>crawled</strong> to those URLs that match your expression. This will override any <code>urlCrawlPattern</code> value.<br><br>The use of a <code>urlCrawlRegEx</code> will allow Crawlbot to spider outside of the seed domain; it will follow all matching URLs regardless of domain.</td></tr>
  <tr><td>urlProcessPattern</td><td>Specify ||-separated <strong>strings</strong> to limit pages processed to those whose URLs contain <em>any</em> of the content strings. You can use the exclamation point to specify a negative string, e.g. <code>!/category</code> to exclude URLs containing the string "/category," and the <code>^</code> and <code>$</code> characters to limit matches to the beginning or end of the URL.</td></tr>
  <tr><td>urlProcessRegEx</td><td>Specify a regular expression to limit pages <strong>processed</strong> to those URLs that match your expression. This will override any <code>urlProcessPattern</code> value.</td></tr>
  <tr><td>pageProcessPattern</td><td>Specify ||-separated strings to limit pages <strong>processed</strong> to those whose HTML contains <em>any</em> of the content strings.</td></tr>
</tbody>
  </table>


Additional (optional) Parameters:


  <table class="controls table table-bordered" border="0" cellpadding="5">
  <thead><tr><th>Parameter</th><th>Description</th></tr></thead>
  <tbody>
  <tr><td>maxHops</td><td>Specify the depth of your crawl. A <code>maxHops=0</code> will limit <strong>processing</strong> to the seed URL(s) only -- no other links will be processed; <code>maxHops=1</code> will process all (otherwise matching) pages whose links appear on seed URL(s); <code>maxHops=2</code> will process pages whose links appear on those pages; and so on.<br><br>By default (<code>maxHops=-1</code>) Crawlbot will crawl and process links at any depth.</td></tr>
  <tr><td>maxToCrawl</td><td>Specify max pages to spider. Default: 100,000.</td></tr>
  <tr><td>maxToProcess</td><td>Specify max pages to process through Diffbot APIs. Default: 100,000.</td></tr>

  <tr><td>notifyEmail</td><td>Send a message to this email address when the crawl hits the <code>maxToCrawl</code> or <code>maxToProcess</code> limit, or when the crawl completes.</td></tr>
  <tr><td>notifyWebhook</td><td>Pass a URL to be notified when the crawl hits the <code>maxToCrawl</code> or <code>maxToProcess</code> limit, or when the crawl completes. You will receive a POST with <code>X-Crawl-Name</code> and <code>X-Crawl-Status</code> in the headers, and the full <a href="#response">JSON response</a> in the POST body.<br><br>We've integrated with Zapier to make webhooks even more powerful; <a href="http://support.diffbot.com/crawlbot/using-zapier-with-crawlbot-or-bulk-api-jobs/">read more</a> on what you can do with Zapier and Diffbot.</td></tr>
  <tr><td>crawlDelay</td><td>Wait this many seconds between each URL crawled from a single IP address. Specify the number of seconds as an integer or floating-point number (e.g., <code>crawlDelay=0.25</code>).</td></tr>

  <tr><td>repeat</td><td>Specify the number of days as a floating-point (e.g. <code>repeat=7.0</code>) to repeat this crawl. By default crawls will not be repeated.</td></tr>
  <tr><td>onlyProcessIfNew</td><td>By default repeat crawls will only process new (previously unprocessed) pages. Set to 0 (<code>onlyProcessIfNew=0</code>) to process all content on repeat crawls.</td></tr>
  <tr><td>maxRounds</td><td>Specify the maximum number of crawl repeats. By default (<code>maxRounds=0</code>) repeating crawls will continue indefinitely.</td></tr>
  </tbody>
  </table>


#### Response
Upon adding a new crawl, you will receive a success message in the JSON response, in addition to full crawl details:

```json
"response": "Successfully added urls for spidering."
```




### Pausing, Restarting or Deleting Crawls
You can manage your crawls by making GET requests to the same endpoint, `http://api.diffbot.com/v3/crawl`.

Provide the following data:

<table class="controls table table-bordered" border="0" cellpadding="5">
  <thead><tr><th>Parameter</th><th>Description</th></tr></thead>
  <tbody>
  <tr><td>token</td><td>Developer <a href="/pricing">token</a></td></tr>
  <tr>
  <td>name</td>
  <td>Job name as defined when the crawl was created.</td>
  </tr>
  <tr>
  <td colspan="2"><strong>Job-control arguments</strong></td>
  </tr>
  <tr>
  <td>roundStart</td>
  <td>Pass <code>roundStart=1</code> to force the start of a new crawl "round" (manually repeat the crawl). If <code>onlyProcessIfNew</code> is set to 1 (default), only newly-created pages will be processed.</td>
  </tr>
  <tr>
  <td>pause</td>
  <td>Pass <code>pause=1</code> to pause a crawl. Pass <code>pause=0</code> to resume a paused crawl.</td>
  </tr>
  <tr>
  <td>restart</td>
  <td>Restart removes all crawled data while maintaining crawl settings. Pass <code>restart=1</code> to restart a crawl.</td>
  </tr>
  <tr>
  <td>delete</td>
  <td>Pass <code>delete=1</code> to delete a crawl, and all associated data, completely.</td>
  </tr>
</tbody></table>



### Retrieving Bulk API Data
To download results please make a GET request to the following URLs, replacing `token` and `jobName` with your token and bulk job name, respectively. The JSON data and URLs report URLs are also available in the Crawlbot JSON response, as `downloadJson` and `downloadUrls`.



<table class="controls table table-bordered" border="0" cellpadding="5">
  <thead><tr><th>URL</th><th>Description</th></tr></thead>
  <tbody>
  <tr><td>http://api.diffbot.com/v3/crawl/download/token-jobName_data.json</td><td>Download all JSON objects (as processed by Diffbot APIs).</td></tr>
  <tr><td>http://api.diffbot.com/v3/crawl/download/token-jobName_data.csv</td><td>Download a subset of content -- top-level fields only -- as a comma-separated values (CSV) file.</td></tr>
  <tr><td colspan="2"><strong>For diagnostic data:</strong></td></tr>
  <tr><td>http://api.diffbot.com/v3/crawl/download/token-jobName_urls.csv</td><td>Download the "URLs report" CSV file. This lists all URLs encountered by Crawlbot, and the most recent status for each. Useful for debugging.</td></tr>
   </tbody>
  </table>


### Using the Search API to Retrieve Crawl Data

You can also use Diffbot's [Search API](#search-api) to fine-tune the data retrieved from one (or multiple) Crawlbot or Bulk API jobs.

[Search API documentation](#search-api)

### Viewing Crawl Details
Your active crawls (and any active Bulk API jobs) will be returned in the `jobs` object in a request made to `http://api.diffbot.com/v3/crawl`.

To retrieve a single crawl's details, provide the crawl's `name` in your request:

<table class="controls table table-bordered" border="0" cellpadding="5">
  <thead><tr><th>Parameter</th><th>Description</th></tr></thead>
  <tbody>
  <tr><td>token</td><td>Developer <a href="/pricing">token</a></td></tr>
  <tr><td>name</td><td>Name of crawl to retrieve.</td></tr>
   </tbody>
  </table>

To view all crawls, simply omit the `name` parameter.

### Crawlbot Job Response
> Sample response from a single crawl:

```json
{
  "jobs": [
    {
      "name": "crawlJob", 
      "type": "crawl", 
      "jobCreationTimeUTC": 1427410692, 
      "jobCompletionTimeUTC": 1427410798, 
      "jobStatus": {
        "status": 9, 
        "message": "Job has completed and no repeat is scheduled."
      }, 
      "sentJobDoneNotification": 1, 
      "objectsFound": 177, 
      "urlsHarvested": 2152, 
      "pageCrawlAttempts": 367, 
      "pageCrawlSuccesses": 365, 
      "pageCrawlSuccessesThisRound": 365, 
      "pageProcessAttempts": 210, 
      "pageProcessSuccesses": 210, 
      "pageProcessSuccessesThisRound": 210, 
      "maxRounds": 0, 
      "repeat": 0.0, 
      "crawlDelay": 0.25, 
      "obeyRobots": 1, 
      "maxToCrawl": 100000, 
      "maxToProcess": 100000, 
      "onlyProcessIfNew": 1, 
      "seeds": "http://support.diffbot.com", 
      "roundsCompleted": 0, 
      "roundStartTime": 0, 
      "currentTime": 1432312443, 
      "currentTimeUTC": 1432312443, 
      "apiUrl": "http://api.diffbot.com/v3/analyze", 
      "urlCrawlPattern": "", 
      "urlProcessPattern": "", 
      "pageProcessPattern": "", 
      "urlCrawlRegEx": "", 
      "urlProcessRegEx": "", 
      "maxHops": -1, 
      "downloadJson": "http://api.diffbot.com/v3/crawl/download/sampletoken-crawlJob_data.json", 
      "downloadUrls": "http://api.diffbot.com/v3/crawl/download/sampletoken-crawlJob_urls.csv", 
      "notifyEmail": "support@diffbot.com", 
      "notifyWebhook": "http://www.diffbot.com"
    }
  ]
}

```

This will return a JSON response of your token's crawls and Bulk API jobs. 


### Status Codes
The `jobStatus` object will return the following status codes and associated messages:

<table class="controls table table-bordered table-condensed" border="0" cellpadding="5">
  <thead><tr><th>Status</th><th>Message</th></tr></thead>
  <tbody>
<tr><td>0</td><td>Job is initializing</td></tr>
<tr><td>1</td><td>Job has reached maxRounds limit</td></tr>
<tr><td>2</td><td>Job has reached maxToCrawl limit</td></tr>
<tr><td>3</td><td>Job has reached maxToProcess limit</td></tr>
<tr><td>4</td><td>Next round to start in _____ seconds</td></tr>
<tr><td>5</td><td>No URLs were added to the crawl</td></tr>
<tr><td>6</td><td>Job paused</td></tr>
<tr><td>7</td><td>Job in progress</td></tr>
<tr><td>8</td><td>All crawling temporarily paused by root administrator for maintenance.</td></tr>
<tr><td>9</td><td>Job has completed and no repeat is scheduled</td></tr>
   </tbody>
  </table>

## Crawlbot URL Report

The URL Report provides status on every URL crawled and/or processed by a Crawlbot or Bulk API job.

The report is a comma-separated-values (CSV) file, and is available to download from your crawl or bulk job status page as soon as a job has begun—

![Bulk Processing URL Report](/images/url_report.png "Download the URL report using the Detailed URL report (CSV) link.")
Download the URL report using the "Detailed URL report (CSV)" link.

—or, using the Crawlbot or Bulk Service API, via the `downloadUrls` field.

Each row corresponds to a single URL evaluated, and provides the following information:

<table class="controls table table-bordered urls">
<thead><tr><th>Column</th><th>Description</th></tr></thead>
<tbody><tr>
<td>URL</td>
<td>Web page URL evaluated</td>
</tr>
<tr>
    <td>Doc ID</td>
    <td>Document ID of the crawled page. This corresponds to the <code>docId</code> field returned in crawl or bulk job JSON data.</td>
</tr>
<tr>
    <td>URL Discovered Time</td>
    <td>Time the URL was first seen/encountered.</td>
</tr>
<tr>
    <td>Crawled Time</td>
    <td>Time the URL was crawled (downloaded and its source spidered for links).</td>
</tr>
<tr>
    <td>Content Length</td>
    <td>Number of characters comprising the HTML source.</td>
</tr>
<tr>
    <td>Duplicate Of</td>
    <td>If the page source is an exact duplicate of another page, the Doc ID of the duplicate page will be returned.</td>
</tr>
<tr>
    <td>Redirects</td>
    <td>Number of redirects pursued before arriving at the final destination URL.</td>
</tr>
<tr>
    <td>Redirected To</td>
    <td>Ultimate destination URL if redirected.</td>
</tr>
<tr>
    <td>Robots.txt Crawl Delay (ms)</td>
    <td>If the page is subject to a robots.txt "crawl delay" the value in milliseconds will be returned.</td>
</tr>
<tr>
    <td>Crawl Round</td>
    <td>If the crawl is a repeating/recurring crawl, the crawl "round" in which this URL was evaluated. Note: URLs will be duplicated for each round in which they are crawled.</td>
</tr>
<tr>
    <td>Crawl Try #</td>
    <td>If there is an error crawling the page (spidering for links), any retries will be enumerated.</td>
</tr>
<tr>
    <td>Hop Count</td>
    <td>This indicates the page's distance from seed(s): "1" indicates the URL was linked-to from a seed; "2" indicates the URL appeared on a page that itself was linked-to from a seed. Hops can be used to narrow crawling via Crawlbot's <code>maxHops</code> argument.</td>
</tr>
<tr>
    <td>Crawl Status</td>
    <td>Returns "Success" if the page was successfully crawled (spidered for links).</td>
</tr>
<tr>
    <td>Diffbot URI</td>
    <td>If the page was processed via a Diffbot API, and an object—product, article, image, discussion, etc.—found, the object's <code>diffbotUri</code> will be returned.</td>
</tr>
<tr>
    <td>Process Attempted</td>
    <td>Indicates if the page was sent to a Diffbot API for processing.</td>
</tr>
<tr>
    <td>Process Response</td>
    <td>Indicates whether or not the Diffbot processing was successful.</td>
</tr>
</tbody></table>

## Video Tutorials

### Crawlbot: Basics

  <iframe src="https://www.youtube.com/embed/qH9VYKxU1NI?rel=0&amp;showinfo=0&amp;modestbranding=1&amp;theme=light" frameborder="0" allowfullscreen=""></iframe>
  
A quick overview of Crawlbot using the [Analyze API](#analyze-api) to automatically identify and extract products from an e-commerce site.

### Crawlbot: Advanced Tutorial

  <iframe src="https://www.youtube.com/embed/c2gET-OugTM?rel=0&amp;showinfo=0&amp;modestbranding=1&amp;theme=light" frameborder="0" allowfullscreen=""></iframe>

This tutorial discusses some of the methods for narrowing your crawl within a site, and setting up a repeat or recurring crawl.

Related links:

* [Various Ways to Control Your Crawlbot Crawls for Web Data](http://blog.diffbot.com/various-ways-to-control-your-crawlbot-crawls-for-web-data/)
* [Crawlbot Support](http://support.diffbot.com/topics/crawlbot/)


