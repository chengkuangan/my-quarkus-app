# Base image is replaced by BuildConfig dockerStrategy.from (demo-openjdk-base:latest).
FROM scratch
USER 185
COPY deployments/ /deployments/
ENV JAVA_APP_JAR="/deployments/quarkus-run.jar"
ENV JAVA_OPTS_APPEND="-Dquarkus.http.host=0.0.0.0 -Djava.util.logging.manager=org.jboss.logmanager.LogManager"
ENV AB_JOLOKIA_OFF=""
