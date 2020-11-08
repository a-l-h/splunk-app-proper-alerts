Install
=======

Prerequisites
-------------

These Apps must be deployed to your Search Head(s):

- `Python Cron Iteration for Splunk <https://splunkbase.splunk.com/app/4027/>`_
- `Lookup File Editor <https://splunkbase.splunk.com/app/1724/>`_

Deployment steps
----------------

#.  `Install the App on your Splunk Search Head(s) <https://docs.splunk.com/Documentation/Splunk/latest/Admin/Deployappsandadd-ons#Deployment_architectures>`_
#.	Launch **Update KV Store lookup** from Reports tab by clicking ``Open in Search``
#.  Verify that active alerts are listed in the **Inventory** dashboard
#.  [OPT] Adjust **getServiceRequest** macro to extract service request # from alerts' description
#.  Set recipient to **Notify admin for alerts to review** alert or disable it
#.  [WARN] Set recipient to **Notify alert recipient of a change** alert as ``$result.email$`` or disable it

.. warning:: **Notify alert recipient of a change** alert will send an email to alert's recipient when triggered.

Upgrade
-------

Relaunch **Update KV Store lookup** from Reports tab by clicking ``Open in Search``
