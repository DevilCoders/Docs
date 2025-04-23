Buld docker image:

ya package pkg.json
sudo docker build -t mrc-tasks-planner:0.1 - < yandex-maps-mrc-tasks-planner.0.0.1-1.tar.gz

# Now we have image in locat Docker repo 'mrc-tasks-planner' with tag 0.1

=============================================
Run docker image:

> sudo docker run -d -p 8380:80 mrc-tasks-planner:0.1  # Run sa daemon
> sudo docker run -i -p 8380:80 mrc-tasks-planner:0.1  # Run interactively
> sudo docker run -it -p 8380:80 mrc-tasks-planner:0.1 bash # Run with shell

How to attach to running Docker:

> sudo docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
e8db6b017e25        meta:0.1            "/bin/sh -c 'yacare e"   3 minutes ago       Up 3 minutes        0.0.0.0:8380->80/tcp   small_knuth

> sudo docker exec -it e8db6b017e25 bash  # Replace e8db6b017e25 with real container id from previous command

How to kill running container
> sudo docker kill e8db6b017e25 # Replace e8db6b017e25 with real container id from previous command

=============================================

Docker daemon should be run on machine (regulus.dev.cloud.maps.yandex.net for example)
=============================================
