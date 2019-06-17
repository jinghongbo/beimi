FROM node as build
ADD https://storage.googleapis.com/otsimobuilds/cocos-creator-1.9.0-linux.tar.xz ./opt/
RUN tar xvjf cocos-creator-1.9.0-linux.tar.xz -d /opt/cocos-creator
FROM nginx
COPY client/version/chess/build/web-mobile /usr/share/nginx/html