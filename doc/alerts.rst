Alerts
======

Update KV Store lookup
----------------------

Its search query broken down in detailed steps:

Remove deleted alerts from the lookup
*************************************

.. list-table::
   :widths: 20 80
   :header-rows: 1

   * - Lines
     - Description
   * - 1
     - Load KV Store lookup
   * - 2-5
     - Filter out active alerts to obtain the list of alerts to be removed from the KV Store lookup
   * - 6
     - Call KV Store lookup to get the ``_key`` field of each alert entry to be deleted
   * - 7
     - Delete alert entries from the lookup using `Gemini KV Store Tools <https://splunkbase.splunk.com/app/3536/#/details>`_ custom command

