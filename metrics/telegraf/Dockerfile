FROM golang:alpine as builder
RUN apk update && apk upgrade --available && apk add git make

RUN go get -u github.com/golang/dep/cmd/dep
RUN go get -d github.com/influxdata/telegraf

WORKDIR /go/src/github.com/influxdata/telegraf

ARG branch=master

RUN git checkout $branch

ENV LDFLAGS="-w -s"
ENV CGO_ENABLED=0
RUN make

FROM alpine:latest

RUN apk update && apk upgrade --available && rm -fr /var/cache/apk/*

COPY --from=builder /go/src/github.com/influxdata/telegraf/telegraf /usr/bin/telegraf

RUN adduser -D -g '' telegraf
USER telegraf

CMD /usr/bin/telegraf
