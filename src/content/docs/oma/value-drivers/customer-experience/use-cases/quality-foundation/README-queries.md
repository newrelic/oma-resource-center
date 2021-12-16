# Quality Foundation Queries
This README is a sub-section of [README.md](README.md).  

## Queries
| Purpose | Query |
| -------  | ---- |
| Overall volume | SELECT count(*) FROM PageView <br/>SINCE 1 WEEK AGO COMPARE WITH 1 WEEK AGO <br/>WHERE *LOB_PAGEVIEW_FILTER* |
| Volume by device type | SELECT count(*) FROM PageView <br/>WHERE *LOB_PAGEVIEW_FILTER* <br/>FACET deviceType SINCE 1 WEEK AGO |
| Volume by region | SELECT count(*) FROM PageView <br/>WHERE *LOB_PAGEVIEW_FILTER* <br/>FACET countryCode SINCE 1 WEEK AGO |
| Synthetics - Pre-login| FROM SyntheticCheck SELECT percentage(count(*),WHERE result = 'FAILED') <br/>WHERE monitorName = *LOB1_SYNTH1_MONITOR* |
| Synthetics - Post-login| FROM SyntheticCheck select percentage(count(*),WHERE result = 'FAILED') <br/>WHERE monitorName = #LOB1_SYNTH2_MONITOR* |
| Time to first byte - 75th percentile| FROM PageView SELECT percentile(backendDuration, 75) AS 'TTFB' <br/>WHERE *LOB_PAGEVIEW_FILTER* <br/>SINCE 1 WEEK AGO
| Cumulative layout shift - 75th percentile| FROM PageViewTiming SELECT percentile(cumulativeLayoutShift, 75) <br/>SINCE 1 WEEK AGO  <br/>WHERE *LOB_PAGEVIEW_FILTER* |
| Time to first byte - 75th percentile| FROM PageViewTiming SELECT percentile(largestContentfulPaint, 75) <br/>SINCE 1 WEEK AGO <br/>WHERE *LOB_PAGEVIEW_FILTER* |
| First input delay - 75th percentile| FROM PageViewTiming SELECT percentile(firstInputDelay, 75) <br/>SINCE 1 WEEK AGO <br/>WHERE *LOB_PAGEVIEW_FILTER* |
| Ajax response times - 75th percentile|  FROM AjaxRequest SELECT percentile(timeToSettle, 75) AS 'Time to Settle' <br/>WHERE *LOB_AJAX_FILTER* SINCE 1 WEEK AGO |
| 4xx and 5xx response codes| FROM AjaxRequest SELECT percentage(count(*), WHERE httpResponseCode >= 400) <br/>WHERE *LOB_AJAX_FILTER* SINCE 1 WEEK AGO |
| Javascript error rate| SELECT count(errorClass)/count(backendDuration) AS 'Javascript Errors/PageView' FROM JavaScriptError, PageView <br/>SINCE 1 WEEK AGO <br/>WHERE *LOB_PAGEVIEW_FILTER* |
 