
FROM phusion/baseimage:0.9.17
MAINTAINER Alexandre Ancel <alexandre.ancel@cemosis.fr>

# Install build environment
RUN apt-get -qq update \
    && apt-get -y --force-yes install sudo xauth vim tmux screen wget \
        git cmake pkg-config automake autoconf libtool \
        g++ gfortran clang-3.6 \
        qt4-dev-tools libqt4-dev libxt-dev python-dev libopenmpi-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Compilers
ENV CC /usr/bin/clang-3.6
ENV CXX /usr/bin/clang++-3.6 

# ParaView
ENV PARAVIEW_VERSION 4.4.0

WORKDIR /tmp
RUN wget "http://www.paraview.org/paraview-downloads/download.php?submit=Download&version=v4.4&type=source&os=all&downloadFile=ParaView-v${PARAVIEW_VERSION}-source.tar.gz" -O ParaView-v${PARAVIEW_VERSION}-source.tar.gz
RUN tar xvzf ParaView-v${PARAVIEW_VERSION}-source.tar.gz
RUN mkdir -p ParaView-v${PARAVIEW_VERSION}-source/build

WORKDIR /tmp/ParaView-v${PARAVIEW_VERSION}-source/build
RUN cmake -DCMAKE_CXX_COMPILER=${CXX} -DCMAKE_C_COMPILER=${CC} \
        -DCMAKE_INSTALL_PREFIX=/opt/ParaView/4.4.0 -DCMAKE_BUILD_TYPE=Release \
        -DPARAVIEW_BUILD_QT_GUI=ON -DPARAVIEW_ENABLE_CATALYST=ON \
        -DPARAVIEW_ENABLE_PYTHON=ON -DPARAVIEW_INSTALL_DEVELOPMENT_FILES=ON \
        -DPARAVIEW_USE_MPI=ON \
        -DBUILD_TESTING=OFF \
        ..
RUN make -j16 && make install
RUN rm -rf /tmp/*

# Set up user so that we do not run as root
# Changing the password does not work on certain OS and is not needed
RUN useradd -m -s /bin/bash -G sudo,docker_env johndoe && \
    echo "johndoe ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# See https://github.com/phusion/baseimage-docker/issues/186
RUN touch /etc/service/syslog-forwarder/down

ENV HOME /home/johndoe

CMD ["/bin/bash"]
