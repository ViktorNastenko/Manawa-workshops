
## Docker commands

### General Usage

Start a container in background

```
    $ docker un -d jenkins
```

Start an interactive container

```
    $ docker un -it ubuntu bash
```

Start a container automatically removed on stop

```
    $ docker un -rm ubuntu bash
```
Export port from a container

```
    $ docker run -p 80:80 -d nginx
```  

Start a named container
```   
    $ docker run --name mydb redis

```
Restart a stoppped container
```
    $ docker start mydb
```

Stop a container 
```
    $ docker stop mydb```
```
Add a metadata to container
```
docker run -d \
label= traefik.backend=jenkins jenkins
```

### Build Images

Build an image from Dockerfile in current directory 

``` 
    $ docker build --tag myimage .
```

Force rebuild of Docker images

```
    $ docker build --no-cache .
```

Convert a container to image 
```
    $ docker commit c7337 myimage
```

Remove all unused images
```
    $ docker mi $(docker images -q -f "dangling=true")
```

