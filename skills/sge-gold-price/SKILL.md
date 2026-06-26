---
name: sge-gold-price
description: >
  MUST USE when user asks for 黄金价格/金价/大盘价/今日金价/Au99.99/上金所/上海黄金交易所.
  Queries Shanghai Gold Exchange H5 delayed quote page for real-time precious metal prices.
  NOT for: 国际金价（伦敦金/纽约金）、银行金条价格、金店回收价——这些是不同维度的价格。
homepage: https://www.sge.com.cn/h5_sjzx/yshq
---

# 上海黄金交易所延时行情查询

查询上海黄金交易所 Au99.99 等品种的当日延时行情，包括最新价、开盘价、最高价、最低价。

## 什么时候用

✅ **用这个 skill 当用户说：**
- "黄金价格多少" / "今日金价"
- "大盘价" / "Au99.99"
- "上金所行情"

❌ **不要用这个 skill 当用户说：**
- "国际金价" / "伦敦金" → 这是国际现货黄金，不同市场
- "银行金条多少钱" → 银行金价含手续费，比基准价高
- "金店回收价" → 回收价是另一个体系

## 数据源

```bash
# 今日延时行情（唯一数据源）
web_fetch https://www.sge.com.cn/h5_sjzx/yshq
```

返回字段：最新价、今开盘、最高价、最低价

## 输出格式

| 合约 | 最新价 | 今开盘 | 最高 | 最低 |
| Au99.99 | ¥xx | ¥xx | xx | xx |

**Au99.99 是基准价，必须包含。**

可选品种：Au(T+D)、mAu(T+D)、Au100g、Au99.95

## 注意事项

- 上金所数据为 **延时行情**，非实时成交价
- 银行挂牌价在 Au99.99 基础上加手续费和点差，有差异正常
- 市场收盘后（15:30），最新价即为当日收盘价
- 若页面无法访问，推荐用户打开手机银行查看
