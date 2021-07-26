  
# Customer Experience 

## Bottom of the Funnel Analysis Dashboard Instructions

![Bottom of the Funnel Analysis example](images/CustomerExperience_BotFunnelAnalysis.png?raw=true "Cx Bottom of the Funnel")

The Bottom of the Funnel Analysis dashboard measures the customer experience during the critical phase of the customer's journey, which starts when the user passes a threshold indicating intent to complete an action.  For example, when a user goes to a cart and initiates checkout. 
 
1. Follow the steps in <docs link> to determine steps in the user journey that you will measure

2. Download the ![dashboard json](botf.json). 

3. Edit botf.json and change ACCOUNT_ID to the account id that you will run most of the queries from.

4. Import the JSON as a new Dashboard via the main Dashboards menu.
![Dashboard import](../images/ImportDashboard.png?raw=true "Dashboard import")

5. Edit the imported dashboard 

## How to edit the Bottom of the Funnel Analysis Dashboard

The dashboard is organized into sections, delineated by pink lines.   At the top is the summary data.  This shows the bottom of the funnel conversion rate, synthetics checks results, and revenue at risk.   The summary data is followed by a row for each step in the user journey at the bottom of the funnel. 

### Edit the summary data
Edit the title tile to reflect the bottom of the funnel process shown in the dashboard.

#### Conversion Funnel 
Update the Funnel query for your bottom of the funnel process
The structure of the funnel query is as follows: <br>
>FROM DATA_TYPE <br>
  SELECT funnel(COMMON_ATTRIBUTE, WHERE .. ACTION_A, .., WHERE .. ACTION_N) <br>
  SINCE 1 WEEK AGO <br>

COMMON_ATTRIBUTE - usually set to session.  You can capture conversions that happen over multiple sessions, by adding ![custom attributes](https://docs.newrelic.com/docs/browser/new-relic-browser/browser-agent-spa-api/setcustomattribute-browser-agent-api/), like customerId, to your PageViews.  This is provided your user is not anonymous. 

WHERE … ACTION - filters for the PageViews relevant to that step in the user’s journey.  

__Examples__  <br>
The following tracks conversions on the basis that a user converts in a single browser session
>FROM PageView SELECT funnel(session_id, <br>
      WHERE appName = ‘CustomerPortal’ and pageUrl like ‘%Checkout%’ AS ‘Begin Checkout’, <br>
      WHERE appName = ‘CustomerPortal’ and pageUrl like ‘%OrderConfirmed%’ AS ‘Order Confirmed’)<br>

The following tracks conversions on the basis that a user is authenticated by the time they begin checkout
>FROM PageView SELECT funnel(customerId, <br>
      WHERE appName = ‘CustomerPortal’ and pageUrl like ‘%Checkout%’ AS ‘Begin Checkout’, <br>
      WHERE appName = ‘CustomerPortal’ and pageUrl like ‘%OrderConfirmed%’ AS ‘Order Confirmed’)<br>

As the funnel query pulls from a single data type, you won’t be able to include User Journey steps that are Ajax Requests.  You can still capture the overall conversion rate however, and capture Ajax request performance in the next sections of the dashboard.

#### Synthetics Check
Change BOTF_MONITOR_NAME to match the synthetics monitor that validates the bottom of the funnel.  This is covered in [!Doc Coming Soon}().

#### Revenue at Risk - Latency
REVENUE_AT_RISK_LATENCY_FILTER - You can filter both related pages and Ajax Requests using pageUrl.  The ![pageUrl value in an AjaxRequest](https://docs.newrelic.com/attribute-dictionary/?dataSource=Browser+agent&event=AjaxRequest&attributeSearch=pageUrl) reflects the page the user was on when they initiated the request.  

CONVERSION_VALUE - set this to what your organization considers the average value of a conversion.  Conversely, using custom attributes, you can change the query to be more specific and use the value of what the end user is about to purchase.   

For example, instead of <br>
>SELECT count(*) * 6.0 AS USD FROM PageView, AjaxRequest WHERE (pageUrl LIKE '%checkout%' or pageUrl LIKE '%confirmOrder%') AND (timeToSettle ..

You could use
>SELECT sum(cartValue) AS USD FROM PageView, AjaxRequest WHERE (pageUrl LIKE '%checkout%' or pageUrl LIKE '%confirmOrder%') AND (timeToSettle ..

provided that you have captured the cart value using ![setCustomAttribute}(https://docs.newrelic.com/docs/browser/new-relic-browser/browser-agent-spa-api/setcustomattribute-browser-agent-api/) or ![setAttribute](https://docs.newrelic.com/docs/browser/new-relic-browser/browser-agent-spa-api/setattribute-browser-spa-api/).

One thing to be aware of is that in this example, the same cart value could be added multiple times if the same user experiences multiple interactions with slowness or errors.

#### Revenue at Risk - Errors
REVENUE_AT_RISK_ERRORS_FILTER - This is likely to be the same as REVENUE_AT_RISK_LATENCY_FILTER

CONVERSION_VALUE - Revenue at Risk - Latency

### Edit, remove, or add data for each step in the bottom of the funnel

As stated in ![Docs link coming soon]() the bottom of the funnel is likely to be a mix of full page loads and Ajax requests.  The dashboard json shows an example of a flow that starts with a page load followed by an ajax request followed by a page load. 

For each step, edit the tile that calls out the step in the user journey.  This will help others understand and you remember which thing the user is doing.   Edit the title to match the user step rather than the page name or ajax request name.  

#### Page performance tiles

The page performance tiles capture:<br>
first paint - time from user request to beginning of page render<br>
lcp - largest contentful paint - part of core web vitals. The time from beginning of page render to the largest contentful paint<br>
cls - cumulative layout shift - part of core web vitals.  A score indicating how much the layout shift changes during render<br>
fid - first input delay - part of core web vitals.  Recorded only when a user attempts to interact during render.  The time between user attempt and page response. <br>

To create a page performance row, edit the existing dashboard or add a new row.  The STEP.._FILTER value is there as a placeholder for the page filter.  This value is usually something like pageUrl LIKE %value%

#### AJAX performance tiles

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


 




 