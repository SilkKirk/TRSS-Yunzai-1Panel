# 基于 node:slim 镜像
FROM node:slim

# 设置APT源为USTC
RUN sed -i "s|deb.debian.org|mirrors.ustc.edu.cn|g" /etc/apt/sources.list.d/debian.sources\
    && apt update\
    && apt install -y ca-certificates\
    && sed -i "s|http://mirrors.ustc.edu.cn|https://mirrors.ustc.edu.cn|g" /etc/apt/sources.list.d/debian.sources\
    && apt update\
    && apt full-upgrade -y\
    && apt install -y curl git redis-server chromium fonts-lxgw-wenkai fonts-noto-color-emoji\
    && apt autoremove --purge -y\
    && apt clean\
    && git config --global --add safe.directory "*"\
    && npm install -g pnpm --registry "https://registry.npmmirror.com"\
    && rm -rf /var/cache/* /var/log/* /var/lib/apt /root/.npm

# 工作目录
WORKDIR /root/Yunzai

# 克隆Yunzai项目并安装依赖
RUN [ -s .git ] || git clone --depth 1 --single-branch "https://gitee.com/TimeRainStarSky/Yunzai" . \
    && pnpm install --force

# 创建启动脚本
RUN echo -n 'exec node . start' > /start

# 健康检查
HEALTHCHECK CMD curl -s http://localhost:2536/status || exit 1

# 启动命令
ENTRYPOINT []
CMD ["sh", "/start"]

# 暴露端口
EXPOSE 2536