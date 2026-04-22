# 海外社媒热榜数据源配置

## TikTok

| 项目 | 内容 |
|------|------|
| 发现页 | https://www.tiktok.com/discover |
| 抓取方式 | WebFetch 直接抓取（部分内容需配合 WebSearch 补全） |
| Trends MCP | source=tiktok，追踪话题标签热度增长 |
| 补充搜索 | `TikTok trending {sound/challenge/meme} {日期范围}` |
| 热门音乐追踪 | `TikTok viral song week {日期范围} site:billboard.com` |
| 定位 | 爆款音乐/音效、流行挑战模板、病毒式 meme |

## Twitter / X

| 项目 | 内容 |
|------|------|
| 美国热搜 | https://trends24.in/united-states/ |
| 英国热搜 | https://trends24.in/united-kingdom/ |
| 抓取方式 | WebFetch 直接抓取（trends24.in 可用） |
| 补充搜索 | `Twitter trending topics this week {日期范围}` |
| 定位 | 实时热搜话题、出圈讨论、大规模转推事件 |
| 筛选标准 | 热搜维持 6 小时以上，或转推量 > 5万 |

## Reddit

| 项目 | 内容 |
|------|------|
| 全站周 Top | https://www.reddit.com/r/all/top/?t=week |
| Memes | https://www.reddit.com/r/memes/top/?t=week |
| Dank Memes | https://www.reddit.com/r/dankmemes/top/?t=week |
| Gaming | https://www.reddit.com/r/gaming/top/?t=week |
| 抓取方式 | WebFetch 直接抓取（Reddit 对境外 IP 开放） |
| 补充搜索 | `Reddit viral post meme {日期范围} site:reddit.com` |
| 定位 | 跨版块热帖、流行梗起源、大规模讨论 |
| 筛选标准 | upvote > 5万 或 评论量 > 2000 或跨平台传播 |

## Instagram

| 项目 | 内容 |
|------|------|
| 抓取方式 | WebSearch（Instagram 不开放直接抓取） |
| 热门 Reels 搜索 | `Instagram Reels trending {日期范围}` |
| 热门话题标签 | `Instagram trending hashtag {日期范围}` |
| Trends MCP | source=google search，追踪 `instagram trend [话题]` 搜索增长 |
| 定位 | 热门 Reels 格式、视觉美学趋势、爆款话题标签 |
| 筛选标准 | Reel 播放量 > 100万，或话题标签本周新增帖子量显著飙升 |

## Facebook

| 项目 | 内容 |
|------|------|
| 抓取方式 | WebSearch（Facebook 不开放直接抓取） |
| 搜索关键词 | `Facebook viral video/post {日期范围}` |
| 定位 | 大规模传播的病毒视频、跨年龄层热点 |
| 备注 | 仅收录有明确跨平台传播证据的内容，Facebook 单平台内容通常不单独列条 |

## Discord

| 项目 | 内容 |
|------|------|
| 抓取方式 | WebSearch（Discord 无公开 API，通过 Reddit 二次传播追踪） |
| 搜索关键词 | `Discord trending meme/topic {日期范围} site:reddit.com` |
| 定位 | 游戏社区、亚文化圈层梗，流出后在 Reddit/TikTok 大规模传播 |
| 备注 | Discord 原生内容通常不收录，须有公开平台二次传播才计入 |

## Trends MCP 使用配置

| 用途 | 参数 |
|------|------|
| TikTok 话题热度 | source=tiktok，percent_growth=[7D, 30D] |
| Google 搜索验证 | source=google search，验证话题是否扩散到主流 |
| 新闻体量验证 | source=news volume，确认有媒体报道 |

## 辅助参考网站（WebFetch 可用）

| 网站 | 用途 |
|------|------|
| https://knowyourmeme.com/memes/recent | 近期新梗追踪，最可靠的梗数据库 |
| https://trends24.in/united-states/ | Twitter/X 美国热搜历史记录 |
| https://www.reddit.com/r/all/top/?t=week | Reddit 全站周榜 |
| https://charts.spotify.com/charts/overview/global | Spotify 全球歌曲榜（TikTok 音乐交叉验证）|
