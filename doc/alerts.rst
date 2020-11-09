Alerts
======

Notify admin for alerts to review
---------------------------------

This alert notifies Splunk admins of the count of alerts that need to be reviewed.

The idea is to enable it after the first initial review of all alerts.

This way, Splunk admins get notified of any alert to review whether new of modified.

The recipient(s) must be set and the schedule should be adjusted to your needs.

Email body contains the following message::

   There are <count> remaining alerts to review.

Notify alert recipient of a change 
------------------------------

This alert notifies the recipient of an alert of any change made on an alert is the recipient to.

The goal is to avoid any issue that could arise from unsolicited or unannounced modifications.

The recipient of this alert is the recipient of the modified alert.

.. note:: If the alert has no recipient, alert is sent to email set in ``Notify admin for alerts to review`` alert.

Email body contains the following message::

   Your alert '<alert name>' has been modified.
   Please find below what has changed - prefixed with new - within alert's main parameters.
   
It also comes with the inline table below:

.. list-table::
   :widths: 10 10 10 10 10
   :header-rows: 0
   
   * - modification date
     - alert
     - app
     - ``<field>``
     - new ``<field>``
   
.. note:: Possible ``<field>`` values: ``cron schedule``, ``earliest time``, ``latest time``, ``search``, ``actions``, ``email``,  ``owner``
 
.. attention:: 

   ``new <field>`` column comes up only if there is a new value for the said field. 
   If the ``new <field>`` value is ``N/A``, please do not consider. The column shows 
   up because there was a new value for that field in another modified alert triggered 
   at the same time.

**Search query steps:**

.. list-table::
   :widths: 5 95
   :header-rows: 0
   
   * - 1
     - Search for all enabled and scheduled alerts, then for each alert:
   * - 3
     - Add triggeredalerts` to actions if alert.track is true
   * - 4
     - Set recipient field only if action.email is true
   * - 7
     - Clean ``updated`` field
   * - 8-11
     - Set fields to N/A so that MD5 hash is never empty
   * - 12
     - Save the MD5 hash of the concatenation of :hoverxref:`main fields<Considered fields>` for later comparison
   * - 13
     - Clean ``latest_time`` field
   * - 14
     - Prefix all fields name except ``alert`` & ``app`` with ``new_`` for later comparison
   * - 16-19
     - Load KV Store lookup entries that do have an ``owner``
   * - 20
     - Group both data sets (1 & 9-12) by ``alert`` and by ``app``
   * - 21
     - Filter out results having the same MD5 hash of main fields in both data sets
   * - 24-29
     - Eval main alert fields to identify the modified ones
   * - 35-38
     - Retrieve App label
   * - 42-49
     - If email is invalid set it as set in ``Notify admin for alerts to review`` alert
   * - 51
     - Fill any ``null`` column with ``N/A``
