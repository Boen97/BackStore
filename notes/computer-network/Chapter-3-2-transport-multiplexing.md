## MultiPlexing and Demultiplexing
- MultiPlexing
The Job of gather data chunk at the source host from different sockets, encapsulating each data chunk with header information to create segaments 
are called MultiPlexing.

jusk like the job of gather everyone's mail, and post it to post service.


- Demultiplexing

the job of delivery the data in a transport-layer segament to the correct socket are called demultiplexing.

just like the job of postman, delivey each mail to each person.

- socket identifier

each socket in the host are be assigned a port number.

in the segament header files, has source port number and destination port number, whick are be used to demultiplexing.

0 to 1023 are called well-known port numbers.

## Connectionless MultiPlexing and Demultiplexing

UDP socket are identified by desitination IP address and destination port.

UDP segament are composed by source address and desitination address.

two segaments with different source address but has the same desitination address will be delived to the same distination socket.

address are composed by id address and port number.

the source address in UDP segament are used as return address, where the server socket use it to return msg back.

## Connection-Oriented MultiPlexing and Demultiplexing

TCP socket are identified by source IP address, source port number, desitination IP address, desitination port number

## port scanning

nmap most free and popular port scanning application.

If a host is found to be running an application with a known security flaw (e.g., a SQL server listening on port 1434 was subject to a buffer overflow, allowing a remote user to execute arbitrary code on the vulnerable host, a flaw exploited by the Slammer worm [CERT 2003–04]), then that host is ripe for attack.
hacker first figout out whick port are accept TCP or UDP, and whick application are running, then use the application security flaw to attack.

the nmap are just sequentially scan ports, both TCP and UDP are sequentially scaned

## Web server and TCP

socket and process are not always one-to-one

in web server, there is only one process, and use thread to create socket for each HTTP TCP connection, which could improve the performance of the server