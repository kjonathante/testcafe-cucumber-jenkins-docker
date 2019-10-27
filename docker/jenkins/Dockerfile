FROM jenkins/jenkins:lts

# Run stuff as root

USER root

# Install with apt

RUN apt-get update -qqy && apt-get install -qqy --no-install-recommends \
    apt-transport-https \
    ca-certificates \
    software-properties-common \
 && curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - \
 && apt-key fingerprint 0EBFCD88 \
 && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" \
 && apt-get update -qqy \
 && apt-get install -qqy docker-ce \
 && usermod --append --groups docker jenkins

 # Disable Jenkins manual setup

ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"

# Copy the configuration scripts

COPY bin/security.groovy /usr/share/jenkins/ref/init.groovy.d/security.groovy
COPY bin/csp.groovy /usr/share/jenkins/ref/init.groovy.d/csp.groovy

# Install Jenkins plugins

COPY config/plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

# Add jenkins user to sudo group so we can run docker under jenkins user

RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers
