FROM alpine:latest

RUN apk add --no-cache git swig cmake ruby-dev build-base

# Install GLIBC 2.35-r0
RUN wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub
RUN wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.35-r0/glibc-2.35-r0.apk
RUN wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.35-r0/glibc-bin-2.35-r0.apk
RUN apk add glibc-2.35-r0.apk
RUN apk add glibc-bin-2.35-r0.apk
ENV LD_LIBRARY_PATH="/usr/glibc-compat/lib/:${LD_LIBRARY_PATH}"
ENV PATH="/usr/glibc-compat/bin/:${PATH}"

WORKDIR /~
RUN git clone https://github.com/PDFTron/PDFNetWrappers

WORKDIR /~/PDFNetWrappers/PDFNetC
RUN wget http://www.pdftron.com/downloads/PDFNetC64.tar.gz
RUN tar xzvf PDFNetC64.tar.gz
RUN mv PDFNetC64/Headers/ .
RUN mv PDFNetC64/Lib/ .
RUN rm PDFNetC64.tar.gz

WORKDIR /~/PDFNetWrappers
RUN mkdir Build

WORKDIR /~/PDFNetWrappers/Build
RUN cmake -D BUILD_PDFNetRuby=ON ..
RUN make
RUN make install

WORKDIR /~/PDFNetWrappers/Samples/AddImageTest/RUBY
