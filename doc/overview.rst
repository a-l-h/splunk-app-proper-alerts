How does it work?
=================


Alert Checks
############

Six different alerts checks are defined within the App:

+-------------+-----------------------------------------------------------+-----------+
| Check       | Definition                                                | Type      |
+=============+===========================================================+===========+
| Source      | Data source must be indexed                               | Manual    |
+-------------+-----------------------------------------------------------+-----------+
| Index       | If applicable, target index(es) must be specified         | Automatic |
+-------------+-----------------------------------------------------------+-----------+
| Runtime     | Runtime must be lower than the gap between two executions | Automatic |
+-------------+-----------------------------------------------------------+-----------+
| Alignment   | Schedule must be coordinated with the search time range   | Manual    |
+-------------+-----------------------------------------------------------+-----------+
| Delay       | Must have at least 1 minute delay                         | Automatic |
+-------------+-----------------------------------------------------------+-----------+
| Structure   | Must be correctly strutured                               | Manual    |
+-------------+-----------------------------------------------------------+-----------+

Automatic Checks
****************

Index
-----

When there is no index specified in a search query, Splunk searches in all available indexes (depending on owner's role). This is not optimal in terms of resource usage and it is best practice to specify index(es) to be searched within the query. 
Searches that use alternate search commands in which index has not to be specified (e.g. dbxquery, inputlookup) are not taken into account (i.e. such queries are marked as having index specified).

`Resource <https://docs.splunk.com/Documentation/Splunk/latest/Search/Writebettersearches#Restrict_searches_to_the_specific_index>`_

Runtime
-------

When Splunk takes so much time to execute the search that it has not finished when the next execution starts.

Delay
-----

It is better practice to leave some delay on alerts by configuring a latest time of at least 1 minute.

`Resource <https://docs.splunk.com/Documentation/Splunk/latest/Alert/AlertSchedulingBestPractices#Schedule_alerts_with_at_least_one_minute_of_delay>`_


Manual Checks
*************

Source
------

Is there any data at all when you run alert's base search (i.e. query's first line)?

Alignment
---------

Schedule must be coordinated with search time range.
For instance, an alert executed every 5 minutes should have a time range of 5 minutes to avoid duplicate alerts and for better usage of resources. 

`Resource <https://docs.splunk.com/Documentation/Splunk/latest/Alert/AlertSchedulingBestPractices#Coordinate_an_alert_schedule_and_search_time_range>`_

Structure
---------

This a way more subjective check whose goal is to make sure search queries are properly written considering searches best practices.

Resource <https://www.splunk.com/en_us/blog/tips-and-tricks/splunk-clara-fication-search-best-practices.html>`_


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
