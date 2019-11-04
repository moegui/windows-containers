FROM openjdk:windowsservercore-1809

ARG JENKINS_VERSION
ENV JENKINS_VERSION ${JENKINS_VERSION:-2.190.2}
ARG JENKINS_URL=https://repo.jenkins-ci.org/public/org/jenkins-ci/main/jenkins-war/${JENKINS_VERSION}/jenkins-war-${JENKINS_VERSION}.war
ENV HOME /jenkins_home
ARG JENKINS_HOME=\jenkins_home
ENV JENKINS_HOME $JENKINS_HOME
ARG http_port=8080
ARG agent_port=50000
ENV JENKINS_SLAVE_AGENT_PORT ${agent_port}
ENV JAVA_OPTS=-Djenkins.install.runSetupWizard=false

RUN mkdir \jenkins_home
RUN mkdir \jenkins_home\workspace
RUN mkdir \jenkins_home\plugins

RUN "[Net.ServicePointManager]::SecurityProtocol = 'TLS11','TLS12','ssl3'" ; \
    Invoke-WebRequest -Uri ${env:JENKINS_URL} -OutFile /jenkins_home/jenkins.war ;

RUN Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

RUN choco install git -y

RUN "[Net.ServicePointManager]::SecurityProtocol = 'TLS11','TLS12','ssl3'" ; \
    Invoke-WebRequest -Uri https://updates.jenkins.io/download/plugins/apache-httpcomponents-client-4-api/4.5.5-3.0/apache-httpcomponents-client-4-api.hpi  -OutFile /jenkins_home/plugins/apache-httpcomponents-client-4-api.hpi ; \
    Invoke-WebRequest -Uri https://updates.jenkins.io/download/plugins/bouncycastle-api/2.17/bouncycastle-api.hpi -OutFile /jenkins_home/plugins/bouncycastle-api.hpi ; \
    Invoke-WebRequest -Uri https://updates.jenkins.io/download/plugins/command-launcher/1.3/command-launcher.hpi -OutFile /jenkins_home/plugins/command-launcher.hpi ; \
    Invoke-WebRequest -Uri https://updates.jenkins.io/download/plugins/credentials/2.1.18/credentials.hpi -OutFile /jenkins_home/plugins/credentials.hpi ; \
    Invoke-WebRequest -Uri https://updates.jenkins.io/download/plugins/display-url-api/2.3.0/display-url-api.hpi  -OutFile /jenkins_home/plugins/display-url-api.hpi ; \
    Invoke-WebRequest -Uri https://updates.jenkins.io/download/plugins/git/3.9.3/git.hpi -OutFile /jenkins_home/plugins/git.hpi ; \
    Invoke-WebRequest -Uri https://updates.jenkins.io/download/plugins/jdk-tool/1.2/jdk-tool.hpi -OutFile /jenkins_home/plugins/jdk-tool.hpi ; \
    Invoke-WebRequest -Uri https://updates.jenkins.io/download/plugins/jsch/0.1.55/jsch.hpi -OutFile /jenkins_home/plugins/jsch.hpi ; \
    Invoke-WebRequest -Uri https://updates.jenkins.io/download/plugins/junit/1.27/junit.hpi -OutFile /jenkins_home/plugins/junit.hpi ; \
    Invoke-WebRequest -Uri https://updates.jenkins.io/download/plugins/mailer/1.23/mailer.hpi -OutFile /jenkins_home/plugins/mailer.hpi ; \
    Invoke-WebRequest -Uri https://updates.jenkins.io/download/plugins/matrix-project/1.14/matrix-project.hpi -OutFile /jenkins_home/plugins/matrix-project.hpi ; \
    Invoke-WebRequest -Uri https://updates.jenkins.io/download/plugins/scm-api/2.3.0/scm-api.hpi -OutFile /jenkins_home/plugins/scm-api.hpi ; \
    Invoke-WebRequest -Uri https://updates.jenkins.io/download/plugins/script-security/1.54/script-security.hpi -OutFile /jenkins_home/plugins/script-security.hpi ; \
    Invoke-WebRequest -Uri https://updates.jenkins.io/download/plugins/ssh-credentials/1.15/ssh-credentials.hpi -OutFile /jenkins_home/plugins/ssh-credentials.hpi ; \
    Invoke-WebRequest -Uri https://updates.jenkins.io/download/plugins/structs/1.17/structs.hpi -OutFile /jenkins_home/plugins/structs.hpi ; \
    Invoke-WebRequest -Uri https://updates.jenkins.io/download/plugins/workflow-api/2.33/workflow-api.hpi -OutFile /jenkins_home/plugins/workflow-api.hpi ; \
    Invoke-WebRequest -Uri https://updates.jenkins.io/download/plugins/workflow-scm-step/2.7/workflow-scm-step.hpi -OutFile /jenkins_home/plugins/workflow-scm-step.hpi ; \
    Invoke-WebRequest -Uri https://updates.jenkins.io/download/plugins/workflow-step-api/2.19/workflow-step-api.hpi -OutFile /jenkins_home/plugins/workflow-step-api.hpi ; \
    Invoke-WebRequest -Uri https://updates.jenkins.io/download/plugins/git-client/2.7.6/git-client.hpi -OutFile /jenkins_home/plugins/git-client.hpi ;
    

COPY home \jenkins_home
EXPOSE ${http_port}
EXPOSE ${agent_port}

CMD java -jar C:\\jenkins_home\\jenkins.war ${JAVA_OPTS}

