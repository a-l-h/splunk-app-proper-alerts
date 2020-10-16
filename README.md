#	![](https://github.com/a-l-h/splunk-app-proper-alerts-doc/blob/master/doc/img/logo.svg) Proper Alerts


##	Version


1.0.1


##	Date


21 October 2020


##	Release Notes


- Initial release


##	Documentation


[Read the Docs](https://splunk-proper-alerts.rtfd.io)


##	Prerequisites


These Apps must be deployed to your Search Head(s):

- [Gemini KV Store Tools](https://splunkbase.splunk.com/app/3536/)
- [Python Cron Iteration](https://splunkbase.splunk.com/app/4027/)
- [Lookup File Editor](https://splunkbase.splunk.com/app/1724/)


##	Deployment Steps


1.	[Install the App on your Splunk Search Head(s)](https://docs.splunk.com/Documentation/Splunk/latest/Admin/Deployappsandadd-ons#Deployment_architectures)
2.	Launch *Update KV Store lookup* alert to populate data by setting cron schedule to the next minute
3.	Go to *Inventory* dashboard to check if active alerts are listed in the first panel
4.	[Optional] Adjust *getServiceRequest* macro if you want to extract the service request reference from alerts' description field
5.	Adjust Update *KV Store lookup* alert cron schedule as needed (and time range accordingly)
7.	[Optional] Enable *Notify admin for alerts to review* alert and adjust recipient
8.	[Optional] Enable *Notify alert owner of a change* alert but note that the fallback recipient maps to the one defined above


##	Contact


[a-l-h](https://github.com/a-l-h)

