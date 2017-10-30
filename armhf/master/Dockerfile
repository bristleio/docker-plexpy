FROM resin/raspberrypi3-alpine-python:3.6-slim
MAINTAINER loganavatar

# set version label
ARG BUILD_DATE
ARG VERSION
ARG GIT_URL='https://github.com/JonnyWong16/plexpy'
ARG GIT_BRANCH=master
LABEL build_version="bristle.io version:- ${VERSION} Build-date:- ${BUILD_DATE}"

# install packages
RUN \
 apk add --no-cache --virtual=build-dependencies \
	g++ \
	gcc \
	make \
        git \
	python-dev && \

# install pycryptodomex
 pip install --no-cache-dir -U \
	pycryptodomex && \

# check to see if branch exists
 remotecheck=$(git ls-remote --heads $GIT_URL $GIT_BRANCH | wc -l) && \

# install app
 if [ $remotecheck = 0 ]; then \
    echo "Bad branch name, $GIT_BRANCH, cloning master instead." && \
    git clone --branch master --depth 1 $GIT_URL /app/plexpy; \
  else \
    echo "Cloning $GIT_BRANCH" && \
    git clone --branch $GIT_BRANCH --depth 1 $GIT_URL /app/plexpy; \
 fi && \

# cleanup
 apk del --purge \
	build-dependencies && \
 rm -rf \
	/root/.cache

# add local files
COPY root/ /

# ports and volumes
VOLUME /config /logs
EXPOSE 8181
