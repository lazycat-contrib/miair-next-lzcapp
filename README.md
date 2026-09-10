# MiAir Next for LazyCat

让小米小爱音箱化身 DLNA 渲染器和 AirPlay 接收器，并附带一个现代化的 Web 管理后台。

上游：https://github.com/deerwan/miair-next

## 安装与使用

要求懒猫微服系统 1.5.0 或更新版本。安装后创建管理员账号，在「账号配置」中登录小米账号并选择音箱。微服、音箱和投送设备需要在同一局域网，网络须允许 SSDP/mDNS 组播。

使用 host 网络；Web 管理端口为 8300，请保证端口空闲。持久化目录 `/lzcapp/var/data` 对应容器 `/app/data`，包含配置、数据库及账号凭据。关闭管理页面不停止投送服务。

## 构建和发布

```sh
mkdir -p dist
lzc-cli project release -o dist/application.lpk
lzc-cli lpk info dist/application.lpk
```

仅发布到喵喵商店，官方商店关闭。镜像通过 `docker.1ms.run` 加速，自动检查时验证 amd64 镜像摘要与 Docker Hub 一致。每日检查三段式稳定版本；首次手动执行工作流时填写 `0.6.0`。

工作流使用组织级 `APPSTORE_URL`、`APPSTORE_TOKEN` 和可选的 `PRIVATE_STORE_GROUP_CODES`。GitHub Release 文件名为 `community.lazycat.app.miair-next-v<version>.lpk`，喵喵商店引用该文件的下载地址及 SHA256。

本仓库不包含上游程序源码；应用许可证为 GPL-3.0-or-later，源码及第三方许可说明见上游仓库。
