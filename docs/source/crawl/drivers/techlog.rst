Tech-Log
=============

A driver for fetching the tech-log (internal logs) from a TG radio.

Usage Example:
--------------

.. code-block::

   >>> from tgtools import Credential, TechLog
   >>> credential = Credential('192.168.0.1', username='admin', password='admin')
   >>> t = TechLog(credential)
   >>> t.fetch('tech_log.zip')


Class Information:
------------------

.. autoclass:: tgtools.parsers.techlog.techlog.TechLog


