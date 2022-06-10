# Ex1-12

## Commands
follow these commands to set up the docker image
```
git clone https://github.com/docker-hy/material-applications.git
cp Dockerfile material-applications/example-frontend/
cd material-applications/example-frontend/
docker build . -t example-frontend && docker run -p 5000:5000 example-frontend
```

## Browser
go to [localhost:5000](http://localhost:5000/) after following the steps above