FROM eclipse-temurin:17-jdk AS build

WORKDIR /app

COPY gradlew .
COPY gradle ./gradle

RUN chmod +x gradlew

COPY . .

RUN ./gradlew clean build --no-daemon

FROM eclipse-temurin:17-jre

WORKDIR /app

# Copy only the shadow JAR (avoids multiple-match COPY error)
COPY --from=build /app/build/libs/linkie-web-backend.jar app.jar

EXPOSE 6969

ENTRYPOINT ["java", "-jar", "app.jar"]
