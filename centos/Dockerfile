FROM centos:centos8
MAINTAINER The CentOS Project <cloud-ops@centos.org


#使用 ADD 命令将 CentOS-Base.repo 拷贝到目标基础镜像的目录下
ADD  CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo
#更新yum源|如果你不需要更新版本，可以不执行此命令（升级后的版本太高可能导致原有软件不能运行）
RUN yum -y update && \
    yum clean all

# 基础库
RUN yum -y install vim sudo && \
    yum clean all

# python
RUN yum -y install gcc mesa-libGL.x86_64 python38 python38-devel && \
    yum clean all

# node
RUN yum -y install nodejs && \
    yum clean all
