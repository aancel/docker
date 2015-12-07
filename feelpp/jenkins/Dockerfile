FROM jenkins

# ENV BUILD llvm-3.5
# ENV FEELPP_CXX clang++-3.5
# ENV FEELPP_CC clang-3.5
# ENV BUILDTYPE Release
# ENV TARGET quickstart
# ENV CXXFLAGS -O2

#ENV CC clang
#ENV CXX clang++

RUN apt-get -qq update
RUN apt-get install -y python-software-properties wget 
RUN add-apt-repository -y ppa:boost-latest/ppa
RUN add-apt-repository -y ppa:kalakris/eigen
RUN add-apt-repository -y ppa:feelpp/petsc
RUN apt-get -qq update
RUN apt-get install -y -qq cmake git make vim
RUN apt-get install -y -qq gcc-4.8 clang-3.5
RUN apt-get install -y -qq libboost1.55-all-dev mpi-default-dev mpi-default-bin libeigen3-dev libpetsc3.4.2-dev libcln-dev petsc-dev libxml2-dev gmsh bison flex transfig imagemagick libtbb-dev libann-dev libglpk-dev automake libtool
