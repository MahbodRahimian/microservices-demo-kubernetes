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
    -o /go/bin/frontend .

FROM scratch

WORKDIR /src

COPY --from=builder /go/bin/frontend /src/server
COPY templates ./templates
COPY static ./static

ENV GOTRACEBACK=single

EXPOSE 8080

ENTRYPOINT ["/src/server"]