#FROM golang:1.18.4-alpine as builder
FROM registry.cn-hangzhou.aliyuncs.com/lbinf/zpscan as builder
RUN apk add --no-cache make git
RUN apk -U --no-cache add libpcap-dev
RUN apk add gcc g++ make cmake
RUN git clone https://github.com/niudaii/zpscan  && mv zpscan  /zpscan-src
WORKDIR /zpscan-src
#COPY . /zpscan-src
RUN go mod download && go build main.go && ls -la  && mv main /zpscan
#    make docker && \
#    mv ./bin/zpscan-docker /zpscan
    
 ENTRYPOINT ["/zpscan"]   
