# Golang binary building stage
FROM golang:1.14

# download the source
WORKDIR /go/src/github.com/nats-io/prometheus-nats-exporter

# build
COPY . .
RUN CGO_ENABLED=0 go build -v -a -tags netgo -installsuffix netgo -ldflags "-s -w"

# Final docker image building stage
FROM scratch
COPY --from=0 /go/src/github.com/nats-io/prometheus-nats-exporter/prometheus-nats-exporter /prometheus-nats-exporter
ENTRYPOINT ["/prometheus-nats-exporter"]
CMD ["--help"]
