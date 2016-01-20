FROM osxcc/osxcc:latest
MAINTAINER zchee <k@zchee.io>

ENV CC=o64-clang \
	CXX=o64-clang++ \
	\
	GOPATH=/go \
	PATH=$GOPATH/bin:/usr/local/go/bin:$PATH \
	GOOS=darwin \
	GOARCH=amd64 \
	CGO_ENABLED=1 \
	GO15VENDOREXPERIMENT=1 \
	\
	GOLANG_VERSION=1.6beta2 \
	GOLANG_DOWNLOAD_SHA256=7ddf9797c7baaac2c16eed1a8d42f9a446223301c7dc8771ea805f211828e6a5

RUN set -ex \
	&& curl -fsSL "https://storage.googleapis.com/golang/go1.4.3.linux-amd64.tar.gz" -o golang.tar.gz \
	&& echo "332b64236d30a8805fc8dd8b3a269915b4c507fe  golang.tar.gz" | sha1sum -c - \
	&& tar -C /root -xzf golang.tar.gz \
	&& rm golang.tar.gz \
	&& mv /root/go /root/go1.4 \
	&& curl -fsSL "https://golang.org/dl/go${GOLANG_VERSION}.linux-amd64.tar.gz" -o golang.tar.gz \
	&& echo "${GOLANG_DOWNLOAD_SHA256}  golang.tar.gz" | sha256sum -c - \
	&& tar -C /usr/local -xzf golang.tar.gz \
	&& rm golang.tar.gz \
	&& cd /usr/local/go/src \
	&& CC=clang CXX=clang++ GOOS=linux GOARCH=amd64 ./make.bash \
	&& CC=o64-clang CXX=o64-clang++ GOOS=darwin GOARCH=amd64 ./make.bash --no-clean \
	&& rm -rf /root/go1.4 \
	&& mkdir -p "${GOPATH}/src" "${GOPATH}/bin" && chmod -R 777 "${GOPATH}"

WORKDIR ${GOPATH}
