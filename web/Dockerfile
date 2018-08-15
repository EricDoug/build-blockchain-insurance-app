FROM node:8.11.3

ENV NODE_ENV production
ENV PORT 3000
ENV DOCKER_SOCKET_PATH /host/var/run/docker.sock
ENV DOCKER_CCENV_IMAGE hyperledger/fabric-ccenv:x86_64-1.1.0

RUN mkdir /app
COPY . /app
WORKDIR /app
RUN cp /etc/apt/sources.list /etc/apt/sources.list.old
COPY sources.list /etc/apt/
RUN apt-get update && apt-get install -y build-essential --force-yes\
	  && npm config set registry https://registry.npm.taobao.org \
      && npm i && npm i --only=dev \
      && npm run build \
      && npm prune \
      && apt-get remove -y build-essential --force-yes

EXPOSE 3000
CMD ["npm", "run", "serve"]
