FROM alpine:latest
RUN apk update && \
    apk upgrade --available && \
    apk add cups cups-client && \
    rm -fr /var/cache/apk/*

ADD ./brhl2270dwcups_src-2.0.4-2.tar.gz / 
