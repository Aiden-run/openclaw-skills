---
name: boss-zhipin-hot-trend
description: >
  注册"BOSS直聘"热门技能；当需要访问或自动化BOSS直聘相关内容时调用。
  查询指定岗位的市场行情：薪资范围、技能要求、技术栈趋势。
  支持传统开发岗（Java/前端/Go）和 AI方向岗（算法/大模型/AI开发/Agent/机器学习等）。
  触发词：[关键词]行情怎么样/薪资待遇/技能要求/技术栈/BOSS直聘/最近行情
---

# BOSS直聘 岗位行情查询

查询指定岗位的招聘市场行情。**关键词由用户输入，替换 `[关键词]` 即可。**

## 什么时候用

✅ **用这个 skill 当用户说：**
- "Java 最近行情怎么样"
- "AI开发薪资待遇"
- "大模型岗技能要求"
- "Go行情" / "前端薪资"

❌ **不要用：** 投简历、跟HR聊天

## 数据采集

搜索 BOSS直聘 **职位详情页（job_detail）**，不搜列表聚合页。

### 多轮搜索

每轮约 15-20 条，多轮搜索合并去重，目标 100+ 条。**将命令中的 `[关键词]` 替换为用户输入：**

```bash
mcporter call 'exa.web_search_exa(query: "zhipin.com/job_detail [关键词] 开发 招聘", numResults: 20)'
mcporter call 'exa.web_search_exa(query: "zhipin.com/job_detail [关键词] 工程师 薪资", numResults: 20)'
mcporter call 'exa.web_search_exa(query: "zhipin.com/job_detail [关键词] 技术栈 招聘", numResults: 20)'
mcporter call 'exa.web_search_exa(query: "zhipin.com/job_detail [关键词] 月薪 招聘", numResults: 20)'
mcporter call 'exa.web_search_exa(query: "zhipin.com/job_detail [关键词] 2026 招聘", numResults: 20)'
mcporter call 'exa.web_search_exa(query: "zhipin.com/job_detail [关键词] 要求 职责", numResults: 20)'
mcporter call 'exa.web_search_exa(query: "zhipin.com/job_detail [关键词] 后端 开发", numResults: 20)'
mcporter call 'exa.web_search_exa(query: "zhipin.com/job_detail [关键词] 工程师 2026", numResults: 20)'
```

合并去重后，目标是 **100 条以上** job_detail 页面。

## 分析方法

AI 直接阅读每条 job_detail 原始描述，提取：薪资范围、技术栈要求、市场趋势。

## 输出格式

```
## [关键词] 招聘行情分析（样本数：xxx条）

### 薪资概览

### 技术栈要求

### 市场趋势
```

## 注意事项

- 数据来自搜索引擎公开索引的 job_detail 页面
- 薪资为税前参考范围
