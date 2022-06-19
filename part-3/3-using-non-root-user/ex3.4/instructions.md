# Ex3-4

## Commands
follow these commands to set up the docker image
```
git clone https://github.com/docker-hy/material-applications.git
cp <Dockerfile-frontend from this directory> material-applications/example-frontend/
cd material-applications/example-frontend/ && mv Dockerfile-frontend Dockerfile && cd ../..
cp <Dockerfile-backend from this directory> material-applications/example-backend/
cd material-applications/example-backend/ && mv Dockerfile-backend Dockerfile && cd ../..
cp <docker-compose file from this directory> material-applications
cd material-applications
docker-compose up
```

## Browser
go to [localhost:5000](http://localhost:5000/) after following the steps above to test