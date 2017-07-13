# Show the total number of docker images available locally

`$ docker images|cut -c 70-90|grep -v 'IMAGE ID' |sort|uniq|wc -l`
