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


