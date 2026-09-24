FROM nexuss.mahbod.com:8082/base/golang:1.23.4-alpine AS builder

WORKDIR /src

ARG GOPROXY
ENV GOPROXY=${GOPROXY}

COPY go.mod go.sum ./

RUN go mod download

COPY . .

ARG SKAFFOLD_GO_GCFLAGS

RUN CGO_ENABLED=0 GOOS=linux \
    go build -gcflags="${SKAFFOLD_GO_GCFLAGS}" \
    -o /productcatalogservice .

FROM scratch

WORKDIR /src

COPY --from=builder /productcatalogservice ./server
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt
COPY products.json .

ENV GOTRACEBACK=single

EXPOSE 3550

ENTRYPOINT ["/src/server"]