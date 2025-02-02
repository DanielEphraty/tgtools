TgCrawl
***********

TgCrawl is a program for interacting with TG radios across a network, and is introduced :doc:`here <../tgcrawl>`.

It comprises:

#. A :doc:`command-line launcher <launcher>` for collating the program configuration (IP addresses, parameters, etc.) and invoking the batch engine.
#. A :doc:`batch engine <batch>` for crawling over a network (multiple radios), performing certain interactions with each radio.
   Information collected (telemtry, retrieved files, ...) is saved to csv/txt files. Interactions with a each radio is managed through a *commander*.
#. A :doc:`commander <commander>` for managing the interaction with a single radio. The commander employs several :doc:`drivers <drivers>` (implementing
   the actual communication with the radio), and :doc:`parsers <parsers>` for extracting useful information.

.. toctree::
   :maxdepth: 2
   :hidden:
   
   launcher
   batch
   commander
   drivers
   parsers
   