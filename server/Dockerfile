FROM golang:1.18-alpine as builder

WORKDIR /my-gin-admin/server
COPY . .

RUN go env -w GO111MODULE=on \
    && go env -w GOPROXY=https://goproxy.cn,direct \
    && go env -w CGO_ENABLED=0 \
    && go env \
    && go mod tidy \
    && go build -o server .

FROM alpine:latest

LABEL MAINTAINER="867235241@qq.com"

WORKDIR /my-gin-admin/server

COPY --from=0 /my-gin-admin/server ./
COPY --from=0 /my-gin-admin/server ./resource/
COPY --from=0 /my-gin-admin/server/config.docker.yaml ./

EXPOSE 8888
ENTRYPOINT ./server -c config.docker.yaml
