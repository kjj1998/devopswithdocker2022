# Ex1-11

## Commands
follow these commands to set up the docker image
```
git clone https://github.com/docker-hy/material-applications.git
cp Dockerfile material-applications/spring-example-project/
cd material-applications/spring-example-project/
docker build . -t spring-project && docker run -p 8080:8080 spring-project
```

## Browser
go to [localhost:8080](http://localhost:8080/) after following the steps above