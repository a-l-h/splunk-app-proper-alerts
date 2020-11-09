#	![](./doc/img/icon.svg) Proper Alerts


##	Version


1.1.3


##	Date


9 November 2020


##	Release Notes


* Fixed *No action* check in *Issues* dashboard
* Added *Close names* check in *Issues* dashboard
* Fixed *Update KV Store lookup* query
  * recipient field is set only if ``action.email`` is true
  * ``triggeredalerts`` is added to ``actions`` when ``alert.track`` is true 
  * null fields are set to ``N/A`` so that MD5 hash is never empty
 

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
5.	Set recipient to *Notify admin for alerts to review* alert or disable it
6.	[WARN] Set recipient to *Notify alert recipient of a change* alert as ``$result.email$`` or disable it

:warning: *Notify alert recipient of a change* alert will send an email to alert’s recipient when triggered


##	Upgrade


Relaunch *Update KV Store lookup* from Reports tab by clicking ``Open in Search``


##	Contact


[a-l-h](https://github.com/a-l-h)

