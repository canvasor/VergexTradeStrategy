# VergeX 运行数据驱动优化包 v6

这个包基于两类真实运行数据做升级：
- A1：解决长期不开单
- S3：保留稳定性，同时控制高保证金占用

## 目录结构
- `README_运行数据驱动优化包.md`
- `A1_S3_运行数据复盘.md`
- `策略总览_与切换条件.md`
- `策略排序_与切换矩阵.csv`
- `VergeX_运行数据驱动优化手册_v6.docx`
- `prompts/`

## 默认启用顺序
1. `S3_NetflowTop_资金流顺势_PRO_v2.txt`
2. `A1_AI500_双周期趋势回撤_PLUS_v2.txt`
3. `A2_AI500_社区Trend_PRO_v2.txt`

## 推荐初始配置
### A1 PLUS v2
- Source Type：AI500 Data Provider
- Decision Interval：30 min
- Position Mode：Isolated Margin
- Max BTC/ETH Leverage：4x
- Max Altcoin Leverage：2x
- Max Account Leverage：2x
- Hard Stop：12%
- K-Line：15m / 1h / 4h

### S3 PRO v2
- Source Type：Netflow Top
- Decision Interval：30 min
- Position Mode：Isolated Margin
- Max BTC/ETH Leverage：4x
- Max Altcoin Leverage：2x
- Max Account Leverage：2x
- Hard Stop：10%
- K-Line：15m / 1h / 4h

## 使用建议
- A1 如果连续 8-12 个周期都只看到极端拉升币，可把最极端、最重复的币临时加入 Excluded Coins。
- S3 如果保证金长期 >65%，先减相关暴露，再考虑开新仓。
