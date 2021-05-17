# Docker Commands

## Basic Commands

### Docker Container

#### Start

If image is not available in local machine, it will be pulled from docker hub and then start it.
```
docker run --name <container_name> \
-p <host_port>:<container_port> \
--network <some_network> \
-e env_var=here \
-e env_var=here \
<image_name>
```
In detached mode,
```
docker run -d <image_name>
```

or (if container already exists)
```
docker start <container_id>
```

#### Accessing the terminal of the container
```
docker exec -it <container_id> bash
```

#### List 

- Running containers,
```
docker ps
```

- All containers,
```
docker ps -a
```

#### Stop
```
docker stop <container_id>
```

#### Remove
```
docker rm <container_id>
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

#### Syntax of compose yaml file
```
version: "<version_of_compose>"

services:
  <name_of_container>:
    image: <image_name>
    ports:
      - <host_port>:<container_port>
    environment:
      - env_var=here
      - env_var=here
    volumes:
      - <name>:<container_path>
      - <name>:<container_path>
 
  <name_of_container>:
    image: <image_name>
    ports:
      - <host_port>:<container_port>
    environment:
      - env_var=here
      - env_var=here
    volumes:
      - <name>:<container_path>
      - <name>:<container_path>
volumes:
  - <name_of_volume>
```

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

This will remove the created network and the container(s).

### Dockerfile

- name of the file should be Dockerfile

#### Syntax
````
FROM <base_image>

RUN <any_linux_command>

ENV env_var=here \
    env_var=here

COPY <copy_from_or_to_container_or_to_host_system>

CMD ["executable", "parameter"]
````

#### Build image from Dockerfile
```
docker build -t app:version <Dockerfile_path>
```

- `-t` is tag

### Docker Volumes

#### Create

This can be done in three ways.

1. Host volumes

```
docker run -v <host_path>:<container_path>
```

The data will be saved into the directory specified by `host_path`

2. Anonymous volumes

```
docker run -v <container_path>
```

The data will be saved into the directory specified by `/var/lib/docker/volumes/random_hash/_data`

3. Named volumes

```
docker run -v <name>:<container_path>
```

The data will be saved into the directory specified by `/var/lib/docker/volumes/random_hash/_data`

(use this in production)

The location of docker volumes in windows using WSL2 is `\\wsl$\docker-desktop-data\version-pack-data\community\docker\volumes\`
