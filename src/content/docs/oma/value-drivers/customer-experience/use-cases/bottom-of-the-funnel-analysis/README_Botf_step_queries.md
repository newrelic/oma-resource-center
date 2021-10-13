# Bottom of the funnel steps queries

Edit, remove, or add data for each step in the bottom of the funnel

As stated in the bottom of the funnel [implementation guide](https://docs.newrelic.com/docs/new-relic-solutions/observability-maturity/customer-experience/bofta-implementation-guide/#distinguish-between-pages-and-actions) the bottom of the funnel is likely to be a mix of full page loads and Ajax requests.  The dashboard json shows an example of a flow that starts with a page load followed by an ajax request followed by a page load. 

For each step, edit the tile that calls out the step in the user journey.  This will help others understand and you remember which thing the user is doing.   Edit the title to match the user step rather than the page name or ajax request name.  

### Page performance tiles

The page performance tiles capture:<br>
first paint - time from user request to beginning of page render<br>
lcp - largest contentful paint - part of core web vitals. The time from beginning of page render to the largest contentful paint<br>
cls - cumulative layout shift - part of core web vitals.  A score indicating how much the layout shift changes during render<br>
fid - first input delay - part of core web vitals.  Recorded only when a user attempts to interact during render.  The time between user attempt and page response. <br>

To create a page performance row, edit the existing dashboard or add a new row.  The STEP.._FILTER value is there as a placeholder for the page filter.  This value is usually something like pageUrl LIKE %value%

### AJAX performance tiles

__Average Response Time__<br>
* Uses Ajax metrics to measure average response times.  To find the correct entity guid and the metric name, use Data Explorer.  
* Select metrics
* Select the browser app associated with the Ajax call.  If the browser is instrumented via auto-injection, make sure you are using the browser app and not the apm app name. 
* Click on the _See timeslice metrics_ link
* Filter to Ajax.  Choose the Ajax response time. 
* Clicking on the Ajax metric will reveal the entity guid. 

__Success % Query__<br>
* Uses AjaxRequest
* STEP2_AJAX_REQUEST_FILTER - Typically set to filter by web app name and the pageUrl that the AjaxRequest is invoked from





 