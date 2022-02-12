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