FROM centos:centos8
MAINTAINER The CentOS Project <cloud-ops@centos.org


#使用 ADD 命令将 CentOS-Base.repo 拷贝到目标基础镜像的目录下
ADD  CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo
#更新yum源|如果你不需要更新版本，可以不执行此命令（升级后的版本太高可能导致原有软件不能运行）
RUN yum -y update && \
    yum clean all

# 基础库
RUN yum -y install epel-release vim sudo && \
    yum -y install screen && \
    yum -y install wget && \
    yum clean all

# python
RUN yum -y install gcc mesa-libGL.x86_64 python38 python38-devel && \
    yum clean all

# node
RUN yum -y install nodejs && \
    npm install -g gulp && \
    yum clean all

# libreoffice库
RUN yum remove libreoffice-* && \
    yum -y install cairo cups-libs libSM && \
    yum install -y ibus && \
    yum install -y libreoffice-headless && \
    yum clean all && \
    # 下载且安装libreoffice库 
    wget -P /opt/soft https://download.documentfoundation.org/libreoffice/stable/7.1.5/rpm/x86_64/LibreOffice_7.1.5_Linux_x86-64_rpm.tar.gz && \
    cd /opt/soft && \
    tar xvf LibreOffice_7.1.5_Linux_x86-64_rpm.tar.gz && \
    cd LibreOffice_7.1.5.2_Linux_x86-64_rpm/RPMS && \
    yum localinstall -y *.rpm && \
    # 下载中文字体
    wget -P /opt/soft https://s3.taihuoniao.com/tian/Fonts.tar.gz && \
    cd /opt/soft && \
    tar xvf Fonts.tar.gz && \
    mv /opt/soft/Fonts /usr/share/fonts/chinese && \
    chmod -R 755 /usr/share/fonts/chinese && \
    fc-cache -fv && \
    rm -rf /opt/soft/*


# java依赖
RUN yum -y install java-1.8.0-openjdk* && \
    yum clean all

