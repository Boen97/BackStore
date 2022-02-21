### why need Flow Control in TCP connection.

- each side of a TCP connection set aside a receive buffer for the connection, the associated application will read data from this buffer, but may not in time
- if the application is slow reading the data in the buffer, the buffer is very easy to overflow by sending to much data.
- so we need flow control in TCP.

