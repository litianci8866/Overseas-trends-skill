# 🌐 Overseas Trends — 海外社媒热榜周报

**A Claude Code Skill** | 每周自动抓取海外社媒热点，生成结构化周报，一键发送飞书

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Platform](https://img.shields.io/badge/Platform-Claude%20Code-blue)](https://claude.ai/code)

---

## 这是什么 / What is this

一个为**游戏行业运营、品牌人、内容创作者**设计的 Claude Code Skill。

想要追上海外热梗但又苦于IP问题没法天天刷到本地爆款？社媒API付费和接入问题让监测成本大大增加？

本skill每周自动抓取 TikTok、Twitter/X、Reddit、Instagram 上的爆款音乐、流行梗、病毒式挑战

使用Trends MCP，每月100免费额度，快乐收集热点！

最后AI还会特别附带「**游戏官号可蹭热点速查**」板块，帮你找到最适合游戏账号追梗的内容，整理成结构化周报，一键发送到飞书。


**覆盖平台：** TikTok · Twitter/X · Reddit · Instagram · Facebook · Discord

**不收录：** 时政新闻、品牌付费推广、单日昙花一现的内容

---

## 功能亮点 / Features

- 🎵 **TikTok 热榜** — 爆款音乐、流行模板、病毒式 meme，含播放量数据
- 🐦 **Twitter/X 热搜** — 跨国热搜话题追踪（美国 + 英国）
- 👾 **Reddit 热帖** — 跨版块热帖与梗起源溯源
- 📸 **Instagram 趋势** — 热门 Reels 格式、视觉美学趋势
- 🎮 **游戏官号可蹭热点速查** — 从本周热点中筛选最适合游戏账号跟拍的内容，附执行思路
- 🔄 **跨期去重** — 自动对比上期内容，不重复收录已报热点
- 📨 **一键发飞书** — 支持个人消息和群聊，格式自动适配

---

## 输出示例 / Sample Output

```
海外社媒热榜 2026年4月15日 - 4月22日

🌐 跨平台热点

1. KitKat Heist 巧克力大劫案
   · 平台 & 数据：Reddit /r/memes 原发帖 upvote 16,000+；Twitter 相关推文超 25 万条
   · 走红原因：欧洲真实货车劫案——12吨KitKat失窃，荒诞数字引爆全网
   · 传播形态：品牌"官方声明"格式跟梗；游戏公司参战（Hitman、Cut the Rope）
   🔗 https://knowyourmeme.com/memes/events/kitkat-heist

🎵 TikTok 热榜

1. BTS "SWIM" Dive Challenge
   · 平台 & 数据：V 原视频 6.9M 播放、5.85M 点赞；#btsswim 持续飙升
   · 走红原因：BTS 回归单曲，V 发布飞扑镜头视频，粉丝批量复刻
   · 传播形态：第一人称飞扑跟拍挑战
   🔗 https://www.tiktok.com/music/SWIM-7618900230566119425

...（完整示例见 references/template.md）
```

---

## 安装 / Installation

**第一步：下载 Skill**

```bash
# 克隆仓库到 Claude Code skills 目录
git clone https://github.com/litianci8866/overseas-trends \
  ~/.claude/skills/overseas-trends
```

或直接下载 ZIP 解压到：
```
C:\Users\{你的用户名}\.claude\skills\overseas-trends\
```

**第二步：配置飞书发送脚本**

参考 [follow-builders](https://github.com/zhang-changelog/follow-ai-builder) 项目配置飞书 webhook，确认以下脚本路径存在：

```
~/.follow-builders/send_to_me.py     # 发送到个人飞书
~/.follow-builders/send_to_group.py  # 发送到群聊
```

**第三步：创建输出目录**

```bash
mkdir -p ~/.claude/skills/overseas-trends/output
```

**第四步（可选）：接入 Trends MCP**

Trends MCP 可提供 12 个平台的实时热度数据，大幅提升热点验证准确性。免费 100 次/月。

```bash
# 先在 trendsmcp.ai 注册获取 API Key
claude mcp add --transport http trends-mcp https://api.trendsmcp.ai/mcp \
  --header "Authorization: Bearer 你的API_KEY"
```

然后在 `~/.claude/settings.json` 中启用：

```json
{
  "enabledMcpjsonServers": ["trends-mcp"]
}
```

---

## 使用方法 / Usage

在 Claude Code 中直接触发：

```
海外热榜         # 生成本周周报
海外趋势         # 同上
overseas trends  # 同上
/overseas-trends # 直接调用
```

生成完成后确认，发送到飞书：

```
发我      # 发送到个人飞书（默认）
发群      # 发送到群聊
```

---

## 文件结构 / File Structure

```
overseas-trends/
├── SKILL.md                    # Skill 主文件，完整执行流程
├── references/
│   ├── template.md             # 周报输出模板（板块结构 + 格式规范）
│   └── sources.md              # 各平台数据源配置（WebFetch URL + 搜索关键词）
├── output/                     # 历史周报存档（自动生成，用于跨期去重）
│   └── YYYY-MM-DD-YYYY-MM-DD.md
└── README.md
```

---

## 环境要求 / Requirements

| 依赖 | 版本 | 说明 |
|------|------|------|
| Claude Code | 最新版 | 需已安装并登录 |
| Python | 3.9+ | 用于飞书发送脚本 |
| Trends MCP | 可选 | 提升热度验证准确性 |
| 网络 | 可访问海外 | Reddit、TikTok discover、KnowYourMeme |

---

## License

MIT — 自由使用、修改、分发，保留署名即可。

---

*Made with Claude Code · 如有问题欢迎提 Issue*
