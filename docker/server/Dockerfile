FROM maven:3.3-jdk-8 as build
COPY /docker/server/conf/settings.xml /usr/share/maven/conf/
WORKDIR /src
COPY pom.xml /src
COPY /src /src/src
RUN mvn install:install-file -Dfile=src/main/resources/WEB-INF/lib/jave-1.0.2.jar -DgroupId=lt.jave -DartifactId=jave -Dversion=1.0.2 -Dpackaging=jar
RUN mvn install:install-file -Dfile=src/main/resources/WEB-INF/lib/ip2region-1.2.4.jar -DgroupId=org.lionsoul.ip2region -DartifactId=ip2region -Dversion=1.2.4 -Dpackaging=jar
RUN mvn compile
RUN mvn package --Dmaven.test.skip=true

FROM openjdk as final
WORKDIR /app
COPY --from=build /src/target /app

COPY --from=build /src/target /dist
#ENTRYPOINT java -Xms1240m -Xmx1240m -Xmn450m -XX:PermSize=512M -XX:MaxPermSize=512m -XX:+UseParNewGC -XX:+UseConcMarkSweepGC -XX:+UseTLAB -XX:NewSize=128m -XX:MaxTenuringThreshold=0 -XX:+UseCMSInitiatingOccupancyOnly -XX:CMSInitiatingOccupancyFraction=60 -XX:+PrintGCDetails -Xloggc:gc.log -jar beimi.war
ENTRYPOINT java -jar beimi-0.8.0.war