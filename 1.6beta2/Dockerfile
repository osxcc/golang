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
	GOROOT_BOOTSTRAP=/go1.5.3 \
	GOLANG_VERSION=1.6beta2 \
	GOLANG_DOWNLOAD_SHA256=7ddf9797c7baaac2c16eed1a8d42f9a446223301c7dc8771ea805f211828e6a5

RUN set -ex \
	&& curl -fsSL "https://storage.googleapis.com/golang${GOROOT_BOOTSTRAP}.linux-amd64.tar.gz" -o golang.tar.gz \
	&& echo "43afe0c5017e502630b1aea4d44b8a7f059bf60d7f29dfd58db454d4e4e0ae53  golang.tar.gz" | sha256sum -c - \
	&& tar -C / -xzf golang.tar.gz \
	&& rm golang.tar.gz \
	&& mv /go "${GOROOT_BOOTSTRAP}" \
	&& curl -fsSL "https://golang.org/dl/go${GOLANG_VERSION}.linux-amd64.tar.gz" -o golang.tar.gz \
	&& echo "${GOLANG_DOWNLOAD_SHA256}  golang.tar.gz" | sha256sum -c - \
	&& tar -C /usr/local -xzf golang.tar.gz \
	&& rm golang.tar.gz \
	&& cd /usr/local/go/src \
	&& CC=clang CXX=clang++ GOOS=linux GOARCH=amd64 ./make.bash \
	&& CC=o64-clang CXX=o64-clang++ GOOS=darwin GOARCH=amd64 ./make.bash --no-clean \
	&& rm -rf "${GOROOT_BOOTSTRAP}" \
	&& mkdir -p "${GOPATH}/src" "${GOPATH}/bin" && chmod -R 777 "${GOPATH}"

WORKDIR ${GOPATH}
