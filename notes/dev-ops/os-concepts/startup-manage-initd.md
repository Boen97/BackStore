# Startup management

[What is init.d in Linux Service Management?](https://www.geeksforgeeks.org/what-is-init-d-in-linux-service-management/)

## service command

- in linux, thera are several services that can be start and stop manully in the system
`service "service name" start/stop/status/restart`

- for example
`service ssh start` `serivce ssh status`

## what is init.d?

- `/etc/init.d`
- the `init.d` is a `daemon` which is `first process` of the linux system.
- then other processes, services are stared by init

> so `init.d` is a `configuration` database for the `init process`

- a `daemon script` holds functions like `start`, `stop`, `status`, and `restart`

`cat /etc/init.d/ssh`

## how to use init.d in service management

```
/etc/init.d/ssh start
/etc/init.d/ssh stop
```
