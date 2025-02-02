Command Line Launcher
**********************

The command-line launcher ``tgcrawl.py``:

* Retrieves any command-line arguments
* Sets default values for all parameters which fine-tune the program's operation. 
* Optionally reads a configuration TOML file to override the default values of these parameters
* Reads a network descriptor text file which provides the range of IP addresses (over which to *crawl*), as well as log-in credentials for the radios.
* Calls the batch engine main API: :class:`~tgtools.crawler.batch.TgCrawler`.




Module Information
==================

.. automodule:: tgtools.tgcrawl

