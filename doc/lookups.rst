Lookups
=======

This App uses 2 lookups, ``alerts_lookup`` and ``search_commands_lookup``

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
     - ooutput_command
   * - <Splunk command>
     - bool
     - bool

It is used in the :hoverxref:`indexIsSpecified<indexIsSpecified>` macro which checks if the index is specified in alerts' queries.

It is also used in the ``No action`` :hoverxref:`additional check<Additional Checks>` from the ``Issues`` dashboard which looks for alert without any configured action.

Lookup Editor App
-----------------

Both of these lookups can be edited manually effortlessly from the ``Lookups`` tab which relies on `Lookup File Editor App <https://splunkbase.splunk.com/app/1724/>`_.
