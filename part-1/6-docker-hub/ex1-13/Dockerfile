FROM golang:1.16

WORKDIR /usr/src/app

EXPOSE 8080

ENV PORT=8080
ENV REQUEST_ORIGIN="https://example.com"
ENV CERT_LOCATION=/usr/local/share/ca-certificates

COPY . .

RUN apt update
RUN apt install -y ca-certificates openssl
RUN openssl s_client -showcerts -connect github.com:443 </dev/null 2>/dev/null|openssl x509 -outform PEM > ${CERT_LOCATION}/github.crt
RUN openssl s_client -showcerts -connect proxy.golang.org:443 </dev/null 2>/dev/null|openssl x509 -outform PEM >  ${CERT_LOCATION}/proxy.golang.crt
RUN update-ca-certificates
RUN go build
RUN go test ./...

CMD ["./server", "PORT", "REQUEST_ORIGIN"]