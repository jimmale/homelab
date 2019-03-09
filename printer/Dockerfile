FROM alpine:latest
RUN apk update && \
    apk upgrade --available && \
    apk add cups cups-client && \
    rm -fr /var/cache/apk/*
