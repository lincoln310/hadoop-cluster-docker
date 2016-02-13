FROM kiwenlau/serf-dnsmasq:0.1.0

MAINTAINER KiwenLau <kiwenlau@gmail.com>

# install openssh-server, vim and openjdk
RUN apt-get update -y
RUN apt-get install -y openssh-server vim
RUN apt-get install -y openjdk-7-jdk 

# move all configuration files into container
ADD files/* /usr/local/  

# set jave environment variable 
ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64 
ENV PATH $PATH:$JAVA_HOME/bin

#configure ssh free key access
RUN mkdir /var/run/sshd && \
ssh-keygen -t rsa -f ~/.ssh/id_rsa -P '' && \
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys && \
mv /usr/local/ssh_config ~/.ssh/config && \
sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

#install hadoop 2.6.3
RUN ln -s /usr/local/hadoop-2.6.3 /usr/local/hadoop && \
#RUN curl -s http://www.eu.apache.org/dist/hadoop/common/hadoop-2.6.3/hadoop-2.6.3.tar.gz | tar -xz -C /usr/local/ \
#RUN cd /usr/local && ln -s ./hadoop-2.6.3 hadoop \
mv /usr/local/bashrc ~/.bashrc && \
mv /usr/local/hadoop-env.sh /usr/local/hadoop/etc/hadoop/hadoop-env.sh 
