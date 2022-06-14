# Ex2-8

## Commands
follow these commands to set up the docker image
```
git clone https://github.com/docker-hy/material-applications.git
cp <frontend Dockerfile from ex1-12> material-applications/example-frontend/
cp <backend Dockerfile from ex1-13> material-applications/example-backend/
cp <docker-compose file for this exercise> material-applications
cp <nginx.conf file for this exercise> material-applications
cd material-applications
docker-compose up
```

## Browser
go to [localhost](http://localhost/) after following the steps above to test the frontend  
go to [localhost/api/ping](http://localhost/api/ping) after following the steps above to test the backend