# observability-maturity
Observability Maturity Architecture Alert Quality Management assets.

NOTE: Prior releases of Alert Quality Management used a webhook to create a custom event (nrAQMIncident) to collect the KPIs that drive this process.  That webhook and custom event are **no longer required**.  Instead, an out of box event (NrAiIssue) is used.  See the [Alert Quality Management implementation guide](https://docs.newrelic.com/docs/new-relic-solutions/observability-maturity/uptime-performance-reliability/alert-quality-management-guide) for details.

## Alert Quality Management Dashboard JSON Instructions

1. Copy the dashboard JSON in this repo into your favorite text editor.
1. Search and Replace all instances of `"accountId": 0000000` with the account ID of the account you're importing this dashbaord into.
1. [Import the dashboard JSON](https://docs.newrelic.com/docs/query-your-data/explore-query-data/dashboards/introduction-dashboards/#dashboards-import).

