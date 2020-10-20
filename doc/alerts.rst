Alerts
======

Notify admin for alerts to review
---------------------------------

This alert notifies Splunk admins of the count of alerts that need to be reviewed.

The idea is to enable it after the first initial review of all alerts.

This way, Splunk admins get notified of any alert to review whether new of modified.

The recipient(s) must be set and the schedule should be adjusted to your needs.

Notify alert owner of a change 
------------------------------

This alert notifies the owner of an alert of any change made on an alert he owns.

The goal is to avoid any issue that could arise from unsolicited or unannounced modifications.

The recipient of this alert is the recipient of the modified alert.

If the alert has no recipient, alert is sent to email set in ``Notify admin for alerts to review`` alert.

**Search query steps:**

.. list-table::
   :widths: 20 80
   :header-rows: 1
   
   * - Lines
     - Description
   * - 1
     - Search for all enabled and scheduled alerts, then for each alert:
   * - 4
     - Clean ``updated`` field
   * - 5
     - Save the MD5 hash of the concatenation of :hoverxref:`main fields<Considered fields>` for later comparison
   * - 6
     - Prefix all fields name except ``alert`` & ``app`` with ``new_`` for later comparison
   * - 8-11
     - Load KV Store lookup entries that do have an ``owner``
   * - 12
     - Group both data sets (1 & 8-11) by ``alert`` and by ``app``
   * - 13
     - Filter out results having the same MD5 hash of main fields in both data sets
   * - 16-21
     - Eval main alert fields to identify the modified ones
   * - 27-30
     - Retrieve App label
   * - 34-39
     - If email is invalid set it as set in ``Notify admin for alerts to review`` alert
