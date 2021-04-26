# Docker Commands

## Basic Commands

### Starting a Container

If image is not available in local machine, it will be pulled from docker hub and then start it.
```
docker run <image_name>
```
#### In detached mode

```
docker run -d <image_name>
```
or
```
docker start <container_id>
```

### Accessing the terminal of the container

```
docker exec -it <container_id> bash
```

### Docker Images

#### List
```
docker images
```

#### Delete

```
docker rmi <image_id>
```

### Network

#### Create
```
docker network create <network_name>
```

#### List

```
docker network ls
```

### Docker Compose

#### Start

used for starting multiple services
```
docker compose -f compose-file.yaml up -d
```

- `-f` is for the file
- `up` is for starting the containers
- `-d` is to detach the terminal <br />
Docker compose also creates a network and runs the services specified in the yaml file in that network.

#### Stop
```
docker compose -f compose-file.yaml down
```

This will remove the created network.

### Dockerfile

- name of the file should be Dockerfile

#### Syntax
````
FROM <base_image>

RUN <any_linux_command>

ENV env_var=here \
    env_var=here

COPY <copy_from_or_to_container_or_host_system>

CMD ["executable", "parameter"]
````

#### Build image from docker file
```
docker build -t app:version <Dockerfile_path>
```

- `-t` is tag.
