Alerts
======

Update KV Store lookup
######################

As :ref:`previously mentioned<KV Store lookup>`, this alert looks for active alerts, performs the :ref:`automatic checks<Automatic Checks>` and save the result to a KV store lookup.

Its search query can be broken down in more detailed steps:

Remove deleted alerts from the lookup
------------------------------------------------

1.      Load KV Store lookup
2-5.    Filter out enabbled and scheduled alerts to obtain the list of alerts that exist in the lookup but are not active in Splunk anymore
6.      Call KV Store lookup to get the ``_key`` field of each alert entry to be deleted
7.      Delete alert entries from the lookup using `Gemini KV Store Tools custom command <https://splunkbase.splunk.com/app/3536/#/details>`_

Search for active alerts
------------------------

8-9.    Search for all enabled and scheduled alerts, then for each alert:
11.     Check if the index is specified in the search query if aplicable, using macro ``indexIsSpecified``
13-14.  Define the owner as being the local-part of the first recipient email address
15.     Extract service request reference from description field, using macro ``getServiceRequest``
18.     Clean the updated field
19.     Save the md5 checksum of the concatenation of main fields for later comparison

Considered fields
*****************

+---------------+-----------------------------+
| Field         | Field Description           |
+===============+=============================+
| ``alert``     | alert name                  | 
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

Also save a md5 checksum of search query.

20-22.  Use Cron Iteration command to calculate the interval between 2 executions
23-24.  Prefix all fields name except alert & app with ``new_`` for later comparison
25-35.  Determine the maximum runtime from scheduler logs of Search Head or Search Head Cluster members, if applicable (27-33)
36.     Filter out alerts only present in scheduler logs
37-38.  Add the current content of the KV Store lookup to the results for comparison
39.     Group both data sets (1-6 & 37-38) by alert and by app
40.     If the md5 checksum of alert's main fields has changed or if runtime is longer than interval, keep the newest values
41.     If the search period of schedule has changed, reset the *Alignment* check
42.     If the search query has changed, reset the *Structure* check
43.     If the search query has changed, reset the *Source* check
45.     If the runtime exceeds the interval, update the *Runtime* check
46-47.  Check if the search period has a minimum delay of 1 minute, if applicable
48-55.  Fields clean up
56-59.  Retrieve App label using a subsearch
60.     Call KV Store lookup to get the ``_key`` field for each entry to update

The output is saved to KV Store lookup **alerts_lookup** using Gemini's custom alert action.

Workflow for that

Notify admin for alerts to review
#################################

This alert notifies Splunk admins of the count of alerts that need to be reviewed.

The idea is to enable it after the first initial review of all alerts so that Splunk admins get notified of any alert to review whether new of modified.

The recipient(s) must be set and the schedule should be adjusted to your needs.

Notify alert owner of a change 
##############################

This alert notifies the owner of an alert of any change made on an alert he owns.

The goal is to avoid any issue that could arise from unsolicited or unannounced modifications.

The recipient of this alert is the recipient of the modified alert?

Search query steps:


1.      Search for all enabled and scheduled alerts, then for each alert:
2.      Save the md5 checksum of the concatenation of main fields for later comparison (link similar to ^^)
3.      Prefix all fields name except alert & app with ``new_`` for later comparison
5.      Load KV Store lookup entries that do have an owner, that is mail recipient(s) as owner field is derived from email.to field
6.      Group both data sets (1 & 5) by alert and by app
7.      Filter out results having the same md5 of main fields on both data sets.
8.      Do some eval tricks among main alert fields to identify the ones that have been modified
9.      Retrieve App label using a subsearch
10.     Check if the email is valid
11.     If email is not valid set it to the one set in "Notify admin for alerts to review" as it should be Splunk admins email
12.     Add ``invalid_email`` field to identify invalid emails...

