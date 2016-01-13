FROM osxcc/osxcc:latest
MAINTAINER zchee <zchee.io@gmail.com>

ENV CC o64-clang
ENV CXX o64-clang++

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH
ENV GOOS darwin
ENV GOARCH amd64
ENV CGO_ENABLED 1
ENV GO15VENDOREXPERIMENT 1

ENV GOLANG_VERSION devel

RUN set -ex \
	&& curl -fsSL "https://storage.googleapis.com/golang/go1.4.3.linux-amd64.tar.gz" -o golang.tar.gz \
	&& echo "332b64236d30a8805fc8dd8b3a269915b4c507fe  golang.tar.gz" | sha1sum -c - \
	&& tar -C /root -xzf golang.tar.gz \
	&& rm golang.tar.gz \
	&& mv /root/go /root/go1.4 \
	&& git clone "https://go.googlesource.com/go" /usr/local/go \
	&& cd /usr/local/go/src \
	&& CC=clang CXX=clang++ GOOS=linux GOARCH=amd64 ./make.bash \
	&& CC=o64-clang CXX=o64-clang++ GOOS=darwin GOARCH=amd64 ./make.bash --no-clean \
	&& rm -rf /root/go1.4 \
	&& mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"

WORKDIR $GOPATH
