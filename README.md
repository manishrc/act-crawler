# Act Crawler

[Apify **act**](https://www.apify.com/docs/actor) compatible with [Apify **crawler**](https://www.apify.com/docs/crawler) - same input  ⟹ same output.

**WARNING:** this is early version and may contain some bugs and may not be fully compatible.

## Usage

There are two ways how to use this act:

* pass crawler configuration as input of this act. Int his case the input looks like: 

  ```json
  {
    "startUrls": [{ "key": "", "value": "https://news.ycombinator.com" }],
    "maxParallelRequests": 10,
    "pageFunction": "function() { return context.jQuery('title').text(); }",
    "clickableElementsSelector": "a"
  }
  ```

* pass **ID** of own **crawler** and act fetches the configuration from that crawler. You can override any attribute you want in the act input: 

  ```json
  {
    "crawlerId": "snoftq230dkcxm7w0",
    "clickableElementsSelector": "a"
  }
  ```

  ​

## Input attributes

Act supports following crawler configuration attributes (for documentation see https://www.apify.com/docs/crawler#home):

| Attribute                 | Type                             | Default | Required | Description                              |
| ------------------------- | -------------------------------- | ------- | -------- | ---------------------------------------- |
| startUrls                 | `[{key: String, value: String}]` | `[]`    | yes      |                                          |
| pseudoUrls                | `[{key: String, value: String}]` |         |          |                                          |
| clickableElementsSelector | `String`                         |         |          | Currently supports only links (`a` elements) |
| pageFunction              | `Function`                       |         | yes      |                                          |
| interceptRequest          | `Function`                       |         |          |                                          |
| injectJQuery              | `Boolean`                        |         |          |                                          |
| injectUnderscore          | `Boolean`                        |         |          |                                          |
| maxPageRetryCount         | `Number`                         | `3`     |          |                                          |
| maxParallelRequests       | `Number`                         | `1`     |          |                                          |
| maxCrawledPagesPerSlave   | `Number`                         | `50`    |          |                                          |
| pageLoadTimeout           | `Number`                         | `30s`   |          |                                          |
| customData                | `Any`                            |         |          |                                          |
| maxCrawledPages           | `Number`                         |         |          |                                          |
| maxOutputPages            | `Number`                         |         |          |                                          |
| considerUrlFragment       | `Boolean`                        | `false` |          |                                          |



Additionally it adds also:

| Attribute            | Type     | Default | Required | Description                              |
| -------------------- | -------- | ------- | -------- | ---------------------------------------- |
| maxPagesPerFile      | `Number` | `1000`  | yes      | Number of outputed pages saved into 1 results file. |
| browserInstanceCount | `Number` | `10`    | yes      | Number of browser instances to be used in the pool. |
| crawlerId            | `String` |         |          | ID of a crawler to fetch configuration from. |
| urlList              | `String` |         |          | Url of the file containing urls to be enqueued as `startUrls`. This file must either contain one url per line or `urlListRegExp` configuration attribute must be provided. |
| urlListRegExp        | `String` |         |          | RegExp to match array of urls from `urlList` file ^.<br /><br />This RegExp is used this way against the file and must return array of url strings: `contentOfFile.match(new RegExp(urlListRegExp, 'g'));`<br /><br />For example `(http|https)://[\\w-]+(\\.[\\w-]+)+([\\w-.,@?^=%&:/~+#-]*[\\w@?^=%&;/~+#-])?` to simply match any http/https urls. |


