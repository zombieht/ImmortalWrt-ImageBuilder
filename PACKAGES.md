# 第三方软件说明

本仓库仅保留 ImmortalWrt 25.12.x 构建，第三方软件使用 APK 包格式。

构建阶段已接入 dllkids 25.12 x86_64 预编译 APK 源：

```text
https://down.dllkids.xyz/openwrt-feed/25.12/x86_64/packages.adb
```

## 配置位置

- 第三方软件选择：`shell/apk-custom-packages.sh`
- 第三方 APK 整理：`shell/apk-prepare-packages.sh`

需要集成某个软件时，取消 `shell/apk-custom-packages.sh` 中对应 `CUSTOM_PACKAGES` 行的注释即可。

## 常见可选软件

| 软件包 | 说明 |
| --- | --- |
| `luci-app-store` | iStore 应用商店，可通过工作流 `enable_store` 开关自动集成 |
| `luci-i18n-quickstart-zh-cn` | 首页和网络向导 |
| `luci-app-adguardhome` | AdGuardHome DNS 去广告 |
| `luci-app-run` | Run 安装器 |
| `luci-app-quickfile` | 文件管理器 |
| `luci-theme-aurora` | Aurora 主题 |
| `luci-app-partexp` | 分区扩容 |
| `luci-app-bandix` | 流量监控 |
| `luci-app-mosdns` | DNS 分流，当前 25.12 x86-64 仓库未提供，默认不启用 |
| `luci-app-ssr-plus` | 代理工具 |
| `luci-app-passwall2` | 代理工具 |
| `luci-app-rtp2httpd` | IPTV 流媒体转发 |
| `luci-app-lucky` | 端口转发、反向代理等网络工具 |
| `luci-app-taskplan` | 任务计划 |

完整可选项以 `shell/apk-custom-packages.sh` 中的注释列表为准。
