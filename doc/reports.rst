Reports
=======

Update KV Store lookup
----------------------

This reports looks for all active alerts, perform the automatic checks against each and save results into a KV Store lookup.

Lets break down its search query:

Search for active alerts
++++++++++++++++++++++++

.. list-table::
   :widths: 20 80
   :header-rows: 0

   * - 1-2
     - Search for all enabled and scheduled alerts, then for each alert:
   * - 3
     - Check if the index is specified in the search query, if applicable, using macro ``indexIsSpecified``
   * - 5-6
     - Extract service request reference from the description field, using macro ``getServiceRequest``
   * - 8
     - Clean ``updated`` field
   * - 9
     - Save the MD5 hash of the concatenation of main fields for later comparison

Considered fields
*****************

.. list-table::
   :widths: 20 80
   :header-rows: 1

   * - Field
     - Field Description
   * - ``alert``
     - alert name
   * - ``app``
     - app name
   * - ``updated``
     - last update timestamp
   * - ``cron_schedule``
     - alert schedule
   * - ``cron_schedule``
     - alert schedule
   * - ``earliest_time``
     - search period earliest time
   * - ``latest_time``
     - search period latest time
   * - ``search``
     - search query
   * - ``email``
     - recipient(s)
   * - ``actions``
     - alert action(s)
   * - ``owner``
     - alert owner (knowledge object)

Also save the MD5 hash of the search query.

.. list-table::
   :widths: 20 80
   :header-rows: 0

   * - 10-12
     - Use `Cron Iteration <https://splunkbase.splunk.com/app/4027/#/details>`_ command to calculate the interval between 2 executions
   * - 13
     - Calculate the search time range interval using earliest and latest time
   * - 14
     - If search time range interval = cron schedule interval, or if query is not an ``index=foo`` search, *Alignment* check is passed
   * - 16-18
     - Prefix all fields name except ``alert`` & ``app`` with ``new_`` for later comparison
   * - 18-28
     - Determine the maximum runtime from scheduler logs
   * - 29
     - Filter out alerts only present in scheduler logs

Compare it to current KV Store lookup entries
+++++++++++++++++++++++++++++++++++++++++++++

.. list-table::
   :widths: 20 80
   :header-rows: 0

   * - 30-31
     - Add the current content of the KV Store lookup to the results for comparison
   * - 32
     - Group both data sets (1-2 & 30-31) by ``alert`` and by ``app``
   * - 33
     - If the MD5 of main fields have changed or if runtime exceeds interval, or if indexIsSpecified value differs, keep the newest values
   * - 34
     - If the search query has changed, reset the *Structure* check
   * - 35
     - If the search query has changed, reset the *Source* check
   * - 37
     - If the runtime exceeds the interval, update the *Runtime* check
   * - 39-40
     - Check if the search period has a minimum delay of 1 minute, if applicable
   * - 41-44
     - Fields clean up
   * - 45-48
     - Retrieve App label
     
Save results to the KV Store lookup
+++++++++++++++++++++++++++++++++++

.. list-table::
   :widths: 20 80
   :header-rows: 0

   * - 49
     - Call KV Store lookup to get the ``_key`` field for each entry to update
   * - 50
     - Update ``alert_lookup`` KV store lookup entries with the results

The output can be both:

- alerts created after the last run of the report
- alerts modified since the last run of the report

.. warning:: Report runs every hour. If you change its cron schedule to your needs, adjust time range accordingly.

Clean KV Store lookup
---------------------

Whenever an alert is enabled and scheduled, it is saved it the KV Store lookup thanks to the ``Update KV Store lookup`` report above.

If the same alert is disabled or even deleted later on, it has to be removed from the KV Store lookup.

This is what the ``Clean KV Store lookup`` report does, removing disabled or deleted alerts from the KV Store lookup.


.. list-table::
   :widths: 20 80
   :header-rows: 0

   * - 1
     - Load the current content of the KV Store lookup
   * - 2
     - Mark this data set with the key value ``source=kv_store``
   * - 3-7
     - Append the list of enabled and scheduled alerts marked with key value ``source=rest``
   * - 8
     - Group both data sets (1-2 & 3-7) by ``alert`` and by ``app``
   * - 9
     - Count the number of data sets each alert is in
   * - 10
     - Filter out alerts that are only part of 1 data set
   * - 12
     - Save results to the KV store
     
.. hint:: In simple steps, the report loads all entries from the KV Store lookup, takes out disabled or deleted alerts, and overwrites the output back to the lookup. As a result, deleted or disabled alerts are no longer in the lookup.
