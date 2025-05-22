
FROM eclipse-temurin:21-jdk AS builder

WORKDIR /usr/app/

COPY build.gradle* settings.gradle* gradlew .
COPY ./gradle ./gradle

RUN chmod +x ./gradlew
RUN ./gradlew
RUN ./gradlew downloadRepos

COPY . .
COPY ./pb ./proto

RUN ./gradlew installDist -PprotoSourceDir=./proto

FROM eclipse-temurin:21-jre AS release
WORKDIR /usr/app/

COPY --from=builder /usr/app/ ./
ENV AD_PORT=9099
ENTRYPOINT ["./build/install/opentelemetry-demo-ad/bin/Ad"]
