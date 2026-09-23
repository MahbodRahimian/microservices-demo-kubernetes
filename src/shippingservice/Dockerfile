FROM local/golang:1.23.4-alpine AS builder

ARG TARGETOS=linux
ARG TARGETARCH=amd64
ARG SKAFFOLD_GO_GCFLAGS

WORKDIR /src

COPY go.mod go.sum ./
COPY vendor ./vendor

COPY . .

RUN GOOS=${TARGETOS} \
    GOARCH=${TARGETARCH} \
    CGO_ENABLED=0 \
    go build \
    -mod=vendor \
    -gcflags="${SKAFFOLD_GO_GCFLAGS}" \
    -o /go/bin/shippingservice .

FROM scratch

WORKDIR /src

COPY --from=builder /go/bin/shippingservice /src/shippingservice

ENV APP_PORT=50051
ENV GOTRACEBACK=single

EXPOSE 50051

ENTRYPOINT ["/src/shippingservice"]