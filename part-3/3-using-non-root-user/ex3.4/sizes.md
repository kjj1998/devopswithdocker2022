# Optimizing Image Sizes

## Frontend

```
FROM ubuntu:18.04

WORKDIR /usr/src/app

ENV REACT_APP_BACKEND_URL="http://localhost:8080"

COPY . .

EXPOSE 5000

RUN apt update
RUN apt install -y curl
RUN curl -sL https://deb.nodesource.com/setup_16.x | bash
RUN apt install -y nodejs
RUN echo $(node -v)
RUN echo $(npm -v)
RUN npm install
RUN npm run build
RUN npm install -g serve
RUN useradd -m userapp
RUN chown userapp /usr/src/app

USER userapp

CMD ["serve", "-s", "-l", "5000", "build"]
```

Size: 599 MB

```
FROM ubuntu:18.04

WORKDIR /usr/src/app

# To connect to the backend as required in Ex1.14
ENV REACT_APP_BACKEND_URL="http://localhost:8080"

COPY . .

EXPOSE 5000

RUN apt update && apt install -y curl && \ 
    curl -L https://deb.nodesource.com/setup_16.x | bash - && \
    apt install -y nodejs && \
    npm install && \
    npm run build && \ 
    npm install -g serve && \ 
    useradd -m userapp && \ 
    chown userapp /usr/src/app

USER userapp

CMD ["serve", "-s", "-l", "5000", "build"]
```

Size: 597 MB

```
FROM ubuntu:18.04

WORKDIR /usr/src/app

# To connect to the backend as required in Ex1.14
ENV REACT_APP_BACKEND_URL="http://localhost:8080"

COPY . .

EXPOSE 5000

RUN apt update && apt install -y curl ca-certificates && \ 
    curl -L https://deb.nodesource.com/setup_16.x | bash - && \
    apt install -y nodejs && \
    npm install && \
    npm run build && \ 
    npm install -g serve && \
    apt-get purge -y --auto-remove curl && \
    rm -rf /var/lib/apt/lists/* && \ 
    useradd -m userapp && \ 
    chown userapp /usr/src/app

USER userapp

CMD ["serve", "-s", "-l", "5000", "build"]
```

Size: 552 MB

## Backend
```
FROM golang:1.16

WORKDIR /usr/src/app

EXPOSE 8080

ENV PORT=8080
ENV CERT_LOCATION=/usr/local/share/ca-certificates

# CORS whitelisted url to communicate with the frontend as required in ex 1.14
ENV REQUEST_ORIGIN="http://localhost:5000"

COPY . .

RUN apt update
RUN apt install -y ca-certificates openssl
RUN openssl s_client -showcerts -connect github.com:443 </dev/null 2>/dev/null|openssl x509 -outform PEM > ${CERT_LOCATION}/github.crt
RUN openssl s_client -showcerts -connect proxy.golang.org:443 </dev/null 2>/dev/null|openssl x509 -outform PEM >  ${CERT_LOCATION}/proxy.golang.crt
RUN update-ca-certificates
RUN go build
RUN go test ./...
RUN useradd -m appuser
RUN chown appuser /usr/src/app

USER appuser

CMD ["./server", "PORT", "REQUEST_ORIGIN"]
```

Size: 1.09GB

```
FROM golang:1.16

WORKDIR /usr/src/app

EXPOSE 8080

ENV PORT=8080
ENV CERT_LOCATION=/usr/local/share/ca-certificates

# CORS whitelisted url to communicate with the frontend as required in ex 1.14
ENV REQUEST_ORIGIN="http://localhost:5000"

COPY . .

RUN apt update && apt install -y ca-certificates openssl && \
    openssl s_client -showcerts -connect github.com:443 </dev/null 2>/dev/null|openssl x509 -outform PEM > ${CERT_LOCATION}/github.crt && \
    openssl s_client -showcerts -connect proxy.golang.org:443 </dev/null 2>/dev/null|openssl x509 -outform PEM >  ${CERT_LOCATION}/proxy.golang.crt && \
    update-ca-certificates && \
    go build && \
    go test ./... && \
    useradd -m appuser && \
    chown appuser /usr/src/app

USER appuser

CMD ["./server", "PORT", "REQUEST_ORIGIN"]
```

Size: 1.09 GB

```
FROM golang:1.16

WORKDIR /usr/src/app

EXPOSE 8080

ENV PORT=8080
ENV CERT_LOCATION=/usr/local/share/ca-certificates

# CORS whitelisted url to communicate with the frontend as required in ex 1.14
ENV REQUEST_ORIGIN="http://localhost:5000"

COPY . .

RUN apt update && apt install -y ca-certificates openssl && \
    openssl s_client -showcerts -connect github.com:443 </dev/null 2>/dev/null|openssl x509 -outform PEM > ${CERT_LOCATION}/github.crt && \
    openssl s_client -showcerts -connect proxy.golang.org:443 </dev/null 2>/dev/null|openssl x509 -outform PEM >  ${CERT_LOCATION}/proxy.golang.crt && \
    update-ca-certificates && \
    go build && \
    go test ./... && \
    apt-get purge -y --auto-remove openssl && \
    rm -rf /var/lib/apt/lists/* && \ 
    useradd -m appuser && \
    chown appuser /usr/src/app

USER appuser

CMD ["./server", "PORT", "REQUEST_ORIGIN"]
```

Size: 1.07 GB