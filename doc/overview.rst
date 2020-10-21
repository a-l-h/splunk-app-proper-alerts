Overview
========

The App arbitrarily defines 6 :ref:`alerts checks<Alert checks>` each alert should pass.

These checks are either :ref:`automatically<Automatic checks>` performed by :ref:`App's main report<KV Store lookup>` or manually reviewed by Splunk admins through an :ref:`interactive dashboard<Inventory dashboard>`.

Alert checks
------------

.. list-table::
   :widths: 10 80 10
   :header-rows: 1

   * - Check
     - Definition
     - Type
   * - Source
     - Target data source must be indexed
     - Manual
   * - Index
     - If applicable, target index(es) must be specified in the search query
     - Automatic
   * - Runtime
     - Runtime must be lower than the interval between one run to the next
     - Automatic
   * - Alignment
     - Alert schedule must be coordinated with search time range
     - Automatic
   * - Delay
     - Alert must be scheduled with at least one minute of delay  
     - Automatic
   * - Structure
     - Search query must be correctly structured 
     - Manual

Automatic checks
++++++++++++++++

Index
*****

When there is no index specified in a search query, Splunk searches in all available allowed indexes. This is not optimal in terms of resource usage and it is best practice to specify index(es) to be searched within the query. 
Searches that use alternate search commands in which index has not to be specified (e.g. ``dbxquery``, ``inputlookup``) are not taken into account (i.e. such queries are marked as having index specified). `Resource <https://docs.splunk.com/Documentation/Splunk/latest/Search/Writebettersearches#Restrict_searches_to_the_specific_index>`_

Runtime
*******

When Splunk takes so much time to execute the query that search job is not finished when the alert's next run launches.

Alignment
*********

Alert schedule must be coordinated with search time range.
For instance, an alert running every 5 minutes should have a time range of 5 minutes to avoid duplicate alerts and for better use of resources. `Resource <https://docs.splunk.com/Documentation/Splunk/latest/Alert/AlertSchedulingBestPractices#Coordinate_an_alert_schedule_and_search_time_range>`_

Delay
*****

It is better practice to leave some delay on alerts by configuring a latest time of at least 1 minute. `Resource <https://docs.splunk.com/Documentation/Splunk/latest/Alert/AlertSchedulingBestPractices#Schedule_alerts_with_at_least_one_minute_of_delay>`_


Manual checks
+++++++++++++

Source
******

Is there any data at all when you run alert's base search (i.e. query's first line)?

Structure
*********

This a way more subjective check whose goal is to make sure search queries are properly written considering searches best practices. `Resource <https://www.splunk.com/en_us/blog/tips-and-tricks/splunk-clara-fication-search-best-practices.html>`_

KV Store lookup
---------------

The ``Update KV Store lookup`` report is the core function of the App.

It checks for all enabled and scheduled alerts, perform the automatic checks and save results into a KV Store lookup.

:ref:`See Update KV Store lookup report<Update KV Store lookup>`

Inventory dashboard
-------------------

This dashboard loads KV Store lookup entries and lets Splunk admins review each alert independently. 

During the review the admin will address alert manual checks and save results to the KV Store through interactive buttons. 

:ref:`See Review Alerts<Review Alerts>`

Concurrency dashboard
---------------------

The goal of this dashboard is to help resolve alert spreading issues.

Whith a growing number of alerts, there could be plenty of alerts launching at the same schedule.

This could be limited by the maximum concurrent scheduled searches Splunk scheduler can run.

Hence, the idea is to represent the number of alerts launched over time against this concurrency limit so it becomes easy to spot too busy schedules.

:ref:`See Improve Spreading<Improve Spreading>`
