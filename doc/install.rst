Install
=======

Prerequisites
#############

These Apps must be deployed to your Search Head(s):

- `Gemini KV Store Tools <https://splunkbase.splunk.com/app/3536/>`_
- `Python Cron Iteration for Splunk <https://splunkbase.splunk.com/app/4027/>`_
- `Lookup File Editor <https://splunkbase.splunk.com/app/1724/>`_

Deployment Steps
################

1.  `Install the App on your Splunk Search Head(s) <https://docs.splunk.com/Documentation/Splunk/latest/Admin/Deployappsandadd-ons#Deployment_architectures>`_
#.  Set cron schedule for **Update KV Store lookup** alert to the next minute 
#.  Open the **Inventory** dashboard to check if active alerts are listed in the panel
#.  [OPT] Adjust **getServiceRequest** macro to extract service request # from alerts' description
#.  [OPT] Enable **Notify admin for alerts to review** alert and adjust recipient
#.  [OPT] Enable **Notify alert owner of a change** alert
