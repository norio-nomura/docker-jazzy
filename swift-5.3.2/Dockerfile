FROM norionomura/swift:532
LABEL maintainer "Norio Nomura <norio.nomura@gmail.com>"

RUN apt-get update && apt-get install -y \
    libsqlite3-dev libxml2-dev ruby-dev && \
    rm -r /var/lib/apt/lists/*

ENV SOURCEKITTEN_REVISION="0.30.1"
ENV JAZZY_VERSION=""

# Install SourceKitten
RUN git clone --branch $SOURCEKITTEN_REVISION https://github.com/jpsim/SourceKitten.git && \
    cd SourceKitten && \
    swift build --configuration release -Xswiftc -static-stdlib && \
    mv `swift build --configuration release -Xswiftc -static-stdlib --show-bin-path`/sourcekitten /usr/bin && \
    cd .. && \
    rm -rf SourceKitten && \
    gem install bundler && \
    gem install cocoapods-downloader --version 1.3 && \
    gem install cocoapods --version 1.9 && \
    gem install jazzy --version "$JAZZY_VERSION"

# Print Installed SourceKitten Version
RUN sourcekitten version
