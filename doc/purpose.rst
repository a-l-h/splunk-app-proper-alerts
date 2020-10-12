

Purpose
=======

It is pretty easy for Splunk admins to lost track on Splunk alerts. The data source could no longer exist, the search query could be malformed, search period and time schedule could be uncoordinated and so on.

This could be addressed by reviewing alerts from time to time but there is a more efficient way that consists in reviewing alerts once, and then only review alerts whenever a change occurs after being notified about it.

This is the purpose of this App: help Splunk admins to continuously maintain properly configured alerts.

To do so, the App leverages Splunk KV Store to save a collection of configured alerts which gets updated every time an alert is added, modified or deleted, and uses an interactive dashboard to let Splunk admin review the alert beased on defined checks.


