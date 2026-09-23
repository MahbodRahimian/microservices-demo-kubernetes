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
    -o /productcatalogservice .

FROM scratch

WORKDIR /src

COPY --from=builder /productcatalogservice ./server
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt

COPY products.json .

ENV GOTRACEBACK=single

EXPOSE 3550

ENTRYPOINT ["/src/server"]