FROM openjdk:11.0.5-windowsservercore-1809

ARG JENKINS_VERSION
ENV JENKINS_VERSION ${JENKINS_VERSION:-latest}
ARG JENKINS_URL=https://updates.jenkins.io/${JENKINS_VERSION}/jenkins.war
ENV HOME /jenkins_home
ARG JENKINS_HOME=C:\\jenkins_home
ENV JENKINS_HOME $JENKINS_HOME
ARG http_port=8080
ARG agent_port=50000
ENV JENKINS_SLAVE_AGENT_PORT ${agent_port}
ENV JAVA_OPTS=-Djenkins.install.runSetupWizard=true

RUN mkdir \jenkins_home
RUN mkdir \jenkins_home\workspace
RUN mkdir \jenkins_home\plugins

RUN "[Net.ServicePointManager]::SecurityProtocol = 'TLS11','TLS12','ssl3'" ; \
    Invoke-WebRequest -Uri ${env:JENKINS_URL} -OutFile \jenkins_home\jenkins.war ;

RUN Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

RUN choco install git -y

EXPOSE ${http_port}
EXPOSE ${agent_port}

CMD java -jar C:\\jenkins_home\\jenkins.war ${JAVA_OPTS}