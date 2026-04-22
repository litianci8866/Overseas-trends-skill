---
name: overseas-trends
description: 海外社媒热榜周报生成器。每周抓取 TikTok、Instagram、Reddit、Twitter/X、Facebook、Discord 上的热门话题、流行梗、爆款音乐/模板，整理成结构化周报发送到飞书。触发关键词：海外热榜、海外趋势、overseas trends。
---

# 海外社媒热榜周报

## 任务目标

抓取过去 7 天（含今天）海外主流社媒平台的热门内容，整理成结构化周报。优先级顺序：**TikTok > Twitter/X > Reddit > Instagram > Facebook/Discord**。

重点关注：
- TikTok 爆款音乐、流行模板、病毒式 meme
- Twitter/X 热搜话题、出圈讨论
- Reddit 跨版块热帖、流行梗
- Instagram 热门 Reels、流行视觉趋势
- Facebook/Discord 有规模传播的话题

**不收录**：新闻事件本身（时政归国内周报）、品牌付费推广内容、单日昙花一现的内容（须有持续传播证据）。

---

## 执行步骤

### 第一步：确定时间范围 & 读取上期内容

明确本次周报起止日期（今天往前推 7 天），所有搜索和内容判断严格遵守此范围。

**读取上期周报（用于跨期去重）**：

检查输出目录 `C:\Users\litianci\.claude\skills\overseas-trends\output\` 是否存在历史文件，读取**最近 2 期**（防止隔期重复收录）：

```bash
ls C:\Users\litianci\.claude\skills\overseas-trends\output\ | sort -r | head -2
```

若存在，用 Read 工具逐一读取，提取其中已收录的所有热点名称，合并构建「已收录清单」，后续抓取时对照去重。若目录不存在或无文件，跳过此步。

### 第二步：按平台分类抓取

#### 1. TikTok（最高优先级）

**爆款音乐 / 音效**
- Trends MCP：`get_growth` source=tiktok，搜索本周热门 sound/song 关键词
- WebSearch：`TikTok trending sound/audio {本周日期范围}`
- WebSearch：`TikTok viral music week {本周日期范围} site:billboard.com OR site:musicweek.com`

**流行模板 / 挑战**
- WebSearch：`TikTok trending challenge/template/trend {本周日期范围}`
- WebSearch：`TikTok new trend this week {本周日期范围}`
- WebFetch：`https://www.tiktok.com/discover`（直接抓取发现页，筛选热榜标签）

**病毒式 Meme**
- WebSearch：`TikTok meme viral {本周日期范围}`
- WebSearch：`TikTok trending meme format {本周日期范围} site:knowyourmeme.com`

筛选标准：视频播放量 > 500万 或 话题标签 > 1亿播放，或跨平台被二次传播。

#### 2. Twitter / X（次高优先级）

**实时热搜**
- WebFetch：`https://trends24.in/united-states/`（美国实时 Twitter 热搜，可直接抓取）
- WebFetch：`https://trends24.in/united-kingdom/`（英国）
- WebSearch：`Twitter trending topics this week {本周日期范围}`

**出圈话题 / 讨论**
- WebSearch：`Twitter/X viral tweet thread {本周日期范围}`
- WebSearch：`X.com trending discussion meme {本周日期范围}`

筛选标准：话题须在热搜榜维持 6 小时以上，或转推量 > 5万。

#### 3. Reddit（热帖 + 流行梗）

**跨版块热帖**
- WebFetch：`https://www.reddit.com/r/all/top/?t=week`（本周全站 Top，可直接抓取）
- WebFetch：`https://www.reddit.com/r/memes/top/?t=week`
- WebFetch：`https://www.reddit.com/r/dankmemes/top/?t=week`

**流行梗溯源**
- WebSearch：`Reddit meme origin this week {本周日期范围}`
- WebSearch：`Reddit viral post {本周日期范围} site:reddit.com`

筛选标准：帖子 upvote > 5万，或评论量 > 2000，或被其他平台二次传播。

#### 4. Instagram

**热门 Reels / 话题标签**
- WebSearch：`Instagram Reels trending this week {本周日期范围}`
- WebSearch：`Instagram trending hashtag {本周日期范围}`
- Trends MCP：`get_growth` source=google search，关键词 `instagram trend [话题]`

**视觉流行趋势**
- WebSearch：`Instagram aesthetic trend {本周日期范围}`
- WebSearch：`Instagram viral reel format {本周日期范围}`

筛选标准：Reel 播放量 > 100万，或话题标签新增帖子量本周显著飙升。

#### 5. Facebook / Discord（补充）

**Facebook**
- WebSearch：`Facebook trending video/post {本周日期范围}`
- WebSearch：`Facebook viral content {本周日期范围}`

**Discord**
- WebSearch：`Discord trending meme/topic {本周日期范围} site:reddit.com`（Discord 内容多在 Reddit 二次传播）
- WebSearch：`Discord viral {本周日期范围}`

筛选标准：仅收录有实质跨平台传播证据的内容，Discord 单平台内部讨论不收录。

### 第三步：交叉验证与去重

- 同一内容在多平台传播，合并为一条，标注「跨平台」
- Trends MCP `get_growth` 交叉验证热度增长（source=tiktok / google search）：**7D 增长 > 30% 视为热度上升确认；低于此或无数据则依赖多源搜索结果综合判断**
- 7 天内无新高峰、已明显降温的内容不收录
- 每条内容必须有：名称、平台来源、走红原因、传播形态、可验证链接（至少 1 条直链）

**跨期去重**：对照第一步构建的「已收录清单」，已收录的内容本期不再收录，除非本期有明显新的爆发节点（如话题量比上期翻倍、出现新的二创浪潮、跨平台扩散至新平台）。若有新发展，收录时注明「续」并说明新动态。

### 第四步：按模板生成周报

参考 [references/template.md](references/template.md) 生成最终输出。

**写作规范**：
- 标题：一句话概括内容核心（英文梗附中文说明）
- 子弹点用「·」
- 数据优先：播放量、搜索增长量、转推数等量化指标必须写入
- 链接：有直链则附，无直链不放搜索入口替代

### 第五步：保存本期输出

将最终周报保存为 Markdown 文件，供下期去重使用：

```bash
# 文件名格式：起始日期-截止日期.md（例：2026-04-14-2026-04-21.md）
# 保存路径：C:\Users\litianci\.claude\skills\overseas-trends\output\
```

用 Write 工具将完整周报内容写入对应文件。若 output 目录不存在，先创建：

```bash
mkdir -p /c/Users/litianci/.claude/skills/overseas-trends/output
```

### 第六步：发送到飞书

生成草稿后发给用户确认，确认后发送到个人飞书：

```bash
py -3 -X utf8 C:\Users\litianci\.follow-builders\send_to_me.py
```

如用户说「发群」，则发送到群聊：

```bash
py -3 -X utf8 C:\Users\litianci\.follow-builders\send_to_group.py
```
