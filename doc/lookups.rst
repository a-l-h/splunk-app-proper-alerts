Lookups
=======

This App uses 2 lookups, ``alerts_lookup`` and ``search_commands_lookup``

``alert_lookup`` is the KV Store lookup that store the state of active alerts.

It has the following fields:

.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Field
     - Type
   * - actions
     - string
   * - alert
     - string
   * - app
     - string
   * - app_label
     - string
   * - cron_schedule
     - string
   * - dataSourceExist
     - bool
   * - dateLastReview
     - number
   * - description
     - string
   * - earliest_time
     - string
   * - email
     - string
   * - hasOwner
     - bool
   * - hasServiceRequest
     - bool
   * - indexIsSpecified
     - bool
   * - interval
     - number
   * - latest_time
     - string
   * - md5
     - string
   * - md5_search
     - string
   * - owner
     - string
   * - reviewer
     - string
   * - run_time
     - number
   * - runtimeIsLowerThanInterval
     - bool
   * - scheduleHasAtLeastOneMinuteDelay
     - bool
   * - search
     - string
   * - searchIsCorrectlyStructured
     - bool
   * - searchPeriodIsAlignedWithSchedule
     - bool
   * - service_request
     - string
   * - updated
     - number

``search_commands_lookup`` is the lookup that store splunk search commands.

It is used in the ``indexIsSpecified`` macro that check if the index is specified in alerts' queries.

It is also used ``Issues`` dashboard additional check ``No action`` that looks for alert wothout configured action.

Lookup Editeor App

Trough the ``Lookups`` tab, you can edit both of these lookups in a convenient way using Lookup Editor app.

