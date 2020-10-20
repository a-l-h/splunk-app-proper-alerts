Browse KPIs
-----------

``Issues`` dashboard is stats oriented.

Its purpose is to ease alert reviewing by tracking down its progression:

.. image:: img/issues_panels.png
   :align: center

Stats can be shown by app, owner or even status, reviewed or not.

Click on a panel title to obtain the list of alerts related to each stat:

.. image:: img/issues_drilldown.png
   :align: center
   
Use the ``Close`` button to hide the panel back.

Besides stats on defined :hoverxref:`Alert checks<Alert Checks>`, 3 additional checks are provided:

.. list-table::
   :widths: 20 80
   :header-rows: 1

   * - Check
     - Description
   * - In multiple apps
     - The same alert is configured in multiple Apps
   * - Duplicate alerts
     - Several alerts share the same search query, schedule time and time range
   * - No action
     - Alert has no configured action
     
.. admonition:: In multiple apps

   This is not a big issue since Splunk merges the parameters across different Apps 
   but it can lead to confusion when editing the alert so it should be fixed.

.. admonition:: Duplicate alerts

   As it might indicate a duplicate alert - same alert, different name - it should
   be checked.

.. admonition:: No action

   The search for this check discards actions that could be part of the search query 
   (e.g. outputlookup). This should be investigated first to understand the purpose 
   of having such alerts or reports wihtout action.

.. note:: These additonal checks are global, meaning dashboard's top filters does not apply.
