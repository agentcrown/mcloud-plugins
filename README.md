# mcloud · AgentCrown 新加坡多云比价

在你的 AI 工具里直接比较 **AWS、Azure、Google Cloud、阿里云、腾讯云、华为云** 新加坡区域的服务器价格。价格显示刊例价、你的专属折扣和折后价，并能生成报价单、提交购买意向。

使用前需要一把 **API key**，请向你的 AgentCrown 客户经理索取。**key 只属于你一个人，请不要分享给他人。**

## Claude Code

1. 先把 key 设成环境变量 `MCLOUD_API_KEY`：
   - Windows（PowerShell）：`setx MCLOUD_API_KEY "你的key"`，然后重新打开终端
   - macOS / Linux：在 `~/.zshrc` 或 `~/.bashrc` 里加一行 `export MCLOUD_API_KEY="你的key"`
2. 在 Claude Code 里安装插件：

```
/plugin marketplace add agentcrown/mcloud-plugins
/plugin install mcloud@mcloud
```

## Codex

1. 同样先设置环境变量 `MCLOUD_API_KEY`。
2. 把 [`codex/config.toml`](codex/config.toml) 的内容追加到 `~/.codex/config.toml`。
3. 把 [`generic/skills`](generic/skills) 里的全部文件夹复制到 `~/.agents/skills/`（Windows 是 `C:\Users\你的用户名\.agents\skills\`），这是 Codex 的个人 Skill 目录。

## Cursor

1. 把 [`generic/mcp.json`](generic/mcp.json) 的内容放进 `~/.cursor/mcp.json`（所有项目可用），或项目里的 `.cursor/mcp.json`（只对这个项目），把 `YOUR_MCLOUD_API_KEY` 换成你的 key。
2. 打开 Cursor 的 **Customize → MCPs**，点 mcloud。**放在项目里的配置默认是关闭的**，要把开关打开；看到绿点和"4 tools enabled"就好了。
3. Cursor 会自动读取 `~/.claude/skills` 里的 Skill（`~/.codex/skills` 也会读），把 [`generic/skills`](generic/skills) 里的全部文件夹放进 `~/.claude/skills` 即可。

## OpenClaw 等其他支持 MCP 的工具

1. 在工具的 MCP 设置里导入 [`generic/mcp.json`](generic/mcp.json)，把里面的 `YOUR_MCLOUD_API_KEY` 换成你的 key。
2. 如果工具支持 Skill，把 [`generic/skills`](generic/skills) 里的全部文件夹放进它的 skills 目录。

## 试一下

装好后，在对话里问：

> 新加坡 4 核 16G 的服务器，哪家云最便宜？

## 连不上怎么办

- **显示 "Failed to connect … HTTP 401"**：key 没设置或设置错了。检查环境变量 `MCLOUD_API_KEY`；Windows 用 `setx` 设置后，要**重新打开终端和 Claude / Codex** 才会生效。
- key 确认无误仍然连不上，请联系客户经理重新发一把。

## 说明

- 报价为参考价，不含税、公网 IP 和技术支持费，有效期 7 天，**最终价格以合同为准**。
- 提交购买意向后，你的客户经理会在一个工作日内联系你。本服务不会替你开通或删除任何云资源。

---

## English

Compare Singapore server prices across AWS, Azure, Google Cloud, Alibaba Cloud, Tencent Cloud and Huawei Cloud from your AI tool: list price, your discount and final price, quotes, and purchase requests. You need an API key from your AgentCrown account manager.

**Claude Code:** set the `MCLOUD_API_KEY` environment variable, then run
`/plugin marketplace add agentcrown/mcloud-plugins` and `/plugin install mcloud@mcloud`.

**Codex:** set `MCLOUD_API_KEY`, append [`codex/config.toml`](codex/config.toml) to `~/.codex/config.toml`, and copy the folders in [`generic/skills`](generic/skills) into `~/.agents/skills/`.

**Other MCP clients:** import [`generic/mcp.json`](generic/mcp.json) with your key filled in.

"Failed to connect … HTTP 401" means the key is missing or wrong; after `setx` on Windows, restart your terminal and AI tool.

Quotes are indicative, exclude taxes, public IPs and support, are valid for 7 days, and are final only under contract.
