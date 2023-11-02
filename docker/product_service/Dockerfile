FROM ubuntu
ENV TZ=Europe/Moscow
RUN apt-get clean && apt-get update -y 
RUN DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get -y install tzdata git sudo build-essential autoconf libtool libssl-dev zlib1g-dev librdkafka-dev pkg-config cmake gcc git g++ mysql-client libmysqlclient-dev libboost-all-dev libssl-dev && apt-get clean
RUN git clone --depth 1 --branch poco-1.12.4-release https://github.com/pocoproject/poco.git && cd poco && mkdir cmake-build && cd cmake-build && cmake .. && make -j2 && sudo make install && cd .. && cd ..
RUN git clone https://github.com/edenhill/librdkafka.git && cd librdkafka && ./configure && make && sudo make install && cd 
RUN git clone https://github.com/mfontanini/cppkafka && cd cppkafka && mkdir build && cd build && cmake .. && make && sudo make install && cd 
RUN git clone https://github.com/PavelProjects/arch_lab.git
RUN cd ./arch_lab && mkdir build && cd build && cmake  .. && make product_service
RUN sudo ldconfig
ENTRYPOINT [ "arch_lab/build/product_service" ]