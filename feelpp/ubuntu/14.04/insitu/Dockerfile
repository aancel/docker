FROM ubuntu:14.04.2

ENV FEELPP_CXX clang++-3.6
ENV FEELPP_CC clang-3.6
ENV BUILDTYPE Release

ENV CC ${FEELPP_CC}
ENV CXX ${FEELPP_CXX}

RUN apt-get -qq update
RUN apt-get install -y software-properties-common python-software-properties
RUN add-apt-repository ppa:ubuntu-toolchain-r/test
RUN apt-get -qq update
RUN apt-get install -y -qq gcc-4.9 g++-4.9
RUN apt-get install -y -qq cmake git make vim automake libtool man wget 
RUN apt-get install -y -qq ${FEELPP_CC} mpi-default-dev mpi-default-bin

# make directories
RUN mkdir -p /root/src
WORKDIR /root/src

# Get source and extract if needed
# ParaView
RUN wget -O ParaView-v4.4.0-source.tar.gz "http://www.paraview.org/paraview-downloads/download.php?submit=Download&version=v4.4&type=source&os=all&downloadFile=ParaView-v4.4.0-source.tar.gz"
RUN tar zxvf ParaView-v4.4.0-source.tar.gz

# Install additional dependencies
RUN apt-get install -y -qq xserver-xorg libgl1-mesa-dev libxt-dev libpython-dev

# Build ParaView
RUN mkdir -p /root/build/ParaView/4.4.0
WORKDIR /root/build/ParaView/4.4.0

RUN cmake /root/src/ParaView-v4.4.0-source -DCMAKE_C_COMPILER=/usr/bin/clang-3.6 -DCMAKE_CXX_COMPILER=/usr/bin/clang++-3.6 -DCMAKE_BUILD_TYPE=Release -DPARAVIEW_BUILD_QT_GUI=OFF -DPARAVIEW_ENABLE_CATALYST=ON -DPARAVIEW_ENABLE_PYTHON=ON -DPARAVIEW_INSTALL_DEVELOPMENT_FILES=ON -DPARAVIEW_USE_MPI=ON
RUN make -j 4 install

# Build Feel++
WORKDIR /root/src
RUN git clone --depth=1 --branch=develop git://github.com/feelpp/feelpp.git feelpp

# Install additional dependencies
RUN apt-get install -y -qq bison flex libcln-dev libann-dev libglpk-dev libreadline-dev
RUN apt-get install -y -qq libboost1.55-all-dev libhdf5-mpi-dev libxml2-dev 
RUN apt-get install -y -qq libeigen3-dev petsc-dev libgmsh-dev gmsh

RUN mkdir -p /root/build/feelpp/develop
WORKDIR /root/build/feelpp/develop

RUN cmake /root/src/feelpp -DCMAKE_C_COMPILER=/usr/bin/clang-3.6 -DCMAKE_CXX_COMPILER=/usr/bin/clang++-3.6 -DCMAKE_BUILD_TYPE=Release -DFEELPP_ENABLE_VTK_INSITU=ON -DCMAKE_BUILD_TYPE=${BUILDTYPE}
RUN make -j 16 install-feelpp
#RUN make -j 16 quickstart
RUN make -j 16 install

CMD ["/bin/bash"]
