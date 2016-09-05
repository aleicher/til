# Stop and remove all docker containers

To stop all running docker containers, run:

`docker stop $(docker ps -a -q)`

To remove the containers:

`docker rm $(docker ps -a -q)`

To remove all images as well:

`docker rmi $(docker images -q)`
