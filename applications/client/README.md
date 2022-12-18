# Start go dev env

```
docker run -it -v ${PWD}:/go/src --net redis -p 80:80 golang:1.19-alpine
```

Now you can interact with go and the source code from within a docker container. cd into the src directory and run `go build`. Note, you will need to install git in order for go to pull down the packages. `apk add --no-cache git` followed by:

- go mod init example.com/hello
- go build client.go
- you may need to run manual `go get` commands for each modules

# Docker build

Now that you've used the docker container to build your applciation, you can use docker on your local machine to package it into a container image. 

```
docker build -t redis-client:v1.0.0 .
```

# Run the new Image

```
docker run -it --net redis \
  -e REDIS_HOST=redis \
  -e REDIS_PORT=6379 \
  -e REDIS_PASSWORD="foobarred" \
  -p 80:80 \
  redis-client:v1.0.0
```

```
# single liner, same command as above

docker run -it --net redis -e REDIS_HOST=redis -e REDIS_PORT=6379 -e REDIS_PASSWORD="foobarred" -p 80:80 redis-client:v1.0.0
```

