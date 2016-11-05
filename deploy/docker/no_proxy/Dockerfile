FROM debian:latest

ENV http_proxy=

RUN apt-get update
RUN apt-get install --force-yes -y wget
RUN mkdir -p /opt
RUN chmod 777 -R /opt
RUN apt-get update
RUN wget -P /opt/ https://raw.githubusercontent.com/tulioalberton/multinet/master/deploy/commands.sh
RUN chmod +x /opt/commands.sh
RUN /bin/bash  "/opt/commands.sh $http_proxy"

# Configure ssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:zaq1' | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
