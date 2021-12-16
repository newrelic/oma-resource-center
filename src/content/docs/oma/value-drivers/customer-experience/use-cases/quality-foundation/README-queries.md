# Quality Foundation Queries
This README is a sub-section of [README.md](README.md).  

# Dashboard edit instructions

Find and replace the text below.  This example has only two tabs.  You can add more as needed. 
**Page 1 Section**

| Text | Value |
| ----- | ----- |
| **ACCOUNT_ID1** | Account Id of the accounts you are querying from.  In most cases all the queries on a page will come from the same account id.  If this is not true for you, you can change the value of the account id per widget. |
|**LOB1_SYNTH1_MONITOR** | Name of the ping synthetic monitor (as it appears in New Relic) that checks the site is available for anynomous and authenticated users|
|**LOB1_SYNTH2_MONITOR** |  Name of the scripted Synthetic monitor (as it appears in New Relic) that checks the site is available for authenticated users (post login)</tr>
|**LOB1_PAGEVIEW_FILTER** | NRQL WHERE clause that filters PageView and PageViewTiming results to specific apps and/or page URLs e.g. appName = 'Travel.PROD' AND pageUrl LIKE '%hotel%' </tr>
|**LOB1_AJAX_FILTER** | WHERE clause that filters PageView and AjaxResult to specific apps and/or page URLs.  Often the same value as LOB1_PAGEVIEW_FILTER 
|**LOB1** |Name of the first LOB, product, or shared function.|

**Page 2 Section** <br>
The attributes below have the same definitions as above, but with values that match the second line of business/product/global feature that you are measuring. 

| Text | 
| ----- | 
| **ACCOUNT_ID2** |
| **LOB2_SYNTH1_MONITOR** |
| **LOB2_SYNTH2_MONITOR** |
| **LOB2_PAGEVIEW_FILTER** |
| **LOB2_AJAX_FILTER** |
| **LOB2** |

 3. Import the JSON as a new Dashboard via the main Dashboards menu.
![Dashboard import](../images/ImportDashboard.png?raw=true "Dashboard import")

 4. Review results.  Add/remove dashboard widgets as needed
 5. Done


## Reference - Queries

This section lists each of the queries on each page.  They are broken out into sections to help people new to [NRQL](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/introduction-nrql-new-relics-query-language/) see the different components. 

| Purpose | Select | From | Where | Since/Facet/Compare with |
| -------  | ---- | ---- | ----| ---- |
| Overall volume | SELECT count(*) | FROM [PageView](https://docs.newrelic.com/attribute-dictionary/?dataSource=Browser+agent&event=PageView) | WHERE *LOB_PAGEVIEW_FILTER* | SINCE 1 WEEK AGO COMPARE WITH 1 WEEK AGO|
| Volume by device type | SELECT count(*) | FROM [PageView](https://docs.newrelic.com/attribute-dictionary/?dataSource=Browser+agent&event=PageView)  | WHERE *LOB_PAGEVIEW_FILTER* |FACET deviceType SINCE 1 WEEK AGO |
| Volume by region | SELECT count(*) | FROM [PageView](https://docs.newrelic.com/attribute-dictionary/?dataSource=Browser+agent&event=PageView)  |WHERE *LOB_PAGEVIEW_FILTER* |FACET countryCode SINCE 1 WEEK AGO |
| Synthetics - Pre-login| SELECT [percentage](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/nrql-syntax-clauses-functions/#func-percentage)(count(*),WHERE result = 'FAILED') |FROM [SyntheticCheck](https://docs.newrelic.com/attribute-dictionary/?dataSource=Synthetics&event=SyntheticCheck) | WHERE monitorName = *LOB1_SYNTH1_MONITOR* |SINCE 1 WEEK AGO
| Synthetics - Post-login| SELECT [percentage](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/nrql-syntax-clauses-functions/#func-percentage)(count(*),WHERE result = 'FAILED')| FROM [SyntheticCheck](https://docs.newrelic.com/attribute-dictionary/?dataSource=Synthetics&event=SyntheticCheck) | WHERE monitorName = *LOB1_SYNTH2_MONITOR* |SINCE 1 WEEK AGO
| Time to first byte - 75th percentile | SELECT [percentile](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/nrql-syntax-clauses-functions/#func-percentile)(backendDuration, 75) AS 'TTFB'|FROM [PageView](https://docs.newrelic.com/attribute-dictionary/?dataSource=Browser+agent&event=PageView)  |WHERE *LOB_PAGEVIEW_FILTER* |SINCE 1 WEEK AGO
| Cumulative layout shift - 75th percentile| SELECT [percentile](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/nrql-syntax-clauses-functions/#func-percentile)(cumulativeLayoutShift, 75) |FROM [PageViewTiming](https://docs.newrelic.com/attribute-dictionary/?dataSource=Browser+agent&event=PageViewTiming) | WHERE *LOB_PAGEVIEW_FILTER*|SINCE 1 WEEK AGO |
| Largest contentful paint - 75th percentile| SELECT [percentile](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/nrql-syntax-clauses-functions/#func-percentile)(largestContentfulPaint, 75)|FROM [PageViewTiming](https://docs.newrelic.com/attribute-dictionary/?dataSource=Browser+agent&event=PageViewTiming) |WHERE *LOB_PAGEVIEW_FILTER* |SINCE 1 WEEK AGO |
| First input delay - 75th percentile| SELECT [percentile](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/nrql-syntax-clauses-functions/#func-percentile)(firstInputDelay, 75)|FROM [PageViewTiming](https://docs.newrelic.com/attribute-dictionary/?dataSource=Browser+agent&event=PageViewTiming) |WHERE *LOB_PAGEVIEW_FILTER*|SINCE 1 WEEK AGO <br/> |
| Ajax response times - 75th percentile| SELECT [percentile](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/nrql-syntax-clauses-functions/#func-percentile)(timeToSettle, 75) AS 'Time to Settle'|FROM [AjaxRequest](https://docs.newrelic.com/attribute-dictionary/?dataSource=Browser+agent&event=AjaxRequest)  |WHERE *LOB_AJAX_FILTER* |SINCE 1 WEEK AGO |
| 4xx and 5xx response codes| SELECT [percentage](https://docs.newrelic.com/docs/query-your-data/nrql-new-relic-query-language/get-started/nrql-syntax-clauses-functions/#func-percentage)(count(*), WHERE httpResponseCode >= 400) |FROM [AjaxRequest](https://docs.newrelic.com/attribute-dictionary/?dataSource=Browser+agent&event=AjaxRequest) |WHERE *LOB_AJAX_FILTER* |SINCE 1 WEEK AGO |
| Javascript error rate| SELECT count(errorClass)/count(backendDuration) AS 'Javascript Errors/PageView'| FROM [JavaScriptError](https://docs.newrelic.com/attribute-dictionary/?dataSource=Browser+agent&event=JavaScriptError), PageView |WHERE *LOB_PAGEVIEW_FILTER*|SINCE 1 WEEK AGO  |

## Riffs
* If there is noticeable different between web and mobile web performance, you can show it separately in the same dashboard by breaking out each line of charts into alternating rows.  In the even rows, add the following to the WHERE clause: AND deviceType = 'Desktop'.  In odd rows, add the following to the WHERE clause: AND deviceType != 'Desktop'.  Make sure to update widget titles accordingly. 


 