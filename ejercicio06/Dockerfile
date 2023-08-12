FROM registry.access.redhat.com/redhat-openjdk-18/openjdk18-openshift:1.15-7
COPY passwordapi.jar /app/passwordapi.jar
WORKDIR /app
CMD ["java", "-jar", "passwordapi.jar"]