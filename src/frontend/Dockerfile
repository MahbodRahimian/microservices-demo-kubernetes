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
    -o /go/bin/frontend .

FROM scratch

WORKDIR /src

COPY --from=builder /go/bin/frontend /src/server
COPY ./templates ./templates
COPY ./static ./static

ENV GOTRACEBACK=single

EXPOSE 8080

ENTRYPOINT ["/src/server"]