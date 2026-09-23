FROM --platform=$BUILDPLATFORM local-golang:1.23.4-alpine AS builder

ARG TARGETOS
ARG TARGETARCH
ARG SKAFFOLD_GO_GCFLAGS

WORKDIR /src

COPY go.mod go.sum ./

RUN --mount=type=cache,target=/go/pkg/mod \
    go mod download

COPY . .

RUN --mount=type=cache,target=/go/pkg/mod \
    --mount=type=cache,target=/root/.cache/go-build \
    GOOS=${TARGETOS} \
    GOARCH=${TARGETARCH} \
    CGO_ENABLED=0 \
    go build \
    -gcflags="${SKAFFOLD_GO_GCFLAGS}" \
    -o /go/bin/shippingservice .

FROM scratch

WORKDIR /src

COPY --from=builder /go/bin/shippingservice /src/server

ENV GOTRACEBACK=single

EXPOSE 50051

ENTRYPOINT ["/src/server"]