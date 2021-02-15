FROM maven:3.6.3-jdk-11 AS process-builder
COPY pom.xml /tmp/
COPY src /tmp/src/
WORKDIR /tmp
RUN mvn clean package

FROM camunda/camunda-bpm-platform:tomcat-7.14.0
ENV DB_DRIVER=org.postgresql.Driver \
	DB_URL="jdbc:postgresql://processenginedemo.cdpmv6fuwbmi.us-east-1.rds.amazonaws.com:5432/process_engine_demo?user=camunda&password=nobullshitbpm"
COPY --from=process-builder \
	/tmp/target/camundaawsdemo.war \
	/camunda/webapps/camundaawsdemo.war