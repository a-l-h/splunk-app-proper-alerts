#	![](https://github.com/a-l-h/splunk-app-proper-alerts/blob/master/doc/img/logo.svg) Proper Alerts


##	Version


1.0.1


##	Date


20 October 2020


##	Release Notes


- Initial release


##	Documentation


[Read the Docs](https://proper-alerts.rtfd.io)


##	Prerequisites


These Apps must be deployed to your Search Head(s):

- [Gemini KV Store Tools](https://splunkbase.splunk.com/app/3536/)
- [Python Cron Iteration](https://splunkbase.splunk.com/app/4027/)
- [Lookup File Editor](https://splunkbase.splunk.com/app/1724/)


##	Deployment Steps


1.	[Install the App on your Splunk Search Head(s)](https://docs.splunk.com/Documentation/Splunk/latest/Admin/Deployappsandadd-ons#Deployment_architectures)
2.	Set cron schedule for *Update KV Store lookup* alert to the next minute
3.	Open the *Inventory* dashboard to check if active alerts are listed in the panel
4.	[OPT] Adjust getServiceRequest macro to extract service request # from alerts' description
5.	[OPT] Enable Notify admin for alerts to review alert and adjust recipient
6.	[OPT] Enable Notify alert owner of a change alert


##	Contact


[a-l-h](https://github.com/a-l-h)


