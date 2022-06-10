# Securing TCP Connections: TLS

> this `enhanced version of TCP` is commonly known as `Transport Layer Security (TLS)`
> an earlier and similar version of this protocol is `SSL version 3`

- Since its inception, SSL and its successor TLS have enjoyed broad deployment
- TLS is supported by all popular Web browsers and Web servers

> You can identify that `TLS` is being used by your browser when the URL begins with `https`: rather than http.

## understand the `need` for `TLS`

- If `no confidentiality (encryption)` is used, an intruder could intercept Bob’s order and obtain his payment card information. 
- if `no data integrity is used`, an intruder could modify Bob's order
- if `no server authentication is used`, a server could display Alice Incorporated’s famous logo 
- when in actuality the site maintained by Trudy, who is masquerading as Alice Incorporated. 

> TLS addresses these issues by enhancing `TCP` with `confidentiality, data integrity, server authentication and client authentication`

> TLS is often used to provide `security` to transactions that take place over `HTTP`
> however, because TLS secures TCP, it can be employed by any application that runs over `TCP`
> TLS provides a simple `API` with `sockets`, which is similar and analogous to `TCP's API`

> when an application wants to employ `TLS`, the application includes `SSL classes/libraries`
