# Relay 固件发布

这里提供基于 OpenWrt 的 Relay 固件，面向以 **x86/64、UEFI、ext4** 运行的虚拟路由器。镜像预装 Relay 管理界面、Pearl 主题、PassWall 和 KMS 组件。新安装时使用通用配置。

## 检查更新

在已配置本通道的 Relay 界面打开 **更新 → 检查自家固件**。候选版标有「仅供测试」，适合在独立虚拟机中试用。正式版通过同一入口提供。固件版本和下载文件也可在 [Releases](https://github.com/sweet0416/relay-firmware/releases) 查看。

OpenWrt 原生「有人值守系统升级」（Attended Sysupgrade）使用独立的构建服务 API。请保留其服务器设置，通过 Relay 访问本发布通道。

## 手动核验

从同一 Release 下载镜像、`packages.manifest`、`vm124-release.json` 和 `vm124-release.json.sig`。以设备中预置的可信公钥核对签名，或使用已独立核对过的[公钥副本](firmware-release.pub)。

```sh
usign -V -p /usr/share/relay-ui/firmware-release.pub -m vm124-release.json -x vm124-release.json.sig
```

验签通过后，用 `sha256sum` 计算镜像和软件包清单的 SHA-256，分别核对签名清单中的 `sha256` 和 `packages_sha256`。安装正式版前，先备份虚拟机，再使用 LuCI 的「备份与刷写」上传已核验的镜像。实际刷写会重启路由器。

## 上游项目

- [OpenWrt 源码](https://github.com/openwrt/openwrt) 与 [OpenWrt 官方发行文件](https://downloads.openwrt.org/releases/)
- [PassWall](https://github.com/Openwrt-Passwall/openwrt-passwall)、[附加软件包源码](https://github.com/Openwrt-Passwall/openwrt-passwall-packages) 与 [二进制软件源](https://github.com/moetayuko/openwrt-passwall-build)
- [vlmcsd 软件包来源](https://github.com/arition/openwrt-repo)
