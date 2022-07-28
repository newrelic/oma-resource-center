  
# Bottom of the funnel analysis dashboard

![Bottom of the Funnel Analysis example](images/CustomerExperience_BotFunnelAnalysis.png?raw=true "Cx Bottom of the Funnel")

The bottom of the funnel analysis dashboard measures the user experience during the critical phase of the user's journey, which starts when the user passes a threshold indicating intent to complete an action.  For example, when a user goes to a cart and initiates checkout.   To implement the dashboard:
 
1. Follow the steps in the [implementation guide](https://docs.newrelic.com/docs/new-relic-solutions/observability-maturity/customer-experience/bofta-implementation-guide/#establish-current-state) to determine steps in the user journey that you will measure

2. Download the dashboard json files.
* [botf_summary.json](botf_summary.json) Dashboard frame including dashboard title and funnel summary charts
* [botf_ajax.json](botf_ajax.json) Ajax latency and response code charts.  Use for any steps that are Ajax requests
* [botf_pageview.json](botf_pageview.json) Pageview time to first byte and CoreWebVital charts.  Use for any steps that are page views

3. Make copies of botf_ajax.json and botf_pageview.json for each step.  For example, if your bottom of the funnel consists of two AJAX calls and no page views, make a botf_ajax_step1.json, botf_ajax_step2.json and discard botf_pageview.json. 

4. Edit each json file and change ACCOUNT_ID to the account id that you will run most of the queries from.  Edit the filters in the summary data and step data queries per the instruction links below.

5. Assemble the dashboard by inserting the json from the steps after line 147 of botf_summary.json.  

6. Import the JSON as a new Dashboard via the main Dashboards menu.  __Tip:__ if the dashboard can't be imported it will mostly likely be due to errors in one or more the queries.  Other reasons may be JSON errors or lack of permissions.  If you experience this, you can try testing exporting any dashboard and reimporting.  Once that works, you can import the dashboard in phases, starting with botf_summary.json and building from there.
![Dashboard import](../images/ImportDashboard.png?raw=true "Dashboard import")

7. Review the dashboard and edit further if needed. 

## Dashboard organization

The dashboard is organized into sections.   The four widgets at the top make up the summary data.  Summary data includes the bottom of the funnel conversion rate, synthetics checks results, and revenue at risk.   

The performance of each step making up the bottom of the funnel follows below the summary data.  Performance data varies depending on the interaction type.  
* If the interaction is a PageView, you will capture Core Web Vitals and time to first byte.  
* If the interaction is an AjaxRequest, you will capture time to settle and http response code types (successes vs errors).

## [Summary data queries](README_Botf_summary.md)
## [Step data queries](README_Botf_step_queries.md)

# KPI measurement

<img src="images/CustomerExperience_Botf_KPIs.png" width="500">

The CustomerExperience_BotFAnalysis document provides a way to measure baselines and track progress while improving KPI performance.

1. Start with the format that works best for you, .ods, or .xls
2. Capture the current baseline.  Identify what needs improving and to what extent by highlighting it in yellow or red.  Highlight the rest in green.
3. Use other filters, as applicable, to identify other KPIs that need improving.  Capture only those that you plan to actively work on or measure.   Examples include KPIs filtered to mobile users where improvement is needed and impactful to the business.
4. Update KPI numbers weekly or after each sprint.  
5. Be aware of how long data is retained.  The KPI spreadsheet needs to be updated before retention of relevant data expires.
 




 