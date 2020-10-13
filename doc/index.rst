.. this is a comment, it is not rendered
   when adding new *.rst files, reference them here
   in this index.rst for them to be rendered and added to the
   table of contents
   
Welcome to the Proper Alerts App documentation
==============================================

Maintaining properly configured alerts is not an easy task in Splunk.

Is the search properly structured? Is data source still being indexed? Are search time and schedule coordinated? What if the runtime is longer than the interval between two occurrences of the same alert?

You probably answered these questions while doing the once in a while alert review which is alright.

But this task becomes a pain in no time when the number of alerts rises and it is not rare to see an environment in which Splunk admins lost track of configured alerts with consequences such as alerts being missed and improper resources usage.

A more efficient way to keep track of configured alerts would consists in reviewing them all once, and then only review the ones that have changed since the last review. This the purpose of this App: help Splunk admins to continuously maintain properly configured alerts.

App Purposes
============

- test
- ok


Index
=====

.. toctree::
   :maxdepth: 2

   overview.rst
   install.rst
   dashboards.rst
   alerts.rst
