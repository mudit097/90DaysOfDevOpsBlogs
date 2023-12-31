---
title: "Day 20 Docker CheatSheet"
datePublished: Wed Aug 16 2023 20:48:58 GMT+0000 (Coordinated Universal Time)
cuid: clle7gpie000109mmcmq3fca4
slug: day-20-docker-cheatsheet
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692218737522/1923567b-0263-4a0d-85f1-eea3ebf4c652.png
tags: ubuntu, docker, aws, devops, 90daysofdevops

---

# **Container Management CLIs**

![](https://miro.medium.com/v2/resize:fit:875/0*wxIwUKubVAa8V8o3.png align="center")

# **Inspecting The Container**

![](https://miro.medium.com/v2/resize:fit:875/0*t_5fRfbXa-B2lMtd.png align="center")

# **Interacting with Container**

![](https://miro.medium.com/v2/resize:fit:875/0*0GGU8k1s3kAncHGo.png align="center")

# **Image Management Commands**

![](https://miro.medium.com/v2/resize:fit:875/0*d6sdX-L2FAZVM8Yj.png align="left")

# **Image Transfer Commands**

![](https://miro.medium.com/v2/resize:fit:875/0*TaY-meNaUbV9Wsk5.png align="left")

# **Builder Main Commands**

![](https://miro.medium.com/v2/resize:fit:875/0*MFN3mZWgdVjoHSDX.png align="left")

# **The Docker CLI**

## **Manage imagesdocker build**

`docker build`

```plaintext
docker build [options] .
  -t "app/container_name"    # name
```

Create an `image` from a Dockerfile.

`docker run`

```plaintext
docker run [options] IMAGE
  # see `docker create` for options
```

Run a command in an `image`.

# **Manage containers**

`docker create`

```plaintext
docker create [options] IMAGE
  -a, --attach               # attach stdout/err
  -i, --interactive          # attach stdin (interactive)
  -t, --tty                  # pseudo-tty
      --name NAME            # name your image
  -p, --publish 5000:5000    # port map
      --expose 5432          # expose a port to linked containers
  -P, --publish-all          # publish all ports
      --link container:alias # linking
  -v, --volume `pwd`:/app    # mount (absolute paths needed)
  -e, --env NAME=hello       # env vars
```

# **Example**

```plaintext
$ docker create --name app_redis_1 \
  --expose 6379 \
  redis:3.0.2
```

Create a `container` from an `image`.

`docker exec`

```plaintext
docker exec [options] CONTAINER COMMAND
  -d, --detach        # run in background
  -i, --interactive   # stdin
  -t, --tty           # interactive
```

# **Example**

```plaintext
$ docker exec app_web_1 tail logs/development.log
$ docker exec -t -i app_web_1 rails c
```

Run commands in a `container`.

`docker start`

```plaintext
docker start [options] CONTAINER
  -a, --attach        # attach stdout/err
  -i, --interactive   # attach stdin
docker stop [options] CONTAINER
```

Start/stop a `container`.

`docker ps`

```plaintext
$ docker ps
$ docker ps -a
$ docker kill $ID
```

Manage `container`s using ps/kill.

# **Images**

`docker images`

```plaintext
$ docker images
  REPOSITORY   TAG        ID
  ubuntu       12.10      b750fe78269d
  me/myapp     latest     7b2431a8d968
$ docker images -a   # also show intermediate
```

Manages `images`.

`docker rmi`

```plaintext
docker rmi b750fe78269d
```

Deletes `image`s.

# **Also, see**

* [Getting Started](http://www.docker.io/gettingstarted/) *(*[*docker.io*](http://docker.io)*)*
    

# **Dockerfile**

## **Inheritance**

```plaintext
FROM ruby:2.2.2
```

# **Variables**

```plaintext
ENV APP_HOME /myapp
RUN mkdir $APP_HOME
```

# **Initialization**

```plaintext
RUN bundle install
WORKDIR /myapp
VOLUME ["/data"]
# Specification for mount point
ADD file.xyz /file.xyz
COPY --chown=user:group host_file.xyz /path/container_file.xyz
```

# **Onbuild**

```plaintext
ONBUILD RUN bundle install
# when used with another file
```

# **Commands**

```plaintext
EXPOSE 5900
CMD    ["bundle", "exec", "rails", "server"]
```

# **Entrypoint**

```plaintext
ENTRYPOINT ["executable", "param1", "param2"]
ENTRYPOINT command param1 param2
```

Configures a container that will run as an executable.

```plaintext
ENTRYPOINT exec top -b
```

This will use shell processing to substitute shell variables, and will ignore any `CMD` or `docker run` command line arguments.

# **Metadata**

```plaintext
LABEL version="1.0"
LABEL "com.example.vendor"="ACME Incorporated"
LABEL com.example.label-with-value="foo"
LABEL description="This text illustrates \
that label-values can span multiple lines."
```

# **See also**

* [https://docs.docker.com/engine/reference/builder/](https://docs.docker.com/engine/reference/builder/)
    

# **docker-compose**

# **Basic example**

```plaintext
# docker-compose.yml
version: '2'services:
  web:
    build: .
    # build from Dockerfile
    context: ./Path
    dockerfile: Dockerfile
    ports:
     - "5000:5000"
    volumes:
     - .:/code
  redis:
    image: redis
```

# **Commands**

```plaintext
docker-compose start
docker-compose stop
docker-compose pause
docker-compose unpause
docker-compose ps
docker-compose up
docker-compose down
```

# **Reference**

# **Building**

```plaintext
web:
  # build from Dockerfile
  build: .
# build from custom Dockerfile
  build:
    context: ./dir
    dockerfile: Dockerfile.dev
# build from image
  image: ubuntu
  image: ubuntu:14.04
  image: tutum/influxdb
  image: example-registry:4000/postgresql
  image: a4bc65fd
```

# **Ports**

```plaintext
ports:
    - "3000"
    - "8000:80"  # guest:host
# expose ports to linked services (not to host)
  expose: ["3000"]
```

# **Commands**

```plaintext
# command to execute
  command: bundle exec thin -p 3000
  command: [bundle, exec, thin, -p, 3000]
# override the entrypoint
  entrypoint: /app/start.sh
  entrypoint: [php, -d, vendor/bin/phpunit]
```

# **Environment variables**

```plaintext
# environment vars
  environment:
    RACK_ENV: development
  environment:
    - RACK_ENV=development
# environment vars from file
  env_file: .env
  env_file: [.env, .development.env]
```

# **Dependencies**

```plaintext
# makes the `db` service available as the hostname `database`
  # (implies depends_on)
  links:
    - db:database
    - redis
# make sure `db` is alive before starting
  depends_on:
    - db
```

# **Other options**

```plaintext
# make this service extend another
  extends:
    file: common.yml  # optional
    service: webapp
volumes:
    - /var/lib/mysql
    - ./_data:/var/lib/mysql
```

# **Advanced features**

# **Labels**

```plaintext
services:
  web:
    labels:
      com.example.description: "Accounting web app"
```

# **DNS servers**

```plaintext
services:
  web:
    dns: 8.8.8.8
    dns:
      - 8.8.8.8
      - 8.8.4.4
```

# **Devices**

```plaintext
services:
  web:
    devices:
    - "/dev/ttyUSB0:/dev/ttyUSB0"
```

# **External links**

```plaintext
services:
  web:
    external_links:
      - redis_1
      - project_db_1:mysql
```

# **Hosts**

```plaintext
services:
  web:
    extra_hosts:
      - "somehost:192.168.1.100"
```

# **sevices**

To view list of all the services runnning in swarm

```plaintext
docker service ls
```

To see all running services

```plaintext
docker stack services stack_name
```

to see all services logs

```plaintext
docker service logs stack_name service_name
```

To scale services quickly across qualified node

```plaintext
docker service scale stack_name_service_name=replicas
```

# **clean up**

To clean or prune unused (dangling) images

```plaintext
docker image prune
```

To remove all images which are not in use containers, add — a

```plaintext
docker image prune -a
```

To Purne your entire system

```plaintext
docker system prune
```

To leave swarm

```plaintext
docker swarm leave
```

To remove swarm ( deletes all volume data and database info)

```plaintext
docker stack rm stack_name
```

To kill all running containers

```plaintext
docker kill $(docker ps -q )
```

Reach me out for any queries …

LinkedIn: [https://www.linkedin.com/in/mudit--mathur/](https://www.linkedin.com/in/mudit--mathur/)

Signing of … Thanks a lot for going through the post