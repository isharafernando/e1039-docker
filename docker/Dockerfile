FROM scientificlinux/sl:7

RUN yum -y update && \
    yum -y install sudo screen wget patch libtool git-all gcc gcc-c++ gcc-gfortran \
           boost-devel python-devel cmake doxygen mariadb-devel sqlite-devel \
           zlib-devel freetype-devel pcre-devel xz-devel lz4-devel libX11-devel \
           libXpm-devel libXft-devel libXext-devel fftw-devel gsl-devel libxml2-devel \
           openssl-devel libXmu-devel xerces-c-devel mesa-libGL-devel mesa-libGLU-devel && \
    yum -y clean all && \
    useradd -d /home/e1039 -G wheel -m -U -p $(openssl passwd -1 spinquest) e1039 && \
    mkdir -p /opt/e1039/.downloads && chown -R e1039:e1039 /opt/e1039 && \
    mkdir -p /var/e1039_install_cache && chown -R e1039:e1039 /var/e1039_install_cache
COPY yum.conf /etc/yum.conf
COPY sqsetup /usr/local/bin
COPY tarballs/share.tar.bz2      /var/e1039_install_cache/
COPY tarballs/resource.tar.bz2   /var/e1039_install_cache/
COPY tarballs/core.tar.bz2       /var/e1039_install_cache/
COPY install_cache/*             /var/e1039_install_cache/


# below should be done as normal user
USER e1039
WORKDIR /home/e1039

COPY --chown=e1039:e1039 this-e1039.sh      /opt/e1039
RUN cat /var/e1039_install_cache/bashrc_supplement >> /home/e1039/.bashrc

CMD ["/bin/bash"]