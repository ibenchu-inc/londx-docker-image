ARG NODE_VERSION=20
FROM node:${NODE_VERSION}-alpine

ENV LANG=C.UTF-8

# 设置时区为上海，日志中文
RUN apk add --no-cache tzdata && \
    cp -r -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo "Asia/Shanghai" > /etc/timezone && \
    apk del tzdata

# 安装 pm2 及 typescript 支持
RUN npm install pm2@latest -g && pm2 install typescript

WORKDIR /var/www/

EXPOSE 3000

CMD ["pm2-runtime", "npm","--","start"]


