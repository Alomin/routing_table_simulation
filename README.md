routing_table_simulation
========================
All the file below you d better put them in the home directory of your computer, or you type the full path of it, like: DV_Simulation.py ,you should type /User/ryan/Desktop/hw3/DV_Simulation.py
1.get the localip of all the computer you want to use. I have a little python program for you:
python getmyip.py
or you can get the ip in your own way, but here i only support the ip in a LAN. Espesially
you are in a NAT, don’t try computer in different LAN. 
For integrity, 127.0.0.1 is not supported, you will have to use the LAN ip add instead
you ll get like 192.168.1.105

2.initialize like this
for your convenience, here is all the cmd.
ip1 ip2 ip3 ip4 ip5 for 4115~4119 seperately, don’t forget to fill the ip with the ip you get above
python DV_Simulation.py 4115 10
python DV_Simulation.py 4116 10 ip1 4115 5
python DV_Simulation.py 4117 10 ip2 4116 10
python DV_Simulation.py 4118 10 ip2 4116 5 ip1 4115 30
python DV_Simulation.py 4119 10 ip3 4117 6
you are free to add redundant neighbor not exist at all, program discard them after timeout*3.

3.test:
I handle the goes to infinity by set the link cost to infi when cost>99, don’t try cost>99, or maybe a path cost>99. if you want to. open my file and find the infi variable.
very large infi is handled.
here all the cmd below don’t show the infinity link and infinity destination.
because I think that will make the DVtable keep growing, all the infi link are deleted. Except the LINKDOWN cmd, a copy is saved for LINKUP.
Start the program
(wait for a little while like up to 5sec or you can set a shorter timeout of remote to speed up)
SHOWRT
LINKDOWN IP PORT （no colon please!make sure the addr you entered is in neighbor）
SHOWRT
LINKUP IP PORT
SHOWRT
CLOSE
(wait until timeout*3 the link will disappear on remote)
SHOWRT
you will see the DVtable change with your cmd.
4.OPTIONAL:
extra1:change the weight of exist link.
UPDATE IP PORT WEIGHT:

extra2:build a link within two (addr,ip) running this program. Also you can link to a no exist addr,it will timeout*3 and delete. The link exist in current link or link has been LINKDOWN by you are not premitted, simply return “wrong cmd”
NEWLINK IP PORT WEIGHT:

extra3:the infi I ignore is not really invisible if you really want to see. Just open my file and find “infi = 99”, change 99 to a larger number like 100000, Then try to LINKDOWN, you d better type SHOWRT fast several times, you will see the routing table increasing.
it’s easy to make this process visible, but that’s flooding, you really don’t want to see it.

5.protocol including syntax and semantics: I used a self-made json protocol… it’s a table with key value pairs. “”stands for str.{}table,[]list,()tuple,”,” for separate.
If you want to see the flying packet, if left a print(pkt) in this program. Uncomment, and  wait for being flooded every timeout period.

Distributed Bellman-Ford algorithm
