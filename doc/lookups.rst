Lookups
=======

This App uses 4 lookups, ``alerts_lookup``,  ``search_commands_lookup``,  ``alert_whitelist_lookup`` and ``app_whitelist_lookup``

All these lookups can be edited manually effortlessly from the ``Lookups`` tab which relies on `Splunk App for Lookup File Editing <https://splunkbase.splunk.com/app/1724/>`_.

KV Store lookup
---------------

``alert_lookup`` is the KV Store lookup that store the state of active alerts.

It has the following fields:

.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Field
     - Type
   * - ``actions``
     - string
   * - ``alert``
     - string
   * - ``app``
     - string
   * - ``app_label``
     - string
   * - ``cron_schedule``
     - string
   * - ``dataSourceExist``
     - bool
   * - ``dateLastReview``
     - number
   * - ``description``
     - string
   * - ``earliest_time``
     - string
   * - ``email``
     - string
   * - ``hasOwner``
     - bool
   * - ``hasServiceRequest``
     - bool
   * - ``indexIsSpecified``
     - bool
   * - ``interval``
     - number
   * - ``latest_time``
     - string
   * - ``md5``
     - string
   * - ``md5_search``
     - string
   * - ``owner``
     - string
   * - ``reviewer``
     - string
   * - ``run_time``
     - number
   * - ``runtimeIsLowerThanInterval``
     - bool
   * - ``scheduleHasAtLeastOneMinuteDelay``
     - bool
   * - ``search``
     - string
   * - ``searchIsCorrectlyStructured``
     - bool
   * - ``searchPeriodIsAlignedWithSchedule``
     - bool
   * - ``service_request``
     - string
   * - ``updated``
     - number
     
Search commands lookup
----------------------

``search_commands_lookup`` is the lookup that store splunk search commands.

It goes like this:

.. list-table::
   :widths: 33 33 33
   :header-rows: 1

   * - command
     - classic_search
     - output_command
   * - <Splunk command>
     - bool
     - bool

It is used in the :hoverxref:`indexIsSpecified<indexIsSpecified>` macro which checks if the index is specified in alerts' queries.

It is also used in the ``No action`` :hoverxref:`additional check<Additional Checks>` from the ``Issues`` dashboard which looks for alert without any configured action.

Whitelists
----------

You might want to whitelist an alert's specific check or even all alerts for a given App.

This is possible using whitelisting lookups.

.. hint:: In both whitelists below, the App name to use is the one from App's URL ``../en-US/app/<app_name>/..``

Alert whitelist lookup
++++++++++++++++++++++

Use this lookup if you want to whitelist a specific check for a given alert.

.. list-table::
   :widths: 15 15 15 15 15 15
   :header-rows: 1

   * - alert
     - app
     - index
     - runtime
     - alignment
     - delay
   * - <alert name>
     - <app name>
     - bool
     - bool
     - bool
     - bool

To whitelist an alert's specific checks, add alert's name and app, and set the check to be whitelisted to ``1``.

In the example below, alert ``foo`` from the ``bar`` App has both its index and alignment checks whitelisted:

.. list-table::
   :widths: 15 15 15 15 15 15
   :header-rows: 1

   * - alert
     - app
     - index
     - runtime
     - alignment
     - delay
   * - ``foo``
     - ``bar``
     - 1
     - 0
     - 1
     - 0
     
.. note:: The whitelisted checks will be considered as ✔️ in both ``Inventory`` and ``Issues`` dashboards. 

App whitelist lookup
++++++++++++++++++++

Use this lookup if you want to whitelist an entire App from being checked.

.. list-table::
   :widths: 100
   :header-rows: 1

   * - app
   * - <app name>
   
To whitelist an entire App, just add its name to the lookup.
   
.. note:: The whitelisted Apps will not be considered at all in both ``Inventory`` and ``Issues`` dashboards.
