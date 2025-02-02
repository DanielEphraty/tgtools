SSH NETCONF
===============

A low-level NETCONF manager for initiating an SSH NETCONF session with a radio and executing some RPC.
The main API is :class:`~tgtools.drivers.sshnetconf.SSHNetconf`.


.. note::
   Applications would not usually call this API directly, but rather
   through the wrapper commander :class:`~tgtools.crawl.commander.TgCommander`.

Usage Examples
----------------------

.. code-block::

   >>> from tgtools.drivers.sshnetconf import SSHNetconf
   >>> netconf = SSHNetconf('192.168.0.1', username='admin', password='admin')
   >>> netconf.connect()
   >>> response = netconf.rpc(f'<get-events xmlns="http://siklu.com/yang/tg/events"><number>1</number></get-events>')
   >>> netconf.disconnect()
  


Class Information:
------------------

.. autoclass:: tgtools.drivers.sshnetconf.SSHNetconf

