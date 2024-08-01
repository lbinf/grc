#FROM golang:1.18.4-alpine as builder
FROM registry.cn-hangzhou.aliyuncs.com/lbinf/zpscan as builder
RUN apk add --no-cache make git
RUN apk -U --no-cache add libpcap-dev
RUN apk add gcc g++ make cmake
RUN git clone https://github.com/niudaii/zpscan  && cp -R zpscan/*  /zpscan-src
WORKDIR /zpscan-src
#COPY . /zpscan-src
RUN go mod download && \
    make docker && \
    mv ./bin/zpscan-docker /zpscan
    
 ENTRYPOINT ["/zpscan"]   
