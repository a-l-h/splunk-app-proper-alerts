Macros
======

indexIsSpecified
----------------

This macro is used in ``Update KV Store lookup`` report to perform the :hoverxref:`Index automatic check<Index>`

It looks through the ``qualifiedSearch`` field of each alert to find if an index is specified in the query.

While sounding simple at first, several usescases has to be covered:

+ subsearches
+ macros
+ eventypes
+ alternative search commands

As a result, the underlying query handles:

+ up to 2 levels of macros
+ up to 2 levels of eventtypes
+ alternative search commands via the ``search_commands_lookup``

This latter case is simple, if the search is not a classic ``index=foo`` search, then index is not required.

While it still is a good practice to precise the index using alernate commands such as mstats, the initial goal is to spot uneficient search queries within alerts, so mainly classic searches.

If you use a scripted command in an alert query and it is spooted as not having index specified, add your script command to the ``search_commands_lookup`` and give the value ``classic_search = 0``

getServiceRequest
-----------------

This macro is used in ``Update KV Store lookup`` report to perform extract the service request from alert's description field.

This a common practice to add service request reference(s) to alert's description.

Having service request could be useful when investigating an alert from the inventory dashboard as a way to quiclky find context, requesstor or any interesting details before doing any chnages


maxConcurrentSavedSearches
--------------------------

This macro is used in the ``Concurrency`` dashboard to retrieve the maximum number of concurent saved searches that can be run.
