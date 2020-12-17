FROM golang:latest as builder
WORKDIR /workspace
ENV GOPROXY="https:goproxy.io"
ENV  GOSUMDB="off"
ENV  CGO_ENABLED=0
ENV GOOS=linux
ENV GO111MOUDLE=on
WORKDIR /workspace
COPY go.mod  /workspace
COPY go.sum  /workspace
COPY main.go /workspace
RUN go mod download && go build -a -o workflow  /workspace/main.go
FROM alpine as final
COPY --from=builder /workspace/workflow .
EXPOSE  8080
ENTRYPOINT ["./workflow"]