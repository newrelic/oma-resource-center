  
# Customer Experience 

## Segment Whitelist Dashboard Instructions
![Segment Whitelist Dashboard example](images/segment_whitelist_investigation.png?raw=true "Cx Whitelist Investigation")

Importing this dashboard is an optional step in Quality Foundation.  Use the Quality Foundation implementation guide to understand whether or not you need to add additional segments to your browser configuration. 

To use the dashboard:
1. Download segment_whitelist_investigation.json
2. Change **ACCOUNT_ID** to the account that holds your browser data.  If you have multiple accounts with browser data you will need to follow this process for each account. 
3. Import the JSON as a new Dashboard via the main Dashboards menu. ![Dashboard import](../images/ImportDashboard.png?raw=true "Dashboard import")

## Quality Foundation Dashboard Instructions

![Quality Foundation Dashboard example](images/CustomerExperience_QualityFoundation.png?raw=true "Cx Quality Foundation")

The Customer Experience dashboard measures the customer experience for each line of business (LOB) or global function (login, search) in different pages. This approach aligns customer experience with business intiatives. 

1. Decide which global functions, lines of business you need to measure for and plan dashboard pages for each.  Lines of business usually match or encapsulate different products and services offered to end users.
The dashboard JSON includes two pages.  If your dashboard needs to have more than two pages, copy and paste the first page section for each additional page you need.
You can add or remove tabs after importing the dashboard.   Import the dashboard before adding or removing widgets to make layout design easier.

2. Download quality-foundation.json.  Follow the instructions in the [query readme file](README-queries.md) to edit the fie.  When you are done, copy the contents into your clipboard and import the dashboard. 

## Quality Foundation KPI Measurement Instructions

![Quality Foundation KPI example](images/CustomerExperience_QualityFoundation_KPIs.png?raw=true "Cx Quality Foundation KPIs")

The CustomerExperience_QualityFoundation_KPI document provides a way to measure baselines and track progress while improving KPI performance.

1. Start with the format that works best for you, .ods, or .xls
2. Capture the current baseline for all your lines of business pages without further filtering.  Identify what needs improving and to what extent by highlighting it in yellow or red.  Highlight the rest in green.
3. Use other filters, as applicable, to identify other KPIs that need improving.  Capture only those that you plan to actively work on or measure.   Examples include KPIs filtered to mobile users where improvement is needed and impactful to the business.
4. Update KPI numbers weekly or after each sprint.  
5. Be aware of how long data is retained.  The KPI spreadsheet needs to be updated before retention of relevant data expires.
 
