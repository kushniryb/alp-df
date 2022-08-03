FROM alpine:latest

RUN apk add --no-cache git swig cmake ruby-dev gcompat build-base

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
