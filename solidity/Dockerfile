FROM node:15.11-alpine3.13

RUN echo -e 'https://mirrors.aliyun.com/alpine/v3.6/main/\nhttps://mirrors.aliyun.com/alpine/v3.6/community/' > /etc/apk/repositories

RUN apk update
RUN apk add --no-cache python3 make g++ curl

COPY package.json package.json
COPY package-lock.json package-lock.json


RUN npm config set registry https://registry.npm.taobao.org --global

RUN npm config set disturl https://npm.taobao.org/dist --global

RUN npm ci

COPY . .
RUN npm ci
RUN chmod -R +x scripts

RUN npm run typechain


RUN  export PKG_CACHE_PATH=./pkg_cache
RUN  npm run compile-deployer


CMD tail -f /dev/null