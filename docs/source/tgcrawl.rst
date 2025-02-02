TgCrawl
************

Introduction
==============

**TgCrawl** is a tool to interact with multiple TG radios across a network. Interactions include:

 * Collecting and parsing comprehensive telemetry (based around the *get* RPC).
 * Collecting and parsing events (based around the *get-events* RPC).
 * Collecting configuration information (based on the *get-config* RPC)
 * Running a script of CLI commands (utilising the *run-cli-commands* RPC)
 * Setting accurate date/time (based on the computer’s clock and the *set-system-time/date* RPCs).
 * Collecting internal tech logs.

Information collected (and parsed, where applicable) is saved in txt/csv files. Errors, as well as configuration-altering commands, are logged.

**TgCrawl** can interact with both:
 
 * IP-accessible radios (have a network-accessible IP address), and
 * IP-less radios: remote Client Nodes which have no remotely-accessible IP address, (accessing these is via tunneling through their respective IP-accessible Distribution Nodes).

The precise behaviour of **TgCrawl** is fine-tuned using some ancilliary configuration text files:

#. A mandatory description of the network, listing the IP addresses of the radios, and the log-in credentials.
#. An optional (but highly recommended) parameters file, for controlling and fine-tuning the interactions with each radio.
#. If sending a script of CLI commands to the radios, then a file containing the script.

To tie this all together, a command-line launcher (``tgcrawl.py``) is provided.


.. _usage_pointer:

Usage
======

To run **TgCrawl** using the provided command-line launcher, follow these steps.

#. Run through the :doc:`installation instructions <install>`.
#. Using a standard text-editor:

   * edit the template `network file <Network file_>`_ (``network.txt``) to specify the range of IP addresses over which to search for TG radios, 
     and the credentials for logging in.
     Alternatively, create a new file and refer to it using the **-c** option of the command-line launcher.
   * edit the template `configuration file <Config file_>`_ (``config.toml``) to fine-tune the program's behaviour.
     Alternatively, create a new file and refer to it using the **-p** option of the command-line launcher.

#. Run the command-line launcher:

   .. code-block:: none

      usage: tgcrawl [-h] [-m MODE] [-n NETWORK_FILENAME] [-c CONFIG_FILENAME] [-s]

	  options:
		  -h, --help           show this help message and exit
		  -m MODE              Mode of operation (default: once). One of:
									- once: perform actions one time; 
									- poll: perform actions repeatedly;
		  -n NETWORK_FILENAME  Mandatory filename specifying the Network. Default: 'network.txt'
		  -c CONFIG_FILENAME   Optional configuration file for overriding default program parameters. Default: 'configs.toml'
		  -s                   Run in silent (rather than verbose) mode


Network file
--------------

The network, over which **TgCrawl** runs is specified as a text file, with the following format:

 * Username and password to log into the radios
 * A range of IP addresses, described by any number of the following formats (which can be mixed and matched):

    - A single IP address
    - A range of IP addresses: start and end addresses, separated by a hyphen
    - A subnet with a forward slash denoting the number of subnet bits.

.. code-block:: shell
   :caption: Example content of network file defining a total of 1 + 200 + 252 IP addresses:

   username = admin
   password = admin
   192.168.0.1
   10.11.12.1 - 10.11.12.200
   10.10.10.0/24

Further technical details available :class:`here <tgtools.utils.credentials.Credentials>`.

Config file
--------------

The configuration file (simple `TOML <https://toml.io/en/>`_  format) may be used to override
the default program parameters. For a list of these parameters and their respective
meanings, refer to the main :class:`TgCrawl API <tgtools.crawler.crawler.TgCrawler>`.

.. code-block:: shell
   :caption: Example content of configuration file:

   # Parameters for tgcrawler
	[action_scope]                  
	action_local = true                         # Action radios directly IP-accessible (listed in network file) 
	action_remote_cns = false                   # Action remote Client Nodes without remotely-accessible IP address
	action_remote_cns_list = []                 # List of specific remote Client Nodes (all, if unspecified)
	[concurrency]
	concurrency = true                          # Run concurrently (multi-thread)
	concurrency_threads = 10                    # Number of threads (do not exceed 10)
	[poller]                                    # Parameters relevant in POLL mode    
	iterations = 0                              # Number of iterations (value of zero means 'forever')
	iteration_period = 01:00:00                 # Iteration period, format: HH:MM:SS
	[get_configs]
	get_configs = false                         # Fetch configuration file and save
	get_configs_db = 'startup'                  # Type of configuration file
	get_configs_max_files = 3                   # Max number of files to retain per radio
	[get_events]
	get_events = true                           # Fetch events, parse and save
	[get_status]
	get_status = true                           # Fetch all telemetry, parse and save
	get_status_xml = false                      # Save all telemetry as raw (XML) data
	get_status_xml_max_files = 3                # Max number of files to retain per radio
	[get_tech_logs]
	get_tech_logs = false                       # Fetch tech_logs and save
	get_tech_log_max_files = 10                 # Max number of files to retain per radio
	[send_script]
	send_cmds = false                           # Send script (CLI commands)
	send_cmds_script_filename = 'script.txt'    # Script file
	[set_tod]
	set_tod = false                             # Configure radio's date and time
	set_tod_shift = 0                           # Add to computer OS clock to accommodate different timezones
	[output_files]
	dir_output_root = 'output'                  # Root directory for all output files
	dir_get_configs = 'configs'                 # Directory for saving configurations fetched from radios
	dir_get_events = 'events'                   # Directory for saving parsed events fetched from radios
	dir_get_status = 'get_status'               # Directory for saving parsed telemetry fetched from radios
	dir_get_status_xml = 'get_status_xml'       # Directory for saving raw (XML) telemetry fetched from radios
	dir_get_tech_logs = 'tech_logs'             # Directory for saving tech_logs fetched from radios
	filename_cmdlog = 'cmds_log.csv'            # Filename for saving commands sent to radios by this program 
	filename_errlog = 'errs_log.csv'            # Filename for saving errors in interaction of this program and radios
	[debug]
	debug_print = true                          # Increase console verbosity

Technical Documentation
========================

For further technical details of **TgCrawl**, refer to the :doc:`technical documentation <crawl/index>`.

