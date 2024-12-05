FROM maven AS build
RUN mkdir /opt/wapp1
WORKDIR /opt/wapp1
COPY . .
CMD mvn clean install


FROM tomcat
WORKDIR webapps
COPY --from=build /opt/wapp1/target/mywebapp-3.1.war .
RUN rm -rf ROOT && mv mywebapp-3.1.war ROOT.war
EXPOSE 8080
