FROM nexuss.mahbod.com:8082/base/golang:1.23.4-alpine AS builder

WORKDIR /src

COPY go.mod go.sum ./

RUN go mod download

COPY . .

ARG SKAFFOLD_GO_GCFLAGS

RUN CGO_ENABLED=0 GOOS=linux \
    go build -gcflags="${SKAFFOLD_GO_GCFLAGS}" \
    -o /checkoutservice .

FROM scratch

WORKDIR /src

COPY --from=builder /checkoutservice /src/checkoutservice

ENV GOTRACEBACK=single

EXPOSE 5050

ENTRYPOINT ["/src/checkoutservice"]