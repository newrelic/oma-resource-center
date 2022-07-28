# Bottom of the funnel steps queries
This README is a sub-section of [README.md](README.md).  

As stated in the bottom of the funnel [implementation guide](https://docs.newrelic.com/docs/new-relic-solutions/observability-maturity/customer-experience/bofta-implementation-guide/#distinguish-between-pages-and-actions) the bottom of the funnel is likely to be a mix of full page loads and Ajax requests.  The dashboard json shows an example of a flow that starts with a page load followed by an ajax request followed by a page load. 

For each step in the bottom of the funnel, make a copy of either [botf_ajax.json](botf_ajax.json) or [botf_pageview.json](botf_pageview.json)

Edit the tile that calls out the step in the user journey.  This will help others understand and you remember which thing the user is doing.   Edit the title to match the user step rather than the page name or ajax request name.  

### Page performance tiles

The page performance tiles capture:<br>
first paint - time from user request to beginning of page render<br>
lcp - largest contentful paint - part of core web vitals. The time from beginning of page render to the largest contentful paint<br>
cls - cumulative layout shift - part of core web vitals.  A score indicating how much the layout shift changes during render<br>
fid - first input delay - part of core web vitals.  Recorded only when a user attempts to interact during render.  The time between user attempt and page response. <br>

To create a page performance row, edit the existing dashboard or add a new row.  The STEP.._FILTER value is there as a placeholder for the page filter.  This value is usually something like pageUrl LIKE %value%

### AJAX performance tiles

__95th Percentile Response Time__<br>
* Uses AjaxRequest
* AJAX_REQUEST_FILTER - Typically set to filter by web app name and (the pageUrl that the AjaxRequest is invoked from and/or the requestUrl/Ajax destination)
* 95th percentile shows you the maximum time experienced by 95% of your users.  While Core Web Vitals focuses on the 75th percentile, Bottom of the funnel analysis is about taking an aggressive approach to what happens at the end of the funnel.  Thus, it's important to know what the performance is for almost all visitors. The reason the default is not 99% or 100% is that time spent reducing latency for the poorest 5% typically show low returns on investment.  

FROM AjaxRequest SELECT 2 AS TargetMaximumResponseTime, percentile(timeToSettle, 95) WHERE AJAX_REQUEST_FILTER SINCE 1 WEEK AGO TIMESERIES AUTO

Translates to: Show me the timeToSettle for the 95th percentile over the last week.  Set 2.0 seconds as the target maximum time and create a line so I can see times where timeToSettle exceeded it.


__Success % Query__<br>
* Uses AjaxRequest
* AJAX_REQUEST_FILTER - Typically set to filter by web app name and (the pageUrl that the AjaxRequest is invoked from and/or the requestUrl/Ajax destination)

FROM AjaxRequest SELECT 0.98 AS TargetMinumumSuccessRate,percentage(count(\*), WHERE httpResponseCode >= 200 AND httpResponseCode <300) AS 'Successful' WHERE httpResponseCode >= 200 AND AJAX_REQUEST_FILTER SINCE 1 WEEK AGO TIMESERIES AUTO

Translates to: Show me what percentage of calls to the backend came back as successful over the last week.  Set 98% to the target success rate and create a line so I can see times where the target was not met. 







 