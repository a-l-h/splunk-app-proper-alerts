#	![](./doc/img/icon.svg) Proper Alerts


##	Version


1.1.2


##	Date


8 November 2020


##	Release Notes


- Alert owner is now the owner of the knowledge object instead of the first recipient of the alert
- Index check has been improved
- Alerts and Apps can now be whitelisted from the checks
- *Notify alert recipient of a change* has be renamed to *Notify alert recipient of a change* and improved

* Fruit
  * Apple
  * Orange
  * Banana
* Dairy
  * Milk
  * Cheese
  
- test
 - subtest
- ok


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

:warning: *Notify alert owner of a change* alert will send an email to alert’s recipient when triggered


##	Upgrade


Relaunch *Update KV Store lookup* from Reports tab by clicking ``Open in Search``


##	Contact


[a-l-h](https://github.com/a-l-h)

