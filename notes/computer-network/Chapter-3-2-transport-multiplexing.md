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