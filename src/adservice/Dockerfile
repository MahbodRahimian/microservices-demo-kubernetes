FROM local/eclipse-temurin:24.0.2-jdk-noble AS builder

WORKDIR /app

COPY build.gradle gradlew ./

COPY gradle gradle

RUN chmod +x gradlew

RUN ./gradlew downloadRepos

COPY . .

RUN chmod +x gradlew

RUN ./gradlew installDist

FROM local/eclipse-temurin:24.0.2-jre-alpine

WORKDIR /app

COPY --from=builder /app .

EXPOSE 9555

ENTRYPOINT ["/app/build/install/hipstershop/bin/AdService"]