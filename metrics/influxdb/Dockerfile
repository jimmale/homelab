FROM golang:alpine as builder
RUN apk update && apk upgrade --available && apk add git python binutils

RUN go get -u github.com/golang/dep/cmd/dep
RUN go get -d github.com/influxdata/influxdb

WORKDIR /go/src/github.com/influxdata/influxdb

ARG branch=master

RUN git checkout $branch

RUN python ./build.py

WORKDIR /go/src/github.com/influxdata/influxdb/build/
RUN strip -s ./*

FROM alpine:latest

RUN apk update && apk upgrade --available && rm -fr /var/cache/apk/*

COPY --from=builder /go/src/github.com/influxdata/influxdb/build/* /usr/bin/

RUN adduser -D -g '' influxdb
USER influxdb

CMD /usr/bin/influxd
