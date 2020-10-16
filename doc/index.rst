Proper Alerts App Documentation
===============================

Maintaining properly configured alerts is not an easy task in Splunk.

Is the search properly structured? Is data source still being indexed? Are search time and schedule coordinated? What if the runtime is longer than the interval between two occurrences of the same alert?

You probably answered these questions while doing the once in a while alert review.

This task however, becomes a pain in no time when the number of alerts rises and, as a consultant, it is common to see a Splunk environment in which admins lost track of configured alerts with consequences such as alerts being missed and improper resources usage.

A more efficient way to keep track of active alerts would consist in reviewing them all once, and then only review the ones that have been modified since the last review.

This the purpose of this App: help Splunk admins to continuously maintain properly configured alerts.

To do so, the App leverages Splunk KV Store to save active alerts in a lookup that gets updated every time an alert is modified. The lookup is then loaded in an interactive dashboard that lets Splunk admins review alerts.


Topics
======

.. toctree::
   :maxdepth: 2

   overview.rst
   install.rst
   usage.rst
   dashboards.rst
   alerts.rst
   macros.rst
   release_notes.rst
   support.rst
