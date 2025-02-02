Credentials: login details
=============================

``credentials.py`` implements two classes for managing radio login credentials:

 * :class:`~tgtools.utils.credentials.Credential` representing a single set of credentials
   (IP address, username, password).
 * :class:`~tgtools.utils.credentials.Credentials` representing a sequence of
   (one or more) :class:`~tgtools.credentials.Credential`.


Usage Examples:
----------------------

.. code-block::
   :caption: Contents of 'list_ip_addresses.txt'
   
   username = user
   password = passw
   192.168.0.0/28
 
.. code-block:: 
   :caption: Code example
   
   >>> from pathlib import Path
   >>> from tgtools.utils.credentials import Credentials
   >>> creds = Credentials.from_file(Path('temp.txt'))
   >>> for batch in creds.get_batches(5):
           print(batch)
   
   5 Credentials: from 192.168.0.1 to 192.168.0.5
   5 Credentials: from 192.168.0.6 to 192.168.0.10
   4 Credentials: from 192.168.0.11 to 192.168.0.14
   
   >>> print(creds[-1])
   Credential(192.168.0.14, 'user', 'passw')


Class Information:
------------------

.. autoclass:: tgtools.utils.credentials.Credentials

.. autoclass:: tgtools.utils.credentials.Credential



