Batch Engine
********************

The batch engine provides the following functionality:

#. Attempt to log-in to each IP address in a network, and identify it as a TG radio. Where successful:
#. Execute the *get* RPC and parse the results. This includes obtaining a list of remote Client-Nodes which may not have an IP address.
#. Perform one or more interactions with the radio, parsing and saving the results.
#. If so configured, tunnel into the remote IP-less Client Nodes and repeat the interactions.
#. Repeat for the next IP address
#. Excute all above once, or automatically repeat multiple times every specified time period.


The main API is :class:`~tgtools.crawler.batch.TgCrawler`. A typical usage would be to instantiate the class (with all parameters are arguments), and then
run :meth:`~tgtools.crawler.batch.TgCrawler.batch_run` for single network sweep; or :meth:`~tgtools.crawler.batch.TgCrawler.poll_run` for polling mode,
indicating the iteration period and number of iterations.

The batch engine typically connects to several radios concurrently utilising multi-threading. The number of threads should not exceed 10, as this is the maximum number
of tunnels currently supported by the TG radios. It is possible to run the batch engine sequentially, but this is much slower (typically used for debugging only).

The interaction with each radio is managed as an instance of a 'commander' (:class:`~tgtools.crawler.commander.TgCommander`). Outputs are then saved
to files in a thread-safe way.

Class Information:
=======================

.. autoclass:: tgtools.crawler.batch.TgCrawler


