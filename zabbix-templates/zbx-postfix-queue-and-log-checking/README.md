ZBX-POSTFIX-QUEUE-AND-LOG-SPAM-CHECKING
===========

This template for Postfix queue checking: 
-  Number of letters 
-  'blocked' letters (SPAM checking)

This template for Postfix maillog checking:
-  'blocked' letters (SPAM checking)

Items
-----

  * queue.status -  number of letters in queue
  * queue.blocked - number of 'blocked'(SPAM) letters in queue 
  * maillog.blocked - number of 'blocked'(SPAM) letters in maillog last hour

Triggers
--------

* **[WARNING]** => too many letters in queue last 30 minutes
* **[WARNING]** => when find 'blocked' (SPAM) letters in queue
* **[WARNING]** => when find 'blocked' (SPAM) letters in maillog

Installation
------------
1. Please add below user parameteres on monitored mail Postfix server:
```
   UserParameter=queue.status,postqueue -p | grep -v "^[^0-9A-Z]\|^$" | wc -l
   UserParameter=queue.block,postqueue -p | grep -e blocked -e blacklisted | wc -l
   UserParameter=maillog.blocked,journalctl -u postfix -S "$(date -d "-1 hour" +%Y"-"%m"-"%d" "%T)" | grep  -iw -e  blacklisted -e blocked | wc -l
```
2. Please add Zabbix user to systemd-journal group:
```
  usermod -G systemd-journal zabbix
```
3. Please associate **ZBX-POSTFIX-QUEUE-AND-LOG-SPAM-CHECKING** template to the host.


### Requirements

-This template was tested for Zabbix 3.4 and higher.
-This template was tested for Posfix 2.10 and higher.
-This template was tested for CentOS 7.X.

License
-------

These templates were distributed under the terms of the GNU General Public License as published by the Free Software Foundation; either version 2 of the License, or (at your option) any later version.

### Copyright

  Copyright (c) Sergey Kotov

### Authors

  Sergey Kotov
  (kotoffff |at| gmail |dot| com)
