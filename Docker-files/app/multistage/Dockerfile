# ---------- Build Stage ----------
FROM maven:3.9.9-eclipse-temurin-21-jammy AS build_image

# Clone your actual repository
RUN git clone https://github.com/tilaknagulla/actionprofile.git

# Build the project
WORKDIR /actionprofile
RUN mvn clean install -DskipTests

# ---------- Runtime Stage ----------
FROM tomcat:10-jdk21

# Clean default ROOT app
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy WAR from build stage
COPY --from=build_image /actionprofile/target/*.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
