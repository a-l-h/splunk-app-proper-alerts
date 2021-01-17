Release Notes
=============

.. list-table::
   :widths: 20 20 60
   :header-rows: 1

   * - Version
     - Date
     - Comments
   * - 1.1.5
     - 17 Jan 2021
     - | Saved searches can now be searched by type - alert or report
   * - 1.1.4
     - 12 Nov 2020
     - | Fixed whitelisting alert issue in *Inventory* dashboard
       | Fixed *IndexIsSpecified* macro
   * - 1.1.3
     - 9 Nov 2020
     - | Fixed *No action* check in *Issues* dashboard
       | Added *Close names* check in *Issues* dashboard
       | Fixed *Update KV Store lookup* query:
       |  - recipient field is set only if ``action.email`` is true
       |  - ``triggeredalerts`` is added to ``actions`` when ``alert.track`` is true
       |  - null fields are set to ``N/A`` so that MD5 hash is never empty
   * - 1.1.2
     - 8 Nov 2020
     - | Alert owner is now the owner of the knowledge object instead of the first recipient of the alert
       | Index check has been improved
       | Alerts and Apps can now be whitelisted from the checks
       | ``Notify alert recipient of a change`` has be renamed to ``Notify alert recipient of a change`` and improved
   * - 1.1.0
     - 30 Oct 2020
     - Fixed ``Notify alert owner of a change`` alert
   * - 1.0.7
     - 22 Oct 2020
     - Initial release
