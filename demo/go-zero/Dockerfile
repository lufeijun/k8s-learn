FROM golang AS builder

LABEL stage=gobuilder

ENV CGO_ENABLED 0
ENV GOPROXY https://goproxy.cn,direct


WORKDIR /build

ADD go.mod .
ADD go.sum .
RUN go mod download
COPY . .
#COPY demo/etc /app/etc
RUN go build -ldflags="-s -w" -o /app/demo demo/demo.go


FROM scratch

COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt
COPY --from=builder /usr/share/zoneinfo/Asia/Shanghai /usr/share/zoneinfo/Asia/Shanghai
ENV TZ Asia/Shanghai

WORKDIR /app
COPY --from=builder /app/demo /app/demo
#COPY --from=builder /app/etc /app/etc

CMD ["./demo", "-f", "etc/demo-api.yaml"]