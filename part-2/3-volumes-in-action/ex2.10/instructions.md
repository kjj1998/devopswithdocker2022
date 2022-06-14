# Ex2-10

## Commands
follow these commands to set up the docker image
```
git clone https://github.com/docker-hy/material-applications.git
cp <frontend Dockerfile from ex1-12> material-applications/example-frontend/
cp <backend Dockerfile in this exercise> material-applications/example-backend/
cp <docker-compose file for this exercise> material-applications
cd material-applications
docker-compose up
```

## Browser
go to [localhost](http://localhost/) after following the steps above to test

## Note
We need to change the ENV REQUEST_ORIGIN in the backend Dockerfile from http://localhost:5000 to http://localhost