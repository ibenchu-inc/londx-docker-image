ARG NODE_VERSION=20
FROM node:${NODE_VERSION}-alpine

ENV LANG=C.UTF-8

# 设置时区为上海，日志中文
RUN apk add --no-cache tzdata && \
    cp -r -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo "Asia/Shanghai" > /etc/timezone && \
    apk del tzdata

# 安装常用工具和 SSH
RUN apk add --no-cache build-base wget curl busybox openssh git python3 && \
    sed -i s/#PermitRootLogin.*/PermitRootLogin\ yes/ /etc/ssh/sshd_config && \
    echo "root:root" | chpasswd && \
    ssh-keygen -A

# 安装 pm2 及 typescript 支持
RUN npm install pm2@latest -g && pm2 install typescript

# TEST: 安装 argon2
RUN npm install argon2

# 国内源加速
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories
RUN npm set registry https://registry.npm.taobao.org && \
    npm set disturl https://npm.taobao.org/dist && \
    npm set sass_binary_site https://npm.taobao.org/mirrors/node-sass

WORKDIR /var/www/

EXPOSE 22

CMD ["/usr/sbin/sshd","-D","-e"]
