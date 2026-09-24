FROM eclipse-temurin:21 AS builder

WORKDIR /app

COPY ["build.gradle", "gradlew", "./"]
COPY gradle gradle

RUN chmod +x gradlew

RUN ./gradlew downloadRepos

COPY . .

RUN chmod +x gradlew

RUN ./gradlew installDist

FROM eclipse-temurin:21-jre-alpine

WORKDIR /app

COPY --from=builder /app .

EXPOSE 9555

ENTRYPOINT ["/app/build/install/hipstershop/bin/AdService"]