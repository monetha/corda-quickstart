FROM openjdk:8

RUN adduser --disabled-password --gecos '' corda

USER corda

WORKDIR /home/corda/

RUN curl -LO https://software.r3.com/artifactory/corda-releases/net/corda/corda-tools-network-bootstrapper/4.1/corda-tools-network-bootstrapper-4.1.jar

ENTRYPOINT [ "java", "-jar", "/home/corda/corda-tools-network-bootstrapper-4.1.jar", "--dir", "." ]
