  
# Customer Experience 

## Quality Foundation Dashboard Instructions

![Quality Foundation Dashboard example](images/CustomerExperience_QualityFoundation.png?raw=true "Insights")

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

 3. Import the JSON 
 4. Review results.  Add/remove dashboard widgets as needed
 5. Done
 