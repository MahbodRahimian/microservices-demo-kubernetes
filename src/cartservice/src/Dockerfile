FROM nexuss.mahbod.com:8082/base/dotnet-sdk:9.0.100-noble AS builder

WORKDIR /app

COPY cartservice.csproj .

RUN dotnet restore cartservice.csproj -r linux-x64

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