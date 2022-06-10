# Ex1-13

## Commands
follow these commands to set up the docker image
```
git clone https://github.com/docker-hy/material-applications.git
cp Dockerfile material-applications/example-backend/
cd material-applications/example-backend/
docker build . -t example-backend && docker run -p 8080:8080 example-backend
```

## Browser
go to [localhost:8080/ping](http://localhost:8080/ping) after following the steps above