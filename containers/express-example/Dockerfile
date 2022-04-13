ARG NODE_VERSION=16.14.2
FROM public.ecr.aws/docker/library/node:$NODE_VERSION-slim
ARG NODE_VERSION=16.14.2

WORKDIR /opt/app

COPY package.json .
RUN npm install
COPY server.js .

EXPOSE 80
CMD [ "node", "server.js" ]
