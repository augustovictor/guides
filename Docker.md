# Docker

## Glossary
- **Image**: The application we want to run
	- The app binaries and dependencies;
	- Metadata about the image data and how to run it;
	- Structure: `user/repository`
- **Image layers**: 
- **Container**: Instance of that image running as a process
	- **Immutable**: The infrastructur does not change! If any change has to be made then a whole new container should be deployed.
	- **Ephemeral**:
	- **Data Volumes**: Configuration option for a container that creates a new location outside the container Union File System to store unique data. This preserves the data and allows us to attach it to any container we want.
	- **Bind mounts**: Link the container path to the host path.
- **Image registry**: Images repository. E.g., dockerHub
- **Dockerfile**: Recipe to create an image;
- **Docker compose**: Combination of the command line tool and a configuration file;
	- **YAML** file: Specification of the containers that we need to run, network, volumes, env variables, images, etc;
	- **CLI tool** `docker-compose`: Local dev and test automation with **YAML** files;

## Commands
Command | Description
---|---
`docker ps -s` | Info about the container disk usage
`docker system df [-v]` | Docker disk usage
`docker pull alpine` | Just download an image
`docker container run --publish 80:80 --detach --name webhost nginx` | Run in background
`docker container run -it alpine sh` | Like 'bash' of ubuntu. `apk` is the pkg manager
`docker container run -d --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=true -v mysql:/var/lib/mysqlmysql` | Start a mysql container with empty password and named volume `mysql`
`docker container -it` | Start new container iteractively
`docker container exec -it` | Run additional command in **existing** container
`docker container exec -it nginx bash` | Run a new bash process inside `nginx` container
`docker container run --rm -it --name centOs centos:7` | Run container in `it` mode and remove it after exiting;
`docker container ls` | List running containers
`docker container logs -f webhost` | Live logs of `webhost` container
`docker container top webhost` | The process running inside the container
`docker container inspect webhost` | Container details
`docker container stats` | Performance stats for all containers
`docker container -f <CONTAINER_ID>` | Force remove a container
`docker container stop webhost` | Stop container
`docker start webhost` | Start a stopped container
`docker container start -ai ubuntu` | Start again a container iteractively
`docker container port webhost` | Open ports of `webhost` container
`docker container inspect --format '{{ .NetworkSettings.IPAddress }}' webhost` | Ip which the container is running
`docker network ls` | List the networks
`docket network inspect` | Inspect networks
`docker network create <NET_NAME> [--driver]` | Create a network.
`docket network connect <NETWORK_ID> <CONTAINER_ID>` | Atach a network to a container
`docket network disconnect` | Detach a network from container
`docker container run -d --name new_nginx --net my_app_net nginx` | New nginx container using the new network
`--net-alias <NAME>` | Network alias
`docker container run --rm --net net_test alpine nslookup search` | Lookup for servers under an alias
`docker container run --rm --net net_test centos curl -s search:9200` | Request from centos to the servers running under the alias search on port 9200
`docker history mysql` | History of changes to `mysql` image in dockerhub
`docker image tag nginx victor/nginx[:TAG]` | Renamge `nginx` TAG to `victor/nginx`
`docker image push victor/nginx` | Uploads changed layers to an image registry (dockerhub is default)
`docker login` | Login
`docker logout` | Logout (Do it to delete the stored keychain)
`docker image build -t customName .` | Build image from Dockerfile with a custom name in the current dir
`docker volume prune` | Clean unused volumes
`docker container run -d --name webhost -p 80:80 -v $(pwd):/usr/src/app node` | Link current directory with container files
`docker-compose up [--build]` | Setup volumes/networks and start all containers
`docker-compose down [-v][--rmi [local|all]]` | Stop all containers and remove cont/vol/net/image
`docker-compose ps` | List running containers
`docker-compose build` | Rebuild in case anything changed in an image



## Observations
- Containers are just processes limited to what they can access;
- `80:80`: Open port `80` on host and forward to port `80` in container;
- When listing networks: `docker0` == `bridge`(default);
- When creating a network the `bridge` is the defautlt driver used;
- DNS Round Robin test: More than one server responding to the same DNS.
- Rename image to `user/image_name` before pushing to dockerhub;
- Volumes need a manual deletion.

## Best practices
- Create a virtual network for each app without needing to use `-p`:
	- network `my_web_app` for mysql and php/apache containers. No need to open ports to phisical network to make these two apps talk to each other;
	- network `my_api` for mongo and nodejs containers;
- Use DNS to name container IPs; IPs are dynamic;
- Separations of concerns: The binary application and the persistent data should not be in the same container.
- Use Bind Mounts for local development and testing. It will mount the changes in the host machine into the container.
- Do not use `docker-compose` CLI in production;


## Dockerfile format
```sh
FROM
RUN
CMD
```

## Docker-compose file format
```YAML
version:: '3.1' # V1 is the default. V2 is the minimum recommended

services: # Containers. Same as docker run
	servicename: # Friendly name that is also the DNS name inside network
		image: # Optional if you use build:
		ports: # Optional
		command: # Optional. Replace the original CMD specified by the image
		environment: # Optional. Same as -e in docker run
		volumes: # Optional. Same as docker -v in docker run
	servicename2: # ...

volumes: # Optional. Same as docker volume create
networks: # Optional. Same as docker network create
```

## Example: drupal and postgres docker-compose.yml
```YAML
version: '2'

services:
    drupal:
        image: drupal:latest
        ports:
            - "8080:80"
        volumes:
            - drupal-modules:/var/www/html/modules
            - drupal-profiles:/var/www/html/profiles
            - drupal-sites:/var/www/html/sites
            - drupal-themes:/var/www/html/themes
    postgres:
        image: postgres:9.6.2
        # No need to specify ports because we'll use the default 5432. And both containers will run in the same network.
        environment:
            - POSTGRES_PASSWORD=root123
        volumes:
            - pg-db:/var/lib/postgresql/data

volumes:
    drupal-modules:
    drupal-profiles:
    drupal-sites:
    drupal-themes:
    pg-db:
```

## Example: nginx and webserver
**nginx.conf**

```conf
server {
    listen 80;

    location / {
        proxy_pass        http://web;
        proxy_redirect    off;
        proxy_set_header  Host $host;
        proxy_set_header  X-Real-IP $remote_addr;
        proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header  X-Forwarded-Host $server_name;
    }
}
```

**nginx.Dockerfile**

```YAML
FROM nginx:latest

COPY nginx.conf /etc/nginx/conf.d/default.conf
```

**docker-composer.yml**

```YAML
version: '2'

services:
    proxy:
        build:
            context: .
            dockerfile: nginx.Dockerfile
        image: nginx-custom # Optional. To remove a docker-compose buld along withe its images use: 'docker-compose down --rmi local' and do not specify this name attribute
        ports:
            - '80:80'
    web:
        image: httpd
        volumes:
            - ./html:/usr/local/apache2/htdocs
```