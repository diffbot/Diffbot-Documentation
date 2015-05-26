## Bulk API

### Creating a Bulk Job

To create a bulk job, make a POST request to `http://api.diffbot.com/v3/bulk`.

Set your `Content-Type` header to `application/x-www-form-urlencoded` (not `multipart/form-data`). Your POST body content should provide the following:

<table border="0" cellpadding="5" class="controls table table-bordered">
  <thead>
    <tr>
      <th>Argument</th>

      <th>Description</th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>token</td>

      <td>
        Developer <a href="/pricing">token</a>
      </td>
    </tr>

    <tr>
      <td>name</td>

      <td>Job name. This should be a unique identifier and will be used to modify your bulk job and retrieve its output.</td>
    </tr>

    <tr>
      <td>urls</td>

      <td>Space-delimited list of URLs to process.</td>
    </tr>

    <tr>
      <td>apiUrl</td>

      <td>The full Diffbot API to be used for each URL. For instance, to process each URL via the article API, supply <code>http://api.diffbot.com/v3/article</code>. You may also include API parameters, e.g. <code>http://api.diffbot.com/v3/article?fields=meta,tags</code>.</td>
    </tr>

    <tr>
      <td colspan="2"><strong>Optional Arguments</strong></td>
    </tr>

    <tr>
      <td>notifyEmail</td>

      <td>Send a message to this email address when the bulk job completes.</td>
    </tr>

    <tr>
      <td>notifyWebhook</td>

      <td>
        Pass a URL to be notified when the bulk job completes. You will receive a POST with the full <a href="#response">JSON response</a> in the POST body.
      </td>
    </tr>

    <tr>
      <td>repeat</td>

      <td>Specify the number of days as a floating-point (e.g. <code>repeat=7.0</code>) to repeat this job. By default bulk jobs will not be repeated.</td>
    </tr>

    <tr>
      <td>maxRounds</td>

      <td>Specify the maximum number of repeats. Use <code>maxRounds=-1</code> to continually repeat.</td>
    </tr>

    <tr>
      <td>pageProcessPattern</td>

      <td>Enter ||-separated strings to limit pages processed to those whose HTML contains <em>any</em> of the content strings. If a page does not contain at least one of the strings, it will be ignored.</td>
    </tr>
  </tbody>
</table>


#### Response
> If successful, you'll receive this response:

```json
 "response": "Successfully added urls for spidering."
```

Upon adding a new bulk job, you will receive a success message in the JSON response, in addition to full job details.



### Pausing, Deleting or Restarting Bulk Jobs

You can manage your crawls by making GET requests to the same endpoint, `http://api.diffbot.com/v3/bulk`.

Provide the following data:

<table class="controls table table-bordered" border="0" cellpadding="5">
  <thead><tr><th>Parameter</th><th>Description</th></tr></thead>
  <tbody>
  <tr><td>token</td><td>Developer <a href="/pricing">token</a></td></tr>
  <tr>
  <td>name</td>
  <td>Job name as defined when the bulk was created.</td>
  </tr>
  <tr>
  <td>pause</td>
  <td>Pass <code>pause=1</code> to pause a bulk job. Pass <code>pause=0</code> to resume a paused job.</td>
  </tr>
  <tr>
  <td>restart</td>
  <td>Pass <code>restart=1</code> to restart a bulk job. **This will erase all processed data and re-process all of the submitted URLs.**</td>
  </tr>
  <tr>
  <td>delete</td>
  <td>Pass <code>delete=1</code> to delete a job, and all associated data, completely.</td>
  </tr>
</tbody></table>

### Retrieving Bulk API Data

To download results please make a GET request to the following URLs, replacing `token` and `jobName` with your token and bulk job name, respectively. The JSON data and URLs report URLs are also available in the Bulk API JSON response, as `downloadJson` and `downloadUrls`.

<table class="controls table table-bordered" border="0" cellpadding="5">
  <thead><tr><th>URL</th><th>Description</th></tr></thead>
  <tbody>
  <tr><td style="word-wrap: break-word;">http://api.diffbot.com/v3/bulk/download/token-jobName_data.json</td><td>Download all JSON objects (as processed by Diffbot APIs).</td></tr>
  <tr><td>http://api.diffbot.com/v3/bulk/download/token-jobName_data.csv</td><td>Download a subset of content -- top-level fields only -- as a comma-separated values (CSV) file.</td></tr>
  <tr><td colspan="2"><strong>For diagnostic data:</strong></td></tr>
  <tr><td>http://api.diffbot.com/v3/bulk/download/token-jobName_urls.csv</td><td>Download the "URLs report" CSV file. This lists all URLs attempted by the Bulk API, and the most recent status for each. Useful for debugging.</td></tr>
   </tbody>
  </table>

### Using the Search API to Retrieve Bulk Job Data

You can also use Diffbot's [Search API](#search-api) to fine-tune the data retrieved from one (or multiple) Crawlbot or Bulk API jobs.

[Search API documentation](#search-api)

### Viewing Bulk Job Details

Your active bulk jobs (and any active Crawlbot API crawls) will be returned in the `jobs` object in a request made to `http://api.diffbot.com/v3/bulk`.

To retrieve a single job's details, provide the job's `name` in your request:

<table class="controls table table-bordered" border="0" cellpadding="5">
  <thead><tr><th>Parameter</th><th>Description</th></tr></thead>
  <tbody>
  <tr><td>token</td><td>Developer <a href="/pricing">token</a></td></tr>
  <tr><td>name</td><td>Name of bulk job (or crawl) to retrieve.</td></tr>
   </tbody>
  </table>

To view all crawls, simply omit the `name` parameter.

### Bulk Job Response
> Sample response from a single crawl:

```json
 {
  "jobs": [
    {
      "name": "bulkJob",
      "type": "bulk",
      "jobCreationTimeUTC": 1426872272,
      "jobCompletionTimeUTC": 1426872504,
      "jobStatus": {
        "status": 9,
        "message": "Job has completed and no repeat is scheduled."
      },
      "sentJobDoneNotification": 1,
      "objectsFound": 100,
      "urlsHarvested": 200,
      "pageCrawlAttempts": 100,
      "pageCrawlSuccesses": 100,
      "pageCrawlSuccessesThisRound": 100,
      "pageProcessAttempts": 100,
      "pageProcessSuccesses": 100,
      "pageProcessSuccessesThisRound": 100,
      "maxRounds": 0,
      "repeat": 0.0,
      "crawlDelay": 0.25,
      "obeyRobots": 0,
      "roundsCompleted": 0,
      "roundStartTime": 0,
      "currentTime": 1432312440,
      "currentTimeUTC": 1432312440,
      "apiUrl": "http://api.diffbot.com/v3/analyze",
      "urlCrawlPattern": "",
      "urlProcessPattern": "",
      "pageProcessPattern": "",
      "urlCrawlRegEx": "",
      "urlProcessRegEx": "",
      "maxHops": -1,
      "downloadJson": "http://api.diffbot.com/v3/bulk/download/sampletoken-bulkJob_data.json",
      "downloadUrls": "http://api.diffbot.com/v3/bulk/download/sampletoken-bulkJob_urls.csv",
      "notifyEmail": "support@diffbot.com",
      "notifyWebhook": "http://www.diffbot.com"
    }
  ]
}
```

This will return a JSON response of your token's Bulk API jobs. 

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


## Bulk Processing URL Report

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