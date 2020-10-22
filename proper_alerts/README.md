#	Proper Alerts


##	Version


1.0.7


##	Date


22 October 2020


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
4.	[OPT] Adjust *getServiceRequest* macro to extract service request # from alerts' description
5.	Set recipient to *Notify admin for alerts to review* alert or disable it
6.	[WARN] Set recipient to *Notify alert owner of a change* alert as ``$result.email$`` or disable it

:warning: *Notify alert owner of a change* alert will send an email to alert’s recipient when triggered


##	Contact


[a-l-h](https://github.com/a-l-h)




