# IMG
FROM centos:7

# WHO
MAINTAINER boxu@yvhai.com

# Install Basic
# RUN rm -rvf /etc/yum.repos.d/* \
    # && curl http://mirrors.163.com/.help/CentOS7-Base-163.repo -o /etc/yum.repos.d/CentOS7-Base-163.repo \
RUN date \
    && yum update -y \
    && ls -lhrt /etc/yum.repos.d/ \
    && yum install -y sudo make which \
    && yum install -y vim rsync screen sysstat unzip \
    && yum install -y openssh-server openssh-clients \
    && yum install -y tree net-snmp-utils net-tools bind-utils iputils telnet lsof yum-utils \
    && yum install -y device-mapper-persistent-data lvm2 \
    && yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo \
    && yum install -y docker-ce \
    && yum clean all && rm -rf /var/cache/yum

# Install Spec
RUN date \
    && curl -L https://get.daocloud.io/docker/compose/releases/download/1.22.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose \
    && systemctl enable docker \
    && yum clean all && rm -rf /var/cache/yum

# Config
RUN [ ! -d /etc/docker ] && mkdir /etc/docker
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo -e '{\n    "registry-mirrors": ["http://f1361db2.m.daocloud.io"]\n}\n' > /etc/docker/daemon.json \
    && echo -e "\nUseDNS no\nGSSAPIAuthentication no\n" >> /etc/ssh/sshd_config

# patch
# RUN yum install -y xx

# 创建用户
RUN groupadd -g 1000 foobar \
    && useradd -g foobar -u 1000 -s /bin/bash foobar \
    && gpasswd -a foobar docker \
    && echo "foobar ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/99-yh-foobar


# 接口
WORKDIR /project
# USER foobar
EXPOSE 22
VOLUME [ "/project", "/var/run/docker.sock", "/var/lib/docker" ]


# clean


# CMD
ENTRYPOINT [ "/usr/sbin/init" ] 
