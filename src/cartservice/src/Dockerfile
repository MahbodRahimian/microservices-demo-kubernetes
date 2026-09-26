FROM nexuss.mahbod.com:8082/base/dotnet-sdk:9.0.100-noble AS builder

ARG HTTP_PROXY
ARG HTTPS_PROXY
ARG NO_PROXY

ENV HTTP_PROXY=${HTTP_PROXY}
ENV HTTPS_PROXY=${HTTPS_PROXY}
ENV NO_PROXY=${NO_PROXY}

WORKDIR /app

COPY cartservice.csproj .

RUN dotnet restore cartservice.csproj \
    -r linux-x64 \
    --source http://nexuss.mahbod.com:8081/repository/nuget-group/index.json

COPY . .

RUN dotnet publish cartservice.csproj \
    -p:PublishSingleFile=true \
    -r linux-x64 \
    --self-contained true \
    -p:PublishTrimmed=true \
    -p:TrimMode=full \
    -c release \
    -o /cartservice

FROM nexuss.mahbod.com:8082/base/dotnet-runtime-deps:9.0.0-noble-chiseled

WORKDIR /app

COPY --from=builder /cartservice .

EXPOSE 7070

ENV DOTNET_EnableDiagnostics=0 \
    ASPNETCORE_HTTP_PORTS=7070

USER 1000

ENTRYPOINT ["/app/cartservice"]