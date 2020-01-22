# defender
A bash scripting set for blocking IPs with ufw and duplicating to other servers via http delivery. For a single-server option with no clients then you just need to install the 'server' section.

Installation
============

SERVER.

On the server a command line instruction can be used to add one or more IP addresses / subnets to be blocked, either IPv4 or IPv6.

	0. If you have amended your local ufw before.rules and before6.rules then amend the files in server/default as appropriate
	1. Copy the folder to /usr/local/share/defender
	2. Amend the webfile= locations as appropriate - they can either be IP addresses or use DNS.
		** Note this location as it will be required for the client servers
	3. Create links
		ln -s /usr/local/share/defender/def4 /usr/sbin/
		ln -s /usr/local/share/defender/def6 /usr/sbin/
		chmod +x /usr/sbin/def4
		chmod +x /usr/sbin/def6

CLIENT.

On the client machines (other servers) a cron job retrieves the updated list every hour and activates it on that machine.

	0. If you have amended this local ufw before.rules and before6.rules then either amend the files on the server's server/default as appropriate or don't use this functionality
	1. copy 'defend' to /usr/sbin and chmod +x /usr/sbin/defend
	2. amend 'importfile' and 'import6file' to the address or URL being created by the server, as above
	3. add the following line to /etc/crontab to run it hourly (adjust to suit your own preference)
		14 *    * * *   root    /usr/sbin/defend

Usage examples
==============

	To block a single IPv4 address or subnet, on the *server*:
		> def4 1.2.3.4 re
		> def4 1.2.3.4/28 re
	To block more than one address or subnet, leave off the 're' (as in 'reload'), including it only the final entry.

	To block a single IPv6 address or subnet, on the *server*:
		> def6 "0000:0000::0000" re   
		> def6 "0000:0000::0000"/60 re
	To block more than one address or subnet, leave off the 're' (as in 'reload'), including it only the final entry.
	*** Note that IPv6 addresses must be within quotation marks
	
	Adding an address already blocked isn't a problem as duplicates are automatically removed.

	If you don't wish to wait for the cron job on the client machine then just running
		> defend
	at any time will bring across the latest version. Doing so will not impact on the regular task

tl;dr option
============

Although I would recommend you add the IP addresses which are trying to attack -you- you may just install the client option and use the block lists I create for my use if you would like to; just drop me a message. I didn't include my current list in the install as, obviously, there are security considerations were I to do so.

AlisonW
