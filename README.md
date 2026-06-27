# ImmortalWrt-ImageBuilder

本仓库仅保留 ImmortalWrt 25.12.x 的 x86-64 相关构建入口：

- `Build 25.12.x x86-64`：生成 x86-64 EFI 固件镜像。
- `Build 25.12.x ISO x86-64`：先生成 x86-64 EFI 固件，再封装为 ISO 安装器。

> 本项目为个人维护的第三方构建脚本，与 ImmortalWrt 官方没有关联。项目使用 ImmortalWrt 官方 ImageBuilder 打包生成固件，用户自行定制导致的问题不代表 ImmortalWrt 官方固件问题。

## 使用方式

1. Fork 本仓库。
2. 进入 GitHub Actions。
3. 选择以下工作流之一并点击 `Run workflow`：
   - `Build 25.12.x x86-64`
   - `Build 25.12.x ISO x86-64`
4. 按需设置构建参数：
   - `luci_version`：ImmortalWrt 25.12.x 版本。
   - `profile`：固件根分区大小，单位 MB，默认 `1024`。
   - `enable_store`：是否集成 iStore。
   - `include_docker`：是否集成 Docker 相关 LuCI 插件。
   - `enable_pppoe`、`pppoe_account`、`pppoe_password`：PPPoE 拨号配置。
   - `custom_router_ip`：仅 x86-64 固件工作流提供，用于多网口设备的 LAN 管理地址。

## 固件默认属性

- 单网口设备默认使用 DHCP 获取地址。
- 多网口设备默认 WAN 口使用 DHCP，LAN 管理地址默认为 `192.168.100.1`。
- 如果在工作流中启用 PPPoE，WAN 口会切换为 PPPoE 拨号模式。
- 默认用户名为 `root`，密码为空。
- 为方便首次调试，WAN 口防火墙入站默认放行。调试完成后，建议在 LuCI 的防火墙页面将 WAN 入站改为拒绝。

## 第三方软件

25.12.x 使用 APK 包格式。第三方软件配置集中在 `shell/apk-custom-packages.sh`，需要集成时取消对应行的注释即可。

如果在 GitHub Actions UI 中启用 `enable_store`，工作流会自动追加 `luci-app-store`，无需手动修改脚本。

## 目录说明

```text
.github/workflows/build-x86-64-25.12.x.yml  # x86-64 EFI 固件构建
.github/workflows/build-iso-25.12.x.yml     # x86-64 ISO 安装器构建
files/etc/uci-defaults/99-custom.sh         # 固件首次启动配置
shell/apk-custom-packages.sh                # 25.12.x 第三方 APK 包选择
shell/apk-prepare-packages.sh               # 第三方 APK 包整理脚本
x86-64/build25.sh                           # x86-64 25.12.x ImageBuilder 构建脚本
x86-64/imm25.config                         # x86-64 25.12.x ImageBuilder 配置
```

## 第三方 APK 源

构建脚本已接入 dllkids 25.12 x86_64 预编译 APK 源：

```text
https://down.dllkids.xyz/openwrt-feed/25.12/x86_64/packages.adb
```

该源只用于 ImageBuilder 构建阶段解析和下载预编译包。

## ISO 安装器说明

ISO 工作流会先构建 x86-64 EFI 固件，再调用 `wukongdaily/img-installer` 生成 ISO 安装器。ISO 启动后，在命令行输入 `ddd` 可进入安装菜单并选择目标磁盘。

## 相关文档

- [支持范围](SUPPORT.md)
- [第三方软件说明](PACKAGES.md)
