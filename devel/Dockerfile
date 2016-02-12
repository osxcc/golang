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
	GOROOT_BOOTSTRAP=/go1.6rc2 \
	GOROOT_BOOTSTRAP_SHA256=9c19fa0fe32ee9bff79123d47147a5fd15fec451806bf5644a01173a86a8a4b9

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
