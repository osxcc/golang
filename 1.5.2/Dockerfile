FROM osxcc/osxcc:latest
MAINTAINER zchee <k@zchee.io>

ENV CC=o64-clang \
	CXX=o64-clang++ \
	\
	GOLANG_VERSION=1.5.2 \
	GOPATH=/go \
	PATH=$GOPATH/bin:/usr/local/go/bin:$PATH \
	GOARCH=amd64 \
	GOOS=darwin \
	CGO_ENABLED=1 \
	GO15VENDOREXPERIMENT=1 \
	\
	GOROOT_BOOTSTRAP=/go1.4.3 \
	GOLANG_DOWNLOAD_SHA1=cae87ed095e8d94a81871281d35da7829bd1234e

RUN set -ex \
	&& curl -fsSL "https://storage.googleapis.com/golang${GOROOT_BOOTSTRAP}.linux-amd64.tar.gz" -o golang.tar.gz \
	&& echo "332b64236d30a8805fc8dd8b3a269915b4c507fe  golang.tar.gz" | sha1sum -c - \
	&& tar -C / -xzf golang.tar.gz \
	&& rm golang.tar.gz \
	&& mv /go "${GOROOT_BOOTSTRAP}" \
	&& curl -fsSL "https://golang.org/dl/go${GOLANG_VERSION}.linux-amd64.tar.gz" -o golang.tar.gz \
	&& echo "${GOLANG_DOWNLOAD_SHA1}  golang.tar.gz" | sha1sum -c - \
	&& tar -C /usr/local -xzf golang.tar.gz \
	&& rm golang.tar.gz \
	&& cd /usr/local/go/src \
	&& CC=/usr/bin/clang \
		CXX=/usr/bin/clang++ \
		CC_FOR_TARGET=/osxcross/target/bin/o64-clang \
		CXX_FOR_TARGET=/osxcross/target/bin/o64-clang++ \
		./make.bash \
	&& rm -rf "${GOROOT_BOOTSTRAP}" \
	&& mkdir -p "${GOPATH}/src" "${GOPATH}/bin" && chmod -R 777 "${GOPATH}"

WORKDIR "$GOPATH}"
