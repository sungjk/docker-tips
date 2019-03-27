# docker-tips
My 🐳 Docker CLI Tips and Tricks

# Containers
### Starting and Stopping
- `docker start` starts a container so it is running.
- `docker stop` stops a running container.
- `docker restart` stops and starts a container.
- `docker pause` pauses a running container, "freezing" it in place.
- `docker unpause` will unpause a running container.
- `docker wait` blocks until running container stops.
- `docker kill` sends a SIGKILL to a running container.
- `docker attach` will connect to a running container.

### CPU Constraints
The setting is a bit strange -- 1024 means 100% of the CPU, so if you want the container to take 50% of all CPU cores, you should specify 512
```
docker run -it -c 512 agileek/cpuset-test
```

# Volumes

### Lifecycle
```
$ docker volume create
$ docker volume rm
```

### Info
```
$ docker volume ls
$ docker volume inspect
```

# Exposing ports
Mapping the container port to the host port (only using localhost interface) using -p:
```
$ docker run -p 127.0.0.1:$HOSTPORT:$CONTAINERPORT --name CONTAINER -t someimage
```

Listens on the specified network ports at runtime by using EXPOSE:
```
$ EXPOSE <CONTAINERPORT>
```

To expose the container's port on your localhost's port:
```
$ iptables -t nat -A DOCKER -p tcp --dport <LOCALHOSTPORT> -j DNAT --to-destination <CONTAINERIP>:<PORT>
```

If you forget what you mapped the port to on the host container, use docker port to show it:
```
$ docker port CONTAINER $CONTAINERPORT
```

# References
- [Docker Reference documentation](https://docs.docker.com/reference/)
- [Docker Cheat Sheet](https://github.com/wsargent/docker-cheat-sheet)
- Personal experience
