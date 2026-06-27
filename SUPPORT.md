# 支持范围

本仓库当前只保留 ImmortalWrt 25.12.x 的 x86-64 相关构建。

| 工作流 | 输出类型 | 适用范围 | LuCI 版本 |
| --- | --- | --- | --- |
| `Build 25.12.x x86-64` | `squashfs-combined-efi.img.gz` | Intel / AMD x86-64 设备，EFI 启动 | 25.12.x |
| `Build 25.12.x ISO x86-64` | `custom-installer-x86_64.iso` | 虚拟机或物理机安装器，启动后输入 `ddd` 安装 | 25.12.x |

## 默认网络行为

- 单网口设备默认使用 DHCP。
- 多网口设备默认 WAN 使用 DHCP，LAN 管理地址默认 `192.168.100.1`。
- 启用 PPPoE 后，WAN 会改为 PPPoE 拨号。

其它平台和 24.10.x 相关工作流已从本仓库移除。
