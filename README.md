# defender
A bash scripting set for blocking IPs with http delivery.

On the server a command line instruction can be used to add one or more IP addresses / subnets to be blocked, either IPv4 or IPv6.

On the client machines (other servers) a cron job retrieves the updated list every hour and activates it on that machine.

AlisonW
