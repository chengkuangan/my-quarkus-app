# Base image is replaced by BuildConfig dockerStrategy.from (demo-openjdk-base:latest).
FROM scratch
USER 0
# Entire /deployments tree from demo-app:latest (layout varies by how S2I assembled it).
COPY deployments/ /tmp/in/
RUN set -eux; \
    mkdir -p /deployments; \
    if [ -f /tmp/in/quarkus-run.jar ]; then \
      cp -a /tmp/in/quarkus-run.jar /deployments/; \
      [ -d /tmp/in/app ] && cp -a /tmp/in/app /deployments/; \
      [ -d /tmp/in/lib ] && cp -a /tmp/in/lib /deployments/; \
      [ -d /tmp/in/quarkus ] && cp -a /tmp/in/quarkus /deployments/; \
    elif [ -f /tmp/in/target/quarkus-app/quarkus-run.jar ]; then \
      cp -a /tmp/in/target/quarkus-app/. /deployments/; \
    else \
      echo "ERROR: quarkus-run.jar not found in /deployments or /deployments/target/quarkus-app"; \
      find /tmp/in -name 'quarkus-run.jar' 2>/dev/null || true; \
      exit 1; \
    fi; \
    chown -R 185:0 /deployments
USER 185
ENV JAVA_APP_JAR="/deployments/quarkus-run.jar"
ENV JAVA_OPTS_APPEND="-Dquarkus.http.host=0.0.0.0 -Djava.util.logging.manager=org.jboss.logmanager.LogManager"
ENV AB_JOLOKIA_OFF=""
