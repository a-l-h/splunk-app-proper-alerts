Resolve Spreading Issues
------------------------

Spreading issues are addressed in the :hoverxref:`Concurrency dashboard<Concurrency dashboard>`.

The first panel shows the number of alerts scheduled over time against the maximum number of concurrent shcedule searches that Splunk scheduler can run:

.. image:: img/concurrency_panel_1.png
   :align: center

The idea is to spot too busy schedules and to set alerts on more diverse ones to avoid concurrency limit to be maxed out.

There are 3 versions of the dashboard, each having his own source for determining the number of alert running every minute.

Additional info is provided within the dashboard accessible from the ℹ️ button:

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Data source
     - Info
   * - Croniter 
     - Python Cron Iteration for Splunk convert each alert schedule to a timestamp
   * - Scheduler 
     - Scheduled search log events
   * - Search ID
     - Search IDs events

.. tip:: As Croniter converts alerts' cron schedules into timestamps, any alert adjustment would be reflected right after a panel refresh.

Additional panels underneath have the same purpose of spotting busy schedules by showing the most used ones:

.. image:: img/concurrency_panel_2.png
   :align: center

.. tip:: Clicking on a cron schedule would open a new panel with matching alerts which can then be clicked again to open alert's edit page.
