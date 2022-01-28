# Quality Foundation Queries
This README is a sub-section of [README.md](README.md).  

# Dashboard edit instructions
The Quality Foundation dashboard has a main page that displays user centric KPIs at the summary level for a single web application or multiple.  If you are new to dashboarding, it's helpful to test updating query filters and importing the dashboard prior to adding pages for different lines of business or functions.

## Edit [quality-foundation-main.json](quality-foundation-main.json) [#edit-main]
Find and replace the text below.  
| Text | Value |
| ----- | ----- |
| **ACCOUNT_ID1** | Account Id of the accounts you are querying from.  In most cases all the queries on a page will come from the same account id.  If this is not true for you, you can change the value of the account id per widget. |
|**MAIN_SYNTH1_MONITOR** | Name of the ping synthetic monitor (as it appears in New Relic) that checks the site is available for anynomous and authenticated users|
|**MAIN_SYNTH2_MONITOR** |  Name of the scripted Synthetic monitor (as it appears in New Relic) that checks the site is available for authenticated users (post login)|
|**MAIN_PAGEVIEW_FILTER** | NRQL WHERE clause that filters PageView and PageViewTiming results to specific apps and/or page URLs e.g. appName = 'Travel.PROD' AND pageUrl LIKE '%hotel%'|
|**MAIN_AJAX_FILTER** | WHERE clause that filters PageView and AjaxResult to specific apps and/or page URLs.  Often the same value as LOB1_PAGEVIEW_FILTER|

If you are new to dashboarding, you can skip to importing the dashboard to check progress and understanding before starting on the line of business pages. 

## Download and edit [quality-foundation-lob1.json](quality-foundation-lob1.json) for each line of business [#edit-lob]

| Text | Value |
| ----- | ----- |
| **ACCOUNT_ID1** | Account Id of the accounts you are querying from.  In most cases all the queries on a page will come from the same account id.  If this is not true for you, you can change the value of the account id per widget. |
|**LOB1_SYNTH1_MONITOR** | Name of the ping synthetic monitor (as it appears in New Relic) that checks the site is available for anynomous and authenticated users|
|**LOB1_SYNTH2_MONITOR** |  Name of the scripted Synthetic monitor (as it appears in New Relic) that checks the site is available for authenticated users (post login) |
|**LOB1_PAGEVIEW_FILTER** | NRQL WHERE clause that filters PageView and PageViewTiming results to specific apps and/or page URLs e.g. appName = 'Travel.PROD' AND pageUrl LIKE '%hotel%' | 
|**LOB1_AJAX_FILTER** | WHERE clause that filters PageView and AjaxResult to specific apps and/or page URLs.  Often the same value as LOB1_PAGEVIEW_FILTER | 
|**LOB1** |Name of the first LOB, product, or shared function.|

## Add the first line of business json by copying the json into [quality-foundation-main.json](quality-foundation-main.json) after **line 790**.  Make sure to put a comma after the **}** before pasting in your json.  Subsequent pages will be need to be comma seperated.

## Import the JSON as a new Dashboard via the main Dashboards menu. [#import-json]
![Dashboard import](../images/ImportDashboard.png?raw=true "Dashboard import")
It can be helpful to test as you go.  For example, you can start by importing the main dashboard, deleting it after a successful attempt, and then importing again with at least one line of business page.  Once the dashboard is imported you can edit it to your liking.  This includes editing queries, changing layouts, and adding new pages.

## Review results.  Add/remove dashboard widgets as needed [#review-import]

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


 
