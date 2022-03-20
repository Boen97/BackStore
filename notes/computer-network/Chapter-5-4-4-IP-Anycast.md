## IP-Anycast

in addition to being the Internet's inter-AS routing protocal
BGP is often used to implement the IP-anycast service, which is commonly used in DNS

1. replicating the same content on different servers in many different locations
2. having each user access the content from the server that is closest.

> in pratise, CDNs generally choose not to use IP-anycast because BGP routing changes can resulting in different packets of the same TCP connection arriving at
> different instances of the web server.

> But IP-anycast is extensively used by the DNS system to direct DNS query to the cloest root DNS server.
