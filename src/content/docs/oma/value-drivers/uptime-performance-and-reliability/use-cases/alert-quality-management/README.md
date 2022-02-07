# observability-maturity
Observability Maturity Architecture Alert Quality Management assets.

## Alert Quality Management Dashboard JSON Instructions

1. Setup the Alert Webhook (see below)
1. Copy the dashboard JSON in this repo into your favorite text editor.
1. Search and Replace all instances of `"accountId": 0000000` with the account ID of your primary production account.
1. Import the dashboard JSON into your primary production account.


## Alerting Webhook Instructions

1. In the New Relic UI, go to **API Keys** - **Insights Insert Keys** and create a new insert API key. Be prepared to copy the API key as well as the highlighted URL (see screenshot below), Keep in mind that if your account has been enabled for FedRAMP, your endpoint should be ```gov-insights-collector.newrelic.com``` instead of ```insights-collector.newrelic.com```. See [Event API under FedRAMP Services](https://docs.newrelic.com/docs/security/security-privacy/compliance/fedramp-compliant-endpoints/#event-api) 

![Alt text](images/insights_key.png?raw=true "Insights")

2. In the New Relic UI, go to **Alerts & AI** - **Notifications Channels**
3. Add a **Webhook** notification channel.
4. Set the **Channel name** to a meaningful value.
5. Set the **Base url** to the URL generated in the step above.
6. Add a custom header "X-Insert-Key" and add the API key you created in the step above
7. At the top of the **Payload** JSON add the following text:
   `"eventType": "nrAQMIncident",`

![Alt text](images/notification_channel.png?raw=true "Notification Channel")

8. Click the **Save** button.
  - Click **Send Test notification**
  - In New Relic query builder, execute the query: ``select * from nrAQMIncident`` and ensure your test notification is shown
  ![Alt text](images/incident_query.png?raw=true "query")
  - Go back to the notification channel, click on the **Alert Policies** tab and click the **Add Alert Policies** button.
  - Add the webhook to ALL alert policies.
