FROM clojure:openjdk-8-lein-2.9.1-slim-buster

WORKDIR /tmp
COPY project.clj .

RUN set -ex; \
  apt-get update; \
  apt-get -y upgrade; \
  apt install -y curl; \
  curl -sL https://deb.nodesource.com/setup_12.x | bash - ;\
  apt install -y nodejs; \
  lein ancient upgrade :check-clojure; \
  lein do deps, npm install; \
  apt -y autoremove; \
  apt -y autoclean

ENV CLOJURE_TOOLS=linux-install-1.10.1.466.sh
RUN curl -O https://download.clojure.org/install/${CLOJURE_TOOLS} && \
  chmod +x ${CLOJURE_TOOLS} && \
  ./${CLOJURE_TOOLS} && \
  clojure -Stree

# rm project.clj; \

EXPOSE 7888 9500