
### Viewing Infos

```bash
docker version # Base infos for version
docker info # More informations about Docker
docker # Long list of available commands (not all)
```

### Running Containers (old Way)

- Creating a new container
```bash
docker container run --publish 80:80 --detach --name "name-container" nginx 
```
- ***"docker container run"*** is the old way to run a container
- ***"--publish"*** expose the port outside the container
- ***"--detach"*** runs the container in background

> [!info]
> Every time you run this command, it will create a new instance with a different ID.

- View a list of instances on the system
- *It will show all the instances existent (running or not)*
```bash
docker container ls -a
```

- View the logs of detached containers
```bash
docker container logs
```

- Remove containers from the system
```bash
docker container rm -f xxx # or multiple containers 
```

- Start or stop a container
```bash
docker container start name-container
docker container stop name-container
```

- View running processes on the container
```bash
docker container top name-container
```

### Getting Shell into Containers

```bash
docker container run -it --name "name-container" nginx bash
#or
docker container exec -it "name-container" bash
```