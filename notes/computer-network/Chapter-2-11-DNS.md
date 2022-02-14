## DNS the Internet's Directory Service
就像现实世界中我们每个人都拥有自己的身份标识一样，在互联网中Host也拥有自己的身份标识
而在不同的场景下不同的身份标识有不同的功能，有的标识对人友好，有的标识对机器友好

- Hostname
  www.google.com
  nice to people, but not to router or machince
- IP address
  nice to machince, and has hierarchical structure, could provide more specific location information in the Internet

- DNS (Domain name system)
  translate hostnames to IP addresses
  - a distributed database
  - a application layer protocal, use UDP, run on port 53
  - allow user to query the database
  
- The services provided by DNS
  1. translate hostname to IP addresses
  2. Host Alias
  - alias canonical hostname
  3. Mail Server Alias
  - alias mail server hostname
  - use MX record, mail server and web server could be identical alias hostname
  4. Load distribution
  - for replicated servers
  - a set of ip addreses alias to one hostname
  
> the much of complexity in the Internet is located in the edges of the Internet
> DNS is a example

- How DNS works
  1. All DNS query and replay message are send within UDP on port 53
- Why DNS design in distributed
  1. single point of failure
  2. traffic volume
  3. distant centralized database
  4. maintenance
> DNS is a example of a distributed database implemented in the Internet

- Three classed of DNS servers
1. root DNS servers
2. top-level domain(TLD) servers
3. authoritative servers

Local DNS

> a proxy of local client to request DNS service
for example:
1. request www.amazon.com
2. request local DNS server
3. local DNS server request root dns get the IP address of TLD servers for www
4. then reqeust TLD server to get the id addresses of authoritative servers

- recursive query and iterative query
  1. recursive query
     client -> local dns server
     local dns server -> root dns server
     local dns server -> TLD dns server
     local dns server -> authoritative dns server
     local dns server -> client
 2. iterative query
    client -> local dns server
    local dns server -> root dns server
    root dns server -> TLD dns server
    TLD dns server -> authoritative server
    authoritative server -> TLD dns server
    TLD dns server -> root dns server
    ...

- DNS Caching
1. the mapping between ip addressed and hostname are cached
2. the expired time of the cache are often 2 days
3. the ip addresses of TLD servers are also cached, so bypass the root dns server

- DNS Records and Messages

1. RRs(resource records)
(Name, Value, Type, TTL)
    1. Type = A
       mapping of hostname and ip address
    2. Type = NS
       Name = domain(foo.com)
       Value = authoritative DNS server
    3. Type = CNAME
       Name = hostname alias
       Value = canonical hostname
    4. Type = MX
       Name = email hostname alias
       Value = email canonical hostname
       
- DNS Messages
  1. just like HTTP request and response messages
  2. DNS request and reply messages has the same format
  Format
  1. Header section
     - identification
     - Flags
       - recursive desired flag
       - authoritative flag
       ...
  2. Question section
     request hostname and resource type
  3. Answers section
     response RRs
  4. Authority section
     records of other authoritative servers
  5. Additional information
     
 - nslookup program
   send dns query message directly to dns server

- Insert Records into the DNS Database
1. first register a hostname, such as networkutopia.com
2. provide the register the name and ip addresses of your primary and secondary authoritative dns servers
   such as dns1.networkutopia.com and dns2.networkutopia.com, with ip address 212.2.212.1 and 212.2.212.2
3. insert a NS record and A record into TLD servers
4. insert MX record for mail server alias

> more recently, UPDATE option has been added to the DNS protocal, which alow data to be dynamic added or deleted from database via dns messages
     
