# 📱 FlClash 防泄露 + 广告拦截配置

适用于 **FlClash**（Mihomo 内核）的完整分流配置文件，支持多订阅节点自动聚合、按地区分类、服务专属策略组、DNS 防泄露以及强大的广告拦截功能。专为 Android 64 位设备优化，也可用于其他平台的 Clash Meta 客户端。

---

## ✨ 特性

- **🛡️ DNS 防泄露**：Fake‑IP 增强模式，国内使用阿里/腾讯 DoH，国外使用 Google DoH，杜绝 DNS 泄露。
- **🧹 广告拦截**：集成 [anti-AD](https://github.com/privacy-protection-tools/anti-AD) 规则集，过滤大量广告、跟踪器，提升浏览体验。
- **🌐 多订阅聚合**：支持同时添加多个机场订阅，节点自动合并到统一池中。
- **🗂️ 节点分类**：按地区（🇭🇰香港、🇯🇵日本、🇸🇬狮城、🇺🇸美国）自动提取节点，并提供故障转移（Fallback）与自动测速（URL‑Test）策略组。
- **🎯 服务分流**：为 YouTube、Google、ChatGPT、GitHub、Netflix、Telegram 等常用服务设置独立策略组，候选节点丰富灵活。
- **📱 Android 优化**：开启 TUN 模式（mixed 栈），支持所有应用流量接管；针对国内应用（如米家、Apple Push）优化嗅探跳过。

---

## 📁 文件说明

```
.
└── config-rule.yaml    # 主配置文件，直接导入 FlClash 使用
```

您只需要这一个文件即可完成全部设置。

---

## 🚀 快速上手

### 1️⃣ 下载客户端
- 从 [FlClash Releases](https://github.com/chen08209/FlClash/releases) 下载 **arm64‑v8a** 版本的 APK 安装包。
- 其他平台（Windows/macOS/Linux）需使用 Clash Meta 内核的客户端，并导入本配置。

### 2️⃣ 获取配置文件
- 点击本仓库的 `config-rule.yaml` 文件，复制内容或直接下载整个仓库。
- 如果您有个性化需求，可以 Fork 后自行修改。

### 3️⃣ 导入配置
- 打开 FlClash → **设置** → **配置管理** → **导入**，选择 `config-rule.yaml`。
- 导入后会在配置列表中显示，点击激活。

### 4️⃣ 修改订阅链接
- 在激活的配置中，点击 **编辑**（或在文件管理器打开），找到 `proxy-providers` 部分。
- **将 `url: "https://你的订阅链接1"` 替换为你自己的机场订阅地址（支持多个）。**
- 保存并返回。

### 5️⃣ 更新并启动
- 在配置管理页面点击 **更新订阅**（等待完成后，节点列表会出现）。
- 再点击 **更新规则集**（下载所有分流规则，首次可能需要几分钟，之后自动定期更新）。
- 返回主界面，切换到 **规则模式**，开启代理。
- 确保 TUN 已启用（配置中默认开启），即可接管所有网络流量。

---

## ⚙️ 自定义指南

### 🧩 调整策略组
所有服务专属策略组（如 ChatGPT、Netflix）目前使用与 YouTube 相同的候选列表，您可以根据需要修改每个 `proxy-groups` 下的 `proxies` 项。

### 📌 添加国内应用直连
若某些国内应用异常，可在 `rules` 段内添加 `PROCESS-NAME` 规则：
```yaml
- PROCESS-NAME,com.tencent.mm,直连   # 微信
- PROCESS-NAME,com.alibaba.android.rimet,直连  # 钉钉
```

### 🕵️ 调整广告拦截强度
- 规则集中 `anti_ad` 默认使用 anti-AD 列表。若觉得误杀过多，可切换 `🛑 广告拦截` 策略为 **直连**。
- 如需更换规则源，修改 `rule-providers` 下 `anti_ad` 的 `url`，例如使用 [ACL4SSR](https://github.com/ACL4SSR/ACL4SSR) 的列表。

### 📶 性能优化（低配手机）
- 增大测速间隔：将 `url-test` 中的 `interval: 300` 改为 `600` 或更大。
- 删除不常用的策略组，减少内存占用。

## ⚠️ 注意事项

- **节点名称匹配**：自动分类依赖正则表达式，请确保您的节点名称中包含“香港”、“日本”、“US”等关键词，否则无法被归入对应分组。
- **订阅格式**：本配置只接受 Clash 格式的订阅。若机场提供的是 SS/SSR/V2Ray 链接，请先用 [subconverter](https://github.com/tindy2013/subconverter) 转换。
- **规则集更新**：首次使用时请确保网络能正常访问 GitHub 源，否则规则集下载失败。可手动替换为国内镜像。

---

## 📜 致谢
- 参考模板作者 [qichiyuhub](https://github.com/qichiyuhub)
                       
