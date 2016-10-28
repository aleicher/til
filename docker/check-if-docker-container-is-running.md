# Check if a docker container is running based on the container name

If you want to find out if a Docker container with a specific name is currently running you can use the `docker ps` command and then some `grep`, `awk`, `sed` chain.
Alternatively, you can query the [Docker Remote API](https://docs.docker.com/reference/api/docker_remote_api/) and get a JSON response which you can parse with [jq](https://stedolan.github.io/jq/).


## Using the docker remote API
```
#!/bin/sh
# filename: is_container_running.sh
# requirements: docker running locally, jq installed
# usage: ./is_container_running.sh NameOfContainer

curl -s --unix-socket /var/run/docker.sock "http:/containers/json?all=false" |\
  jq --arg containername "/$1" '[ .[].Names | .[] | . == $containername ] | reduce .[] as $item (false; . | $item)'
```

## Using grep and cut and return 0/1
```
#!/bin/sh
docker ps | grep $1 | rev | cut -d ' ' -f 1 | rev | grep -c $1
```

##Using only grep
```
#!/bin/sh
docker ps | grep $1 | grep -o '[^\ ]*$' | grep -c $1
```
##Using grep and return an exit code
e.g. if you want to process the result in another check
```
#!/bin/sh
docker ps | grep $1 | grep -o '[^\ ]*$' | grep -q $1
```

