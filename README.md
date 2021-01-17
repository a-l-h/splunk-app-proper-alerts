#	![](./doc/img/icon.svg) Proper Alerts


##	Version


1.1.5


##	Date


17 January 2021


##	Release Notes


* Saved searches can now be searched by type - alert or report
 

##	Documentation


[Read the Docs](https://proper-alerts.rtfd.io)


##	Prerequisites


These Apps must be deployed to your Search Head(s):

- [Python Cron Iteration](https://splunkbase.splunk.com/app/4027/)
- [Lookup File Editor](https://splunkbase.splunk.com/app/1724/)


##	Deployment Steps


1.	[Install the App on your Splunk Search Head(s)](https://docs.splunk.com/Documentation/Splunk/latest/Admin/Deployappsandadd-ons#Deployment_architectures)
2.	Launch *Update KV Store lookup* from Reports tab by clicking ``Open in Search``
3.	Verify that active alerts are listed in the *Inventory* dashboard
4.	[OPT] Adjust *getServiceRequest* macro to extract service request # from alerts' description
5.	Set recipient to *Notify admin for alerts to review* alert
6.	[WARN] Set recipient to *Notify alert recipient of a change* alert as ``$result.email$``

:warning: *Notify alert recipient of a change* alert will send an email to alert’s recipient when triggered


##	Upgrade


Relaunch *Update KV Store lookup* from Reports tab by clicking ``Open in Search``

:warning: *As 'type' is a new KV Store field, a change will be detected for all alerts, hence if you are using the 'Notify alert recipient of a change' alert, silence its first execution after the upgrade*


##	Contact


[a-l-h](https://github.com/a-l-h)

