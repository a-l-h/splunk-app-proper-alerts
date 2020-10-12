Prerequisites
=============

The following Apps must be deployed to your Search Head(s)

- `Gemini KV Store Tools <https://splunkbase.splunk.com/app/3536/>`_
- `Python Cron Iteration for Splunk <https://splunkbase.splunk.com/app/4027/>`_
- `Lookup File Editor <https://splunkbase.splunk.com/app/1724/>`_

Deployment Steps
================

1. `Install the App on your Splunk Search Head(s) <https://docs.splunk.com/Documentation/Splunk/latest/Admin/Deployappsandadd-ons#Deployment_architectures>`_

2. Launch ``Update KV Store lookup`` alert to populate data: adjust cron schedule to the next minute and wait for it to be triggerred

3. Go to ``Inventory`` dashboard: active alerts should be listed in the first panel

4. Adjust ``Update KV Store Lookup`` alert cron schedule as needed. It is set to run hourly by default. If you change the periodicity, adjust time range accordingly. 

5. [Optional] Enable ``Notify alert owner of a change`` alert.

6. [Optional] Set your team's email as the recipient to ``Notify admin for alerts to review`` alert and enable it.