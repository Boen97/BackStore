### The container's filesystem

- when a container runs, it uses the various layers from an image for its filesystem.
- each container can also get its own scratch space to create/remove/udpate files.
- any changes won't be seen in another container, even if they are using the same image.

- Example.
1. `docker run -d ubuntu bash -c "shuff -i 1-10000 -n 1 -o /data.txt && tail -f /dev/null"`
   - starting a bash shell and invoking two commands
   1. picks a single random number and writes it to data.txt
   2. watching a file to keep the container running.

2. `exec`ing the container, to see the output
   `docker exec <container-id> cat /data.txt`

3. start another container
   `docker run -it ubuntu ls /`

### Container volumes.

> volumns provide the ability to connect specific filesystem paths of the container back to the host machine.
> If a directory in the container is mounted, changes in that directory are also seen on the host machine.
> If we mount the same directory across container restarts, we'd see the same files.

- they are two main types of volumes. we start with names volumes.

#### named volume.
> Think of a named volume as simply a bucket of data.
> Docker maintains the physical location on the disk and you only need to remember the name of the volume.

- create a volume by using the `docker volume create` command.
  `docker volume create todo-db`
- start the app with a volume
  `docker run -dp 3000:3000 -v todo-db:/etc/todos getting-started`
  - `-v` flag to specify a volume amount.
  - we will use the named volume and mount it to `/etc/todos`, which will capature all files created at the path.
  
> while named volumes and bind mountes are the two main types of volumes supported by a default docker engine installation,
> these are many volume driver plugins avaliable to support NFS, SFTP, NetApp, and more!
> This will be especially important once you start running containers on multiple hosts in a clustered environment with Swarm, Kubernates, etc.

#### dive into the volume.
> Where is Docker actually storeing my data when I use named volume.
`docker volume inspect todo-db`
- The `Mountpoint` is the actual location on the disk where data is stored.

> rebuilding images for every changes takes quite a bit of time.
> There is a better way to make changes.
