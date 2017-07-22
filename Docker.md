# Docker

## Glossary
- **Image**: The application we want to run
	- The app binaries and dependencies;
	- Metadata about the image data and how to run it;
- **Image layers**: 
- **Container**: Instance of that image running as a process
- **Image registry**: Images repository. E.g., dockerHub

## Commands
Command | Description
---|---
`docker pull alpine` | Just download an image
`docker container run --publish 80:80 --detach --name webhost nginx` | Run in background
`docker container run -it alpine sh` | Like 'bash' of ubuntu. `apk` is the pkg manager
`docker container -it` | Start new container iteractively
`docker container exec -it` | Run additional command in **existing** container
`docker container exec -it nginx bash` | Run a new bash process inside `nginx` container
`docker container run --rm -it --name centOs centos:7` | Run container in `it` mode and remove it after exiting;
`docker container ls` | List running containers
`docker container logs webhost` | Logs of `webhost` container
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


## Observations
- Containers are just processes limited to what they can access;
- `80:80`: Open port `80` on host and forward to port `80` in container;
- When listing networks: `docker0` == `bridge`(default);
- When creating a network the `bridge` is the defautlt driver used;
- DNS Round Robin test: More than one server responding to the same DNS.

## Best practices
- Create a virtual network for each app without needing to use `-p`:
	- network `my_web_app` for mysql and php/apache containers. No need to open ports to phisical network to make these two apps talk to each other;
	- network `my_api` for mongo and nodejs containers;
- Use DNS to name container IPs; IPs are dynamic;