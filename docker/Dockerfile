FROM ubuntu:20.04

ENV TZ=Europe/Rome
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Initialize the environment 
RUN apt update
RUN apt install -y cmake git emacs build-essential

# Prepare and empty machine for building:
RUN apt-get update -yq
RUN apt-get install -yq
RUN apt-get -y install git cmake libpng-dev libjpeg-dev libtiff-dev libglu1-mesa-dev

# Eigen (Known issues with eigen 3.3.7 as of 12/10/2019, so using this tested branch/commit instead) 
RUN git clone https://gitlab.com/libeigen/eigen --branch 3.2
RUN mkdir eigen_build
RUN cd eigen_build &&\
	cmake . ../eigen &&\
	make && make install &&\
	cd ..

# Boost
RUN apt-get -y install libboost-iostreams-dev libboost-program-options-dev libboost-system-dev libboost-serialization-dev

# OpenCV
RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq libopencv-dev

# CGAL
RUN apt-get -y install libcgal-dev libcgal-qt5-dev

# VCGLib
RUN git clone https://github.com/cdcseacave/VCG.git vcglib

#RUN mkdir -p openMVS/build
#RUN mkdir -p openMVS/repo

#WORKDIR /openMVS/repo

#RUN git clone https://github.com/3DOM-FBK/openMVS.git --branch geom_consistency .

#WORKDIR /openMVS/build
#RUN cmake . ../repo -DCMAKE_BUILD_TYPE=Release -DVCG_ROOT=/vcglib

# Install OpenMVS library
#RUN make -j4 && make install

#ENV PATH /usr/local/bin/OpenMVS:$PATH

CMD bash
