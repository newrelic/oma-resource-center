  
# Customer Experience 

## Quality Foundation Dashboard Instructions

![Quality Foundation Dashboard example](images/CustomerExperience_QualityFoundation.png?raw=true "Cx Quality Foundation")

The Customer Experience dashboard measures the customer experience for each line of business (LOB) or global function (login, search) in different pages. This approach aligns customer experience with business intiatives. 

1. Decide which global functions, lines of business you need to measure for and plan dashboard pages for each.  Lines of business usually match or encapsulate different products and services offered to end users.
The dashboard JSON includes two pages.  If your dashboard needs to have more than two pages, copy and paste the first page section for each additional page you need.
You can add or remove tabs after importing the dashboard.   Import the dashboard before adding or removing widgets to make layout design easier.

2. Find and replace the text below 

**Page 1 Section**

| Text | Value |
| ----- | ----- |
| **ACCOUNT_ID1** | Account Id of the accounts you are querying from.  In most cases all the queries on a page will come from the same account id.  If this is not true for you, you can change the value of the account id per widget. |
|**LOB1** |Name of the first LOB, product, or shared function.|
|**LOB1_SYNTH1_MONITOR** | Name of the ping synthetic monitor (as it appears in New Relic) that checks the site is available for anynomous and authenticated users|
|**LOB1_SYNTH2_MONITOR** |  Name of the scripted Synthetic monitor (as it appears in New Relic) that checks the site is available for authenticated users (post login)</tr>
|**LOB1_PAGEVIEW_FILTER** | NRQL WHERE clause that filters PageView and PageViewTiming results to specific apps and/or page URLs e.g. appName = 'Travel.PROD' AND pageUrl LIKE '%hotel%' </tr>
|**LOB1_AJAX_FILTER** | WHERE clause that filters PageView and AjaxResult to specific apps and/or page URLs.  Often the same value as LOB1_PAGEVIEW_FILTER 



**Page 2 Section** <br>
The attributes below have the same definitions as above, but with values that match the second line of business/product/global feature that you are measuring. 

| Text | 
| ----- | 
| **ACCOUNT_ID2** |
| **LOB2** |
| **LOB2_SYNTH1_MONITOR** |
| **LOB2_SYNTH2_MONITOR** |
| **LOB2_PAGEVIEW_FILTER** |
| **LOB2_AJAX_FILTER** |

 3. Import the JSON as a new Dashboard via the main Dashboards menu.
![Dashboard import](images/ImportDashboard.png?raw=true "Dashboard import")

 4. Review results.  Add/remove dashboard widgets as needed
 5. Done

## Quality Foundation KPI Measurement Instructions

![Quality Foundation KPI example](images/CustomerExperience_QualityFoundation_KPIs.png?raw=true "Cx Quality Foundation KPIs")

The CustomerExperience_QualityFoundation_KPI document provides a way to measure baselines and track progress while improving KPI performance.

1. Start with the format that works best for you, .ods, or .xls
2. Capture the current baseline for all your lines of business pages without further filtering.  Identify what needs improving and to what extent by highlighting it in yellow or red.  Highlight the rest in green.
3. Use other filters, as applicable, to identify other KPIs that need improving.  Capture only those that you plan to actively work on or measure.   Examples include KPIs filtered to mobile users where improvement is needed and impactful to the business.
4. Update KPI numbers weekly or after each sprint.  
5. Be aware of how long data is retained.  The KPI spreadsheet needs to be updated before retention of relevant data expires.
 