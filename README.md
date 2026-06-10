# 好多DNS

一站式公共 DNS 服务器大全，支持快速筛选、一键复制参数，配合测速工具选出最适合你的 DNS。

## 数据来源

本仓库维护了一份全面的公共 DNS 服务器列表（`custom_dns.json`），涵盖：

- **国内推荐 DNS** — 阿里DNS、腾讯DNS、114DNS、百度DNS 等
- **国外推荐 DNS** — Cloudflare、Google、OpenDNS、Quad9 等
- **国内运营商 DNS** — 中国电信/联通/移动各省 DNS
- **自建 DNS** — 个人/社区维护的 DoT/DoH 服务器

每条记录包含：IPv4 / IPv6 地址、DoH URL、DoT 主机、推荐值、描述等字段。

## 使用方法

### 1. 在线浏览

直接打开 `dns-dashboard.html`，或通过本地服务器访问：

```bash
python -m http.server 8080
# 打开 http://localhost:8080/dns-dashboard.html
```

页面功能：
- **筛选** — 按协议（DoH / DoT / DoQ）或类型（自定义/内置）过滤
- **搜索** — 按名称关键词搜索
- **复制** — 点击参数旁的 📋 复制单个值，或点「复制全部」复制整行
- **推荐排序** — 按推荐值降序排列，前三名显示 🥇🥈🥉

### 2. 本地测速

配合 [DnsSpeedTestApp](https://github.com/xihan123/DnsSpeedTestApp/releases) 进行延迟测试：

1. 下载并解压 [DnsSpeedTestApp](https://github.com/xihan123/DnsSpeedTestApp/releases)
2. 将本仓库的 `custom_dns.json` 复制到测速工具目录：

```bash
copy custom_dns.json "%USERPROFILE%\AppData\Local\DNSSpeedTester\custom_dns.json"
```

3. 运行 DnsSpeedTestApp，它会自动读取该 JSON 文件中的 DNS 服务器进行测速
4. 根据测速结果，筛选出延迟最低的 DNS 配置到你的设备

### 3. 客户端配置

测出最快的 DNS 后，在客户端配置 DoH/DoT 使用：

| 平台 | 推荐工具 | 说明 |
|------|----------|------|
| **Android** | [18bit DNS 客户端](https://down.18bit.cn/) | 支持 DoH，轻量易用 |
| **Windows** | [YogaDNS](https://www.yoganetworks.com/yogadns/) | 支持 DoH/DoT，全局接管系统 DNS |

> **提示：** 你可以编辑 `custom_dns.json` 中的 `Score` 字段（数字越大越推荐）和 `Desc` 字段（描述信息），修改后重新复制到测速工具目录即可生效。

## 文件结构

```
├── custom_dns.json       # DNS 服务器数据（JSON 格式）
├── dns-dashboard.html    # 在线浏览页面（单 HTML 文件）
├── parse_dns.py          # 文本转 JSON 解析脚本
└── merge_dns.py          # JSON 合并脚本
```

## JSON 字段说明

```json
{
  "Name": "服务器名称",
  "PrimaryIPString": "主 IP 地址",
  "SecondaryIPString": "备用 IP 地址（多个用空格分隔）",
  "IPv6String": "IPv6 地址（多个用空格分隔）",
  "IsCustom": true,
  "DohUrl": "DoH URL",
  "DotHost": "DoT 主机地址",
  "DotPort": 853,
  "DoqHost": "DoQ 主机地址",
  "DoqPort": 853,
  "Score": 5,
  "Desc": "描述信息"
}
```

## 自定义推荐值

编辑 `custom_dns.json`，为每条 DNS 设置 `Score` 值：

| 分数 | 含义 |
|------|------|
| 10 | ⭐ 强烈推荐 |
| 8 | 👍 推荐 |
| 5 | ✅ 可用 |
| 1 | ℹ️ 一般 |
| null | 不评分 |

页面会按 Score 降序排列，前三名显示金银铜牌 🥇🥈🥉。

## 参考

- DNS 数据来源：[ToolB 公共 DNS 大全](https://toolb.cn/publicdns)
- 测速工具：[xihan123/DnsSpeedTestApp](https://github.com/xihan123/DnsSpeedTestApp)

## License

MIT
