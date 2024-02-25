FROM centos:7                                         # base image for the container

RUN yum -y install openssh-server                     # installing open ssh server

RUN useradd remote_user && \                          #adding user
    echo "1234" | passwd remote_user  --stdin && \    # adding password without interactive input
    mkdir /home/remote_user/.ssh && \                 #creating .ssh dir
    chmod 700 /home/remote_user/.ssh                  # changing mode of dir to read & write to user

COPY remote-key.pub /home/remote_user/.ssh/authorized_keys          # copyig our jenkins .pub ssh key to authrized keys in ubuntu machine

RUN chown remote_user:remote_user   -R /home/remote_user && \       # making user as the owner of dir
    chmod 400 /home/remote_user/.ssh/authorized_keys                # changing mod for the user to the file 

RUN ssh-keygen -A

RUN yum -y install mysql

RUN yum -y install epel-release && \
    yum -y install python3-pip && \
    pip3 install --upgrade pip && \
    pip3 install awscli

CMD /usr/sbin/sshd -D
