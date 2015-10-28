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
RUN apt-get install -y -qq gcc-5 g++-5
RUN apt-get install -y -qq cmake git make vim automake libtool man libreadline-dev
RUN apt-get install -y -qq ${FEELPP_CC} mpi-default-dev mpi-default-bin
RUN apt-get install -y -qq bison flex libcln-dev libann-dev libglpk-dev
RUN apt-get install -y -qq libboost1.55-all-dev libhdf5-mpi-dev libxml2-dev 
RUN apt-get install -y -qq libeigen3-dev petsc-dev libgmsh-dev gmsh

RUN mkdir /src
WORKDIR /src
RUN git clone --depth=1 --branch=develop git://github.com/feelpp/feelpp.git /src/feelpp
RUN mkdir -p /build/opt-llvm
WORKDIR /build/opt-llvm
#RUN cmake /src/feelpp -DCMAKE_C_COMPILER=/usr/bin/clang-3.6 -DCMAKE_CXX_COMPILER=/usr/bin/clang++-3.6 -DCMAKE_BUILD_TYPE=${BUILDTYPE}
#RUN make -j 16 install-feelpp
#RUN make -j 16 quickstart
#RUN make -j 16 install

CMD ["/bin/bash"]
