  
# Customer Experience 

## Quality Foundation Dashboard Instructions

The Customer Experience dashboard measures the customer experience for each line of business (LOB) or global function (login, search) in different pages. This approach aligns customer experience with business intiatives. 

*To use this dashboard*
1. Decide which global functions, lines of business you need to measure for and plan dashboard pages for each.  Lines of business usually match or encapsulate different products and services offered to end users.
The dashboard JSON includes two pages.  If your dashboard needs to have more than two pages, copy and paste the first page section for each additional page you need.
You can add or remove tabs after importing the dashboard.   Import the dashboard before adding or removing widgets to make layout design easier.

2. Find and replace the text below 


&nbsp;&nbsp;&nbsp;&nbsp;Page 1 Section
&nbsp;&nbsp;&nbsp;&nbsp;*ACCOUNT_ID1* Account Id of the accounts you are querying from.  In most cases all the queries on a page will come from the same account id.  If this is not true for you, you can change the value of the account id per widget. 
&nbsp;&nbsp;&nbsp;&nbsp;*LOB1* Name of the first LOB, product, or shared function.  
&nbsp;&nbsp;&nbsp;&nbsp;*LOB1_SYNTH1_MONITOR*  Name of the ping synthetic monitor (as it appears in New Relic) that checks the site is available for anynomous and authenticated users
&nbsp;&nbsp;&nbsp;&nbsp;*LOB1_SYNTH2_MONITOR*  Name of the scripted Synthetic monitor (as it appears in New Relic) that checks the site is available for authenticated users (post login)
&nbsp;&nbsp;&nbsp;&nbsp;*LOB1_PAGEVIEW_FILTER* NRQL WHERE clause that filters PageView and PageViewTiming results to specific apps and/or page URLs e.g. appName = 'Travel.PROD' AND pageUrl LIKE '%hotel%'
&nbsp;&nbsp;&nbsp;&nbsp;*LOB1_AJAX_FILTER* WHERE clause that filters PageView and AjaxResult to specific apps and/or page URLs.  Often the same value as LOB1_PAGEVIEW_FILTER


&nbsp;&nbsp;&nbsp;&nbsp;Page 2 Section 
&nbsp;&nbsp;&nbsp;&nbsp;The attributes below have the same definitions as above, but with values that match the second line of business/product/global feature that you are measuring.
&nbsp;&nbsp;&nbsp;&nbsp;*ACCOUNT_ID2* 
&nbsp;&nbsp;&nbsp;&nbsp;*LOB2_SYNTH1_MONITOR* 
&nbsp;&nbsp;&nbsp;&nbsp;*LOB2_SYNTH2_MONITOR* 
&nbsp;&nbsp;&nbsp;&nbsp;*LOB2_PAGEVIEW_FILTER*
&nbsp;&nbsp;&nbsp;&nbsp;*LOB2_AJAX_FILTER*

 3. Import the JSON 
 4. Review results.  Add/remove dashboard widgets as needed
 5. Done
 