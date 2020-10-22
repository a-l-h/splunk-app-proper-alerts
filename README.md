#	![](https://github.com/a-l-h/splunk-app-proper-alerts/blob/master/doc/img/logo.svg) Proper Alerts


##	Version


1.0.6


##	Date


23 October 2020


##	Release Notes


- Initial release


##	Documentation


[Read the Docs](https://proper-alerts.rtfd.io)


##	Prerequisites


These Apps must be deployed to your Search Head(s):

- [Python Cron Iteration](https://splunkbase.splunk.com/app/4027/)
- [Lookup File Editor](https://splunkbase.splunk.com/app/1724/)


##	Deployment Steps


1.	[Install the App on your Splunk Search Head(s)](https://docs.splunk.com/Documentation/Splunk/latest/Admin/Deployappsandadd-ons#Deployment_architectures)
2.	Set cron schedule for *Update KV Store lookup* report to the next minute
3.	Verify that active alerts are listed in the *Inventory* dashboard
4.	[OPTIONAL] Adjust *getServiceRequest* macro to extract service request # from alerts' description
5.	Set recipient to *Notify admin for alerts to review* alert or disable it
6.	[CAUTION] Set recipient to *Enable Notify alert owner of a change* alert as ``$result.email$`` or disable it

| WARNING: be careful to baz the quux before initializing the retro encabulator! |
| --- |


##	Contact


[a-l-h](https://github.com/a-l-h)


