Install
=======

Prerequisites
#############

The following Apps must be deployed to your Search Head(s)

- `Gemini KV Store Tools <https://splunkbase.splunk.com/app/3536/>`_
- `Python Cron Iteration for Splunk <https://splunkbase.splunk.com/app/4027/>`_
- `Lookup File Editor <https://splunkbase.splunk.com/app/1724/>`_

Deployment Steps
################

1.  `Install the App on your Splunk Search Head(s) <https://docs.splunk.com/Documentation/Splunk/latest/Admin/Deployappsandadd-ons#Deployment_architectures>`_
2.  Launch **Update KV Store lookup** alert to populate data: adjust cron schedule to the next minute 
3.  Go to **Inventory** dashboard: active alerts should be listed in the first panel
4.  [Optional] Adjust **getServiceRequest** macro if you want to extract the service request reference from the description field of each alert
5.  Adjust **Update KV Store lookup** alert cron schedule as needed (and time range accordingly)
6.  [Optional] Enable **Notify admin for alerts to review** alert and adjust recipient
7.  [Optional] Enable **Notify alert owner of a change** alert but note that **the fallback recipient maps to the one defined above**
