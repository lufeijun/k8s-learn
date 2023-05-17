FROM golang AS builder

LABEL stage=gobuilder

ENV CGO_ENABLED 0
ENV GOPROXY https://goproxy.cn,direct


WORKDIR /build

ADD go.mod .
ADD go.sum .
RUN go mod download
COPY . .
COPY demo/etc /app/etc
RUN go build -ldflags="-s -w" -o /app/demo demo/demo.go


WORKDIR /app
CMD ["./demo", "-f", "etc/demo-api.yaml"]