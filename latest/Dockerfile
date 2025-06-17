FROM docker.m.daocloud.io/library/node:slim

RUN sed -i "s|deb.debian.org|mirrors.ustc.edu.cn|g" /etc/apt/sources.list.d/debian.sources\
 && apt update\
 && apt install -y ca-certificates\
 && sed -i "s|http://mirrors.ustc.edu.cn|https://mirrors.ustc.edu.cn|;s|bookworm-updates|bookworm-updates bookworm-backports|" /etc/apt/sources.list.d/debian.sources\
 && apt update\
 && apt full-upgrade -y\
 && apt install -y curl git valkey-server chromium fonts-lxgw-wenkai fonts-noto-color-emoji\
 && apt autoremove --purge\
 && apt clean\
 && git config --global --add safe.directory "*"\
 && npm install -g pnpm --registry "https://registry.npmmirror.com"\
 && rm -rf /var/cache/* /var/log/* /var/lib/apt /root/.npm\
 && echo -n "[ -s .git ]||git clone --depth 1 --single-branch \"https://gitee.com/TimeRainStarSky/Yunzai\" .&&pnpm install --force&&echo -n \"exec node . start\">/start&&exec node . start">/start

HEALTHCHECK CMD curl -s http://localhost:2536/status||exit 1

WORKDIR /root/Yunzai

ENTRYPOINT []

CMD ["sh","/start"]

EXPOSE 2536