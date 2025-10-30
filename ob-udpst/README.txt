Below are recommended steps to run tests:-
----------------

1. Remote end (WAN) uses vanilla OB-UDPST (v8.2.0).
2. On CPE, OB-UDPST binary must always run as a client (Use -u/-d options to perform US/DS tests respectively.)
3. If testing with tunnels (e.g. PPPoE), do not use -T option.

Examples:

Server command:-

Below table shows list of commands to use for different interfaces.
+-----------+-------+------------------------------+
| Interface | proto |               cmd            |
+-----------+-------+------------------------------+
| VLAN      | IPv4  | udpst -v -j -T -p 9001       |
| PPPoE     | IPv4  | udpst -v -j -p 9001          |
| VLAN      | IPv6  | udpst -v -j -T -6 -p 9001    |
| PPPoE     | IPv6  | udpst -v -j -6 -p 9001       |
+-----------+-------+------------------------------+

CPE command:-

Sending rates must be selected based on line speed.
Below table shows list of commands for 10G line rate with different interfaces for Upstream test.
+-----------------+----------------+--------------+-------+-------------------------------------------------------+
| Base Interface1 | next interface | sending rate | proto |                          cmd                          |
+-----------------+----------------+--------------+-------+-------------------------------------------------------+
| Ethernet        |   VLAN         |     1076     | IPv4  | udpst -t 20 -I 1076 -j -T -p 9001 -u <server ip>      |
| Ethernet        |   PPPoE        |     1076     | IPv4  | udpst -t 20 -I 1076 -j -p 9001 -u  <server ip>        |
| Ethernet        |   VLAN         |     1076     | IPv6  | udpst -t 20 -I 1076 -j -T -p 9001 -6 -u < server ip>  |
| Ethernet        |   PPPoE        |     1076     | IPv6  | udpst -t 20 -I 1076 -j -p 9001 -6 -u < server ip>     |
| PON             |   VLAN         |     1063     | IPv4  | udpst -t 20 -I 1063 -j -T -p 9001 -u <server ip>      |
| PON             |   PPPoE        |     1076     | IPv4  | udpst -t 20 -I 1076 -j -p 9001 -u  <server ip>        |
| PON             |   VLAN         |     1063     | IPv6  | udpst -t 20 -I 1063 -j -T -p 9001 -6 -u < server ip>  |
| PON             |   PPPoE        |     1076     | IPv6  | udpst -t 20 -I 1063 -j -p 9001 -6 -u < server ip>     |
| Auto            |   VLAN         |       x      | IPv4  | udpst -t 20 -I  @0  -j -T -p 9001 -u < server ip>     |
| Auto            |   PPPoE        |       x      | IPv6  | udpst -t 20 -I  @0  -j -p 9001 -6 -u < server ip>     |
+-----------------+----------------+--------------+-------+-------------------------------------------------------+
NOTE: * For downstream test change -u to -d
e.g. 
udpst -t 20 -I 1076 -j -T -p 9001 -d <server ip>

Sending rates:-
----------------

User should use below commands to read sending rates:
1) udpst -j -S (tunnels).
2) udpst  -j -T -S (non-tunnels).

Compilation:-
----------------

By default 'MXL_OPT' flag is enabled for better performance.
