Alerts
======

Update KV Store lookup
######################

As previously mentioned  :ref:`anchor text <overview:kv-store-lookup>`  , this alert looks for active alerts, performs the automatic checks :ref:`Automatic Checks` and save the result to a KV store lookup.

It can be broken down in more detailed steps:

Remove deleted alerts from the lookup
-------------------------------------

1. Load KV Store lookup
2. Filter out enabbled and shceduled alerts to obtain the list of alerts that exist in the lookup but are not active in Splunk anymore
3. Call KV Store lookup to get the ``_key`` field of each alert entry to be deleted
4. Delete alert entries from the lookup using `Gemini KV Store Tools custom command <https://splunkbase.splunk.com/app/3536/#/details>`_

Search for active alerts
------------------------

5. Search for all enabled and scheduled alerts, then for each alert:
6. Check if the index is specified in the search query if aplicable, using macro ``indexIsSpecified``
7. Define the owner as being the local-part of the first recipient email address
8. Save the md5 checksum of the concatenation of main fields for later comparison

Considered fields
*****************

+---------------+-----------------------------+
| Field         | Field Description           |
+===============+=============================+
| alert         | alert name                  | 
+---------------+-----------------------------+
| app           | app name                    |
+---------------+-----------------------------+
| updated       | last update timestamp       | 
+---------------+-----------------------------+
| cron_schedule | alert schedule              |
+---------------+-----------------------------+
| earliest_time | search period earliest time |
+---------------+-----------------------------+
| latest_time   | search period latest time   |
+---------------+-----------------------------+
| search        | search query                |
+---------------+-----------------------------+
| email         | recipient email(s)          |
+---------------+-----------------------------+
| actions       | alert action(s)             |
+---------------+-----------------------------+

Also save a md5 checksum of search query independently

9. Use Cron Iteration command to calculate the interval between 2 executions
10. Search scheduler logs to determine the maximum runtime
11. Add the current content of the KV Store lookup to the results for comparison
12. If the md5 checksum of alert's main fields has changed, keep the newest values
13. If the search period of schedule has changed, reset the 'Alignment' check
14. If the search query has changed, reset the 'Structure' check
15. If the runtime exceeeds the interval, update the 'Runtime' check
16. Check if the search period has a minimum delay of 1 minute, if applicable
17. Call KV Store lookup to get the key of each entry to update

Workflow for that

Notify admin for alerts to review
#################################



Notify alert owner of a change 
##############################


