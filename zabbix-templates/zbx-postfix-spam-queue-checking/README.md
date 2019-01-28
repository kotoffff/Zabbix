ZBX-POSTFIX-SPAM-QUEUE-CHECKING
===========

This template for Postfix queue checking: 
 * 1. Number of letters 
 * 2.'blocked' letters (SPAM checking)

Items
-----

  * queue.block  - number of letters in queue
  * queue.status - number of 'blocked'(SPAM) letters in queue

Triggers
--------

* **[WARNING]** => too many letters in queue last 30 minutes
* **[WARNING]** => when find 'blocked' (SPAM) letters in queue

Installation
------------
1. Please add below user parameteres on monitoring mail Postfix server:
   UserParameter=queue.status,postqueue -p | grep -v "^[^0-9A-Z]\|^$" | wc -l
   UserParameter=queue.block,postqueue -p | grep blocked | wc -l
2. Associate **ZBX-POSTFIX-SPAM-QUEUE-CHECKING** template to the host.


### Requirements

This template was tested for Zabbix 3.4 and higher.

License
-------

These templates were distributed under the terms of the GNU General Public License as published by the Free Software Foundation; either version 2 of the License, or (at your option) any later version.

### Copyright

  Copyright (c) Sergey Kotov

### Authors

  Sergey Kotov
  (kotoffff |at| gmail |dot| com)
