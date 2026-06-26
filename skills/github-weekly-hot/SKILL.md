---
name: github-weekly-hot
description: >
  每周五自动采集 GitHub 本周热门项目 Top 10。
  用自然的中文写成博客简报风格输出。
  触发词：GitHub热门/GitHub周报/本周热门项目/这周GitHub有什么。
---

# GitHub 每周热门 Top 10

每周五采集 GitHub 当周最火的开源项目，整理成表格简报。

## 什么时候用

✅ **用这个 skill 当用户说：**
- "这周 GitHub 有什么热门"
- "GitHub 周报"
- "本周热门项目"
- "GitHub top 10"

❌ **不要用这个 skill 当用户说：**
- "查某个具体仓库" → 用 GitHub 仓库查询
- "GitHub 趋势日报" → 这是每日数据，不是周报

## 数据源

### 主数据源：GitHub Trending 周榜（唯一准确数据源）

```bash
# 使用浏览器打开 GitHub Trending 周榜（sandbox 浏览器可直达）
# https://github.com/trending?since=weekly
browser action="open" url="https://github.com/trending?since=weekly" target="sandbox"
browser action="snapshot" compact=true
```

> ✅ GitHub Trending 页面国内 `web_fetch` 会超时，但 **sandbox 浏览器可正常访问**。每个 article 标签对应一个项目，包含：
> - 项目名（heading 里的 link）
> - 描述（paragraph）
> - 编程语言
> - 总星数
> - **本周新增星数（关键！）**：`X stars this week`
> - 作者信息

### 备选：GitHub API Search

当浏览器不可用时使用：

```bash
# 本周新建项目（无法复现 Trending 算法，只作备选）
web_fetch "https://api.github.com/search/repositories?q=created:>$(date -d '7 days ago' +%Y-%m-%d)+stars:>100&sort=stars&order=desc&per_page=15"
```

### 二次备选：Trendshift

- https://trendshift.io/weekly

> ⚠️ GitHub Trending 页面返回的是按**本周新增 star 数**排序的真实热门项目（包含老项目），这是 API 无法精确复现的。浏览器是推荐的首选数据源。

## 输出格式

```
# GitHub 本周热门 Top 10

| # | 项目 | ⭐ | 简介 |
|:-:|:----|:--:|:-----|
| 🥇 | [project](link) | x,xxx | 一句话简介 |
| 🥈 | [project](link) | x,xxx | 一句话简介 |
| 🥉 | [project](link) | x,xxx | 一句话简介 |
| 4 | [project](link) | x,xxx | 一句话简介 |
| ... | ... | ... | ... |

---

**趋势小结：** 概括当周主要方向和亮点。
```

### 要求
- 简介一句话，**说清楚项目是干嘛的**
- 项目名做成超链接
- top 3 序号用 emoji（🥇🥈🥉）
- 最后加 **趋势小结**，自然中文，不要翻译腔

## 注意事项

- 只看 **当周新建或爆发式增长** 的项目
- 如果某个项目连续上榜，标注「连续上榜」
- 数据抓不到时给简短说明，不要空着
