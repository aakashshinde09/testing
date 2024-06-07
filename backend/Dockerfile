# Use Ubuntu as base image
FROM tomcat

# Copy the Maven project directory into the container
COPY . /opt

# Set the working directory in the container
WORKDIR /opt/spring-backend

# Install dependencies
RUN apt update && \
    apt install openjdk-11-jdk -y && \
    apt install maven -y

RUN export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64 && \
    export PATH=$JAVA_HOME/bin:$PATH
    
# Use sed to modify the database configuration in application.properties
RUN sed -i 's/spring.datasource.url=jdbc:mysql:\/\/localhost:3306\/springbackend?useSSL=false/spring.datasource.url=jdbc:mysql:\/\/database-1.ch2eco4q2tci.us-east-1.rds.amazonaws.com:3306\/springbackend?useSSL=false/' /opt/spring-backend/src/main/resources/application.properties && \
    sed -i 's/spring.datasource.username=springbackend/spring.datasource.username=admin/' /opt/spring-backend/src/main/resources/application.properties && \
    sed -i 's/spring.datasource.password=springbackend/spring.datasource.password=akash1234/' /opt/spring-backend/src/main/resources/application.properties && \
    
    echo 'server.port=8085' >> /opt/spring-backend/src/main/resources/application.properties




# Build the Maven project
RUN mvn clean package -Dmaven.test.skip=true

# Expose the port the application runs on
EXPOSE 8085

# Command to run the application
CMD ["java", "-jar", "target/spring-backend-v1.jar"]