  
# Bottom of the funnel analysis dashboard

![Bottom of the Funnel Analysis example](images/CustomerExperience_BotFunnelAnalysis.png?raw=true "Cx Bottom of the Funnel")

The bottom of the funnel analysis dashboard measures the user experience during the critical phase of the user's journey, which starts when the user passes a threshold indicating intent to complete an action.  For example, when a user goes to a cart and initiates checkout.   To implement the dashboard:
 
1. Follow the steps in the [implementation guide](https://docs.newrelic.com/docs/new-relic-solutions/observability-maturity/customer-experience/bofta-implementation-guide/#establish-current-state) to determine steps in the user journey that you will measure

2. Download the [dashboard json](botf.json). 

3. Edit botf.json and change ACCOUNT_ID to the account id that you will run most of the queries from.  Edit the filters.

4. Import the JSON as a new Dashboard via the main Dashboards menu.
![Dashboard import](../images/ImportDashboard.png?raw=true "Dashboard import")

5. Edit the imported dashboard 

## Dashboard organization

The dashboard is organized into sections.   The four widgets at the top make up the summary data.  Summary data includes the bottom of the funnel conversion rate, synthetics checks results, and revenue at risk.   

The performance of each step making up the bottom of the funnel follows below the summary data.  Performance data varies depending on the interaction type.  
* If the interaction is a PageView, you will capture Core Web Vitals and time to first byte.  
* If the interaction is an AjaxRequest, you will capture time to settle and http response code types (successes vs errors).

## [Summary data queries](README_Botf_summary.md)
## [Step data queries](README_Botf_step_queries.md)

# KPI Measurement

<img src="images/CustomerExperience_Botf_KPIs.png" width="500">

The CustomerExperience_BotFAnalysis document provides a way to measure baselines and track progress while improving KPI performance.

1. Start with the format that works best for you, .ods, or .xls
2. Capture the current baseline.  Identify what needs improving and to what extent by highlighting it in yellow or red.  Highlight the rest in green.
3. Use other filters, as applicable, to identify other KPIs that need improving.  Capture only those that you plan to actively work on or measure.   Examples include KPIs filtered to mobile users where improvement is needed and impactful to the business.
4. Update KPI numbers weekly or after each sprint.  
5. Be aware of how long data is retained.  The KPI spreadsheet needs to be updated before retention of relevant data expires.
 




 