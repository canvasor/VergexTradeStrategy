# VergeX 实战策略包（优化版）

这是在原始 `vergex_strategy_pack.zip` 基础上，吸收 v2 / v3 的关键优化点后重做的版本。
目标不是改成纯 AI500 包，而是 **保留原始多 Source Type、多层级策略结构**，同时修掉后续实操里暴露出来的几个关键问题。

## 这次重点优化了什么

### 1. 修正 UI 兼容性
- **只有 Custom 支持正向白名单**
- **非 Custom（AI500 / Netflow Top / OI Increase / Top Gainers / Top Losers 等）不支持正向白名单**
- **Excluded Coins 永远是黑名单**
- `Max Account Leverage` 统一改为当前 UI 更容易兼容的整数值，不再写 1.5x / 1.2x 这类小数

### 2. Prompt 逻辑更适合实盘
所有 Prompt 都加入了更明确的实战约束：
- 只交易当前 Source universe 里的币
- 不分析、不交易 `Excluded Coins`
- 没有有效机会时明确输出 `WAIT`
- 必须给出 invalidation 和至少 1:3 风险收益比
- 大多数周期允许 `WAIT / HOLD`
- 接近账户 hard stop 时优先保本

### 3. 保留原始分层结构，但把 AI500 经验并进去
原始包的优势是策略分层完整，适合从保守到激进逐级测试。
这版保留了 **S1-S7** 的结构，同时把后续 AI500 包里的这些经验融了进去：
- AI500 策略用 Prompt 写优先级，而不是误用 Excluded Coins
- 实测更需要 4H / 1H / 15m 的多周期分工
- 高频策略必须更强调“不交易条件”和“过度交易约束”

## 包内文件
- `VergeX_实战策略手册_优化版.docx`：完整中文手册
- `README_快速开始.md`：本文件
- `策略清单_稳定度排序.csv`：策略总表与排序
- `策略清单_详细版.md`：每个策略按 Studio 第 2-6 步展开
- `公开资料依据_说明.md`：公开资料来源、适用边界与实操提醒
- `版本优化说明.md`：本次相对原始包的改动摘要
- `prompts/`：7 份可直接复制进 Prompt Logic 的英文模板

## 推荐使用顺序
1. 先看 `VergeX_实战策略手册_优化版.docx`
2. 第一阶段先跑：
   - `prompts/S1_BTC_ETH_保守双周期趋势回撤_优化版.txt`
3. 第二阶段再考虑：
   - `prompts/S2_AI500_保守轮动_优化版.txt`
   - `prompts/S3_NetflowTop_资金流顺势_优化版.txt`
4. 更高波动策略放在后面：
   - `S4 / S5 / S6 / S7`

## 当前最重要结论
- **最适合第一次小仓实盘的仍然是 S1。**
- 如果你想在原始多策略框架里加入 AI500 的优势，最值得优先加的是 **S2**。
- 对所有非 Custom 策略：
  - Source Type 决定候选池
  - Excluded Coins 只做黑名单
  - 交易优先级写进 Prompt
- 高频和反转策略最容易因为 UI 误配、Prompt 不够硬、或过度交易而跑偏。

## 最小实盘建议
- 单策略先用小资金
- 第一阶段只开 1 套策略
- 优先用 `Isolated Margin`
- 每次只改 1 个变量
- 先观察几轮是否会频繁 `WAIT`
- 如果策略几乎每轮都要开仓，优先怀疑 Prompt 不够严格

> 本包是工程化落地方案，不是收益承诺，也不是个性化投资建议。
