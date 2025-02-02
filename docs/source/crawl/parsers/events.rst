Events Parser
==============================
Classes :class:`~tgtools.parsers.events.event.Event` and :class:`~tgtools.parsers.events.events.Events` work together to parse radio events
and append to a csv file.

Usage Examples
----------------------

.. code-block::
   :caption: Parsing the output of the **get-events** RPC into list of parsed events
   
   >>> from pathlib import Path
   >>> from tgtools.parsers.event import Event
   >>> xml = ''' <rpc-reply xmlns="urn:ietf:params:xml:ns:netconf:base:1.0"
                            xmlns:nc="urn:ietf:params:xml:ns:netconf:base:1.0"
                            message-id="urn:uuid:fb6a10dc-1097-4e6d-8cb7-7524fc94d327">
	                 <events xmlns="http://siklu.com/yang/tg/events">
		                 <index>0</index>
		                 <event>2024-10-13 23:31:03.784, 1388,SYSTEM, LOCAL,  RADIO,   cn1 link up; Local/Remote Sector: 3/1; Tx/Rx Beam: 32/32; Tx/Rx Az: 20/20 deg; Tx/Rx El: -10/-10 deg</event>
  	                 </events>
	                 <events xmlns="http://siklu.com/yang/tg/events">
		                 <index>1</index>
		                 <event>2024-10-13 23:56:02.304, 1389,SYSTEM, LOCAL,  RADIO,   cn1 link down (was up for 00000:00:24:58); Cause: LinkNegotiationFailed; Local/Remote Sector: 3/1</event>
	                 </events>
                 </rpc-reply>
             '''
	>>> prefix_dict = {'route'='192.168.0.1', 'sampled':'2024-10-23 17:09:00'}
	>>> events = Events.from_xml(xml, prefix_dict)
	>>> print(events)
		Events:
			{'route': '192.168.0.1', 'sampled': '2024-10-23 17:09:00', 'index': 0, 'timestamp': ' 2024-10-13 23:31:03.784', 'id': '1388', 'category': 'SYSTEM', 'device': 'LOCAL', 'type': 'RADIO', 'msg': 'cn1 link up; Local/Remote Sector: 3/1; Tx/Rx Beam: 32/32; Tx/Rx Az: 20/20 deg; Tx/Rx El: -10/-10 deg', 'power_event': '', 'link_name': 'cn1', 'link_event': 'link up', 'up_for': '', 'cause': ''}
			{'route': '192.168.0.1', 'sampled': '2024-10-23 17:09:00', 'index': 1, 'timestamp': ' 2024-10-13 23:56:02.304', 'id': '1389', 'category': 'SYSTEM', 'device': 'LOCAL', 'type': 'RADIO', 'msg': 'cn2 link down (was up for 00000:00:24:58); Cause: LinkNegotiationFailed; Local/Remote Sector: 3/1', 'power_event': '', 'link_name': 'cn2', 'link_event': 'link down', 'up_for': '00000:00:24:58', 'cause': 'LinkNegotiationFailed'}
	>>> events.append_csv(Path('events.csv'))
  
  

Class Information:
------------------

.. autoclass:: tgtools.parsers.events.events.Events

.. autoclass:: tgtools.parsers.events.event.Event


