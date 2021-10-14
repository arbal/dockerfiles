
# docker build -t msoap/shell2http .

# build image
FROM golang:buster as go_builder

RUN apt-get update && apt-get install -y git

ADD . $GOPATH/src/github.com/msoap/shell2http
WORKDIR $GOPATH/src/github.com/msoap/shell2http
ENV CGO_ENABLED=0
#RUN go install -a -v -ldflags="-w -s" ./...
RUN go install -a -v -ldflags="-w -s" github.com/msoap/shell2http@latest

# final image
FROM debian:latest

COPY --from=go_builder /go/bin/shell2http /app/shell2http
ENTRYPOINT ["/app/shell2http"]
CMD ["-help"]