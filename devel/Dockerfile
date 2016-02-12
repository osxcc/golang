FROM osxcc/osxcc:latest
MAINTAINER zchee <k@zchee.io>

ENV CC=o64-clang \
	CXX=o64-clang++ \
	\
	GOLANG_VERSION=devel \
	GOPATH=/go \
	PATH=$GOPATH/bin:/usr/local/go/bin:$PATH \
	GOARCH=amd64 \
	GOOS=darwin \
	CGO_ENABLED=1 \
	GO15VENDOREXPERIMENT=1 \
	\
	GOROOT_BOOTSTRAP=/go1.6beta2 \
	GOROOT_BOOTSTRAP_SHA256=7ddf9797c7baaac2c16eed1a8d42f9a446223301c7dc8771ea805f211828e6a5

RUN set -ex \
	&& curl -fsSL "https://storage.googleapis.com/golang${GOROOT_BOOTSTRAP}.linux-amd64.tar.gz" -o golang.tar.gz \
	&& echo "${GOROOT_BOOTSTRAP_SHA256}  golang.tar.gz" | sha256sum -c - \
	&& tar -C / -xzf golang.tar.gz \
	&& rm golang.tar.gz \
	&& mv /go "${GOROOT_BOOTSTRAP}"

ONBUILD RUN git clone "https://go.googlesource.com/go" /usr/local/go \
		&& cd /usr/local/go/src \
		&& CC=/usr/bin/clang \
			CXX=/usr/bin/clang++ \
			CC_FOR_TARGET=/osxcross/target/bin/o64-clang \
			CXX_FOR_TARGET=/osxcross/target/bin/o64-clang++ \
			./make.bash \
		&& rm -rf "${GOROOT_BOOTSTRAP}" \
		&& mkdir -p "${GOPATH}/src" "${GOPATH}/bin" \
		&& chmod -R 777 "${GOPATH}"

WORKDIR "$GOPATH"
