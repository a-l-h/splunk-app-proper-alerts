How does it work?
=================


Arbitrary Alert Checks
######################

Each alert should pass 6 arbitrary checks defined within the App:

+-------------+-------------------------------------------------------------------------------------------------+---------------------+---------------------+
| Check       | Definition                                                                                      | Type                | Resource            |
+=============+=================================================================================================+=====================+=====================+
| Source      | Data source must be indexed                                                                     | Manual              |                     |
+-------------+-------------------------------------------------------------------------------------------------+---------------------+---------------------+
| Index       | If applicable, target index(es) must be specified                                               | Automatic           |                     |
+-------------+-------------------------------------------------------------------------------------------------+---------------------+---------------------+
| Runtime     | Runtime must be lower than the gap between two executions                                       | Automatic           |                     |
+-------------+-------------------------------------------------------------------------------------------------+---------------------+---------------------+
| Alignment   | Schedule must be coordinated with the search time range                                         | Manual              |                     |
+-------------+-------------------------------------------------------------------------------------------------+---------------------+---------------------+
| Delay       | Must have at least 1 minute delay (i.e. latest_time must not be "now")                          | Automatic           |                     |
+-------------+-------------------------------------------------------------------------------------------------+---------------------+---------------------+
| Structure   | Must be correctly strutured (e.g. careful usage of join & transition, filters added the sooner) | Manual              |                     |
+-------------+-------------------------------------------------------------------------------------------------+---------------------+---------------------+


Update KV Store lookup alert
############################


The "Update KV Store lookup" alert is the core function of the App.

It checks for all enabled and scheduled alerts, perform the automatic checks and save results into a KV Store lookup.

It performs CRUD operations to the KV store collection:

- If the alert does not exist anymore since the last execution of the alert, its entry is deleted from

- If the alert has changed since the last exection of the alert, its entry is updated

- If the alert has been created since the last execution of the alert, a new entry is created

More details on the alert here....


Inventory dashboard
###################


Splunk admins can then use this dashboard to review alerts and manually update the KV store with manual checks

Workflow images

More details here
