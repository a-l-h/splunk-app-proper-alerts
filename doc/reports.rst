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
     - Define the owner as being the local-part of the first recipient email address
   * - 7-9
     - Extract service request reference from the description field, using macro ``getServiceRequest``
   * - 10
     - Clean ``updated`` field
   * - 11
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

Also save the MD5 hash of the search query.

.. list-table::
   :widths: 20 80
   :header-rows: 0

   * - 12-14
     - Use `Cron Iteration <https://splunkbase.splunk.com/app/4027/#/details>`_ command to calculate the interval between 2 executions
   * - 15-16
     - Prefix all fields name except ``alert`` & ``app`` with ``new_`` for later comparison
   * - 17-27
     - Determine the maximum runtime from scheduler logs
   * - 28
     - Filter out alerts only present in scheduler logs

Compare it to current KV Store lookup entries
+++++++++++++++++++++++++++++++++++++++++++++

.. list-table::
   :widths: 20 80
   :header-rows: 0

   * - 29-30
     - Add the current content of the KV Store lookup to the results for comparison
   * - 31
     - Group both data sets (1-6 & 37-38) by ``alert`` and by ``app``
   * - 32
     - If the MD5 of main fields have changed or if runtime exceeds interval, keep the newest values
   * - 33
     - If the search period of schedule has changed, reset the *Alignment* check
   * - 34
     - If the search query has changed, reset the *Structure* check
   * - 35
     - If the search query has changed, reset the *Source* check
   * - 37
     - If the runtime exceeds the interval, update the *Runtime* check
   * - 39-40
     - Check if the search period has a minimum delay of 1 minute, if applicable
   * - 41-47
     - Fields clean up
   * - 48-51
     - Retrieve App label
     
Save results to the KV Store lookup
+++++++++++++++++++++++++++++++++++

.. list-table::
   :widths: 20 80
   :header-rows: 0

   * - 52
     - Call KV Store lookup to get the ``_key`` field for each entry to update
   * - 53
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
