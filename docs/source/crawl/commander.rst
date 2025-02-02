Commander
**********

Manages the interaction with a single radio, with API :class:`tgtools.crawler.commander.TgCommander`.
Methods are provided to:

* Connect and disconnect from a radio (either IP-accessible or IP-less remote Client Node).
* Execute the *get* RPC to fetch comprehensive telemetry, and store both the raw (XML) response, as well as the parsed response.
* Execute the *get-events* RPC to fetch the latest events, and parse the output.
* Execute the *get-config* RPC to fetch one of the configuration databases.
* Execute the *run-cli-commands* RPC to send CLI commands to the radio.
* Execute the *set-system-date* and *set-system-time* RPCs to set the radio's date and time based on the computer's clock.
* Maintain a log of all errors and all configuration-affecting commands sent to the radios.

 

Usage Examples:
==================

.. code-block::
   
   >>> from tgtools import TgCommander, Credential
   >>> credential = Credential('192.168.0.1')
   >>> cmd = TgCommander(credential)
   >>> cmd.connect()
   >>> if cmd.is_connected:
   >>>     cmd.get_and_parse()
   >>>     print(f"Local radio name: {cmd.local_name}")
           Local radio name: dn1
   
   >>>     print(f"List of remote Client Nodes: {cmd.remote_cns_names}")
           Local radio name: dn1
   
   >>>     cmd.get_events_and_parse(2)
   >>>     print(cmd.events_parsed)
           Events:
	          {'route': '192.168.0.1', 'sampled': '2025-01-03 12:30:48', 'local': 'dn1', 'index': 0, 'timestamp': ' 2024-12-29 21:19:00.288', 'id': '101', 'category': 'SYSTEM', 'device': 'LOCAL', 'type': 'GPS', 'msg': 'GPS state changed from 3D to no-fix', 'power_event': '', 'link_name': '', 'link_event': '', 'up_for': '', 'cause': ''}
	          {'route': '192.168.0.1', 'sampled': '2025-01-03 12:30:48', 'local': 'dn1', 'index': 1, 'timestamp': ' 2024-12-29 21:19:01.288', 'id': '102', 'category': 'SYSTEM', 'device': 'LOCAL', 'type': 'GPS', 'msg': 'GPS state changed from no-fix to 3D', 'power_event': '', 'link_name': '', 'link_event': '', 'up_for': '', 'cause': ''}

   >>>     cmd.disconnect()



Class Information:
=====================

.. autoclass:: tgtools.crawler.commander.TgCommander




