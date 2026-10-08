# 野蛮时代用户数据分析（SQL + pyecharts）

基于 tap4fun《野蛮时代》手游用户数据集的数据分析项目。使用 Python(pandas) 完成数据清洗入库，在 MySQL 中完成用户、活跃度、付费、游戏习惯四个维度的 SQL 分析，并用 pyecharts 输出可视化。

## 数据集

- 来源：tap4fun 野蛮时代用户数据集（比赛数据，train + test 两个文件）
- 规模：合计约 861 MB，3,116,941 条记录，109 个字段
- 字段说明见 `tap4fun竞赛数据/字段说明.xlsx`
- 原始 CSV 体积过大且版权归比赛方所有，不随仓库上传，本地保留

## 技术栈

Python / pandas / SQLAlchemy → MySQL → SQL 分析 → pyecharts 可视化

## 项目结构

- `etl.py`：合并 train/test 两个 CSV，只取分析需要的 11 个字段，清洗后写入 MySQL
- `analyse.sql`：四个维度的分析 SQL（用户分析 / 活跃度 / 付费 / 游戏习惯）
- `visualize.py`：查询结果用 pyecharts 渲染 HTML 图表
- `野蛮时代数据分析.md`：完整分析报告（含指标口径与结论）
- `tap4fun竞赛数据/字段说明.xlsx`：数据字段字典

## 复现

1. 本地准备 MySQL，建库 `test`
2. 修改 `etl.py` 中的数据目录和 MySQL 连接串，运行 `python etl.py` 完成入库
3. 按 `analyse.sql` 顺序执行（先 alter 字段类型，再跑各段查询）
4. 运行 `python visualize.py` 生成可视化页面

> 说明：脚本中的 MySQL 连接串（root:root@172.16.122.25）为当时的开发环境，复现时改成本地连接即可。

## 核心结论

- 总用户 311.7 万，付费用户（PU）60,988 人，付费率 1.96%
- ARPU 0.58 元，ARPPU 29.19 元，付费用户合计消费约 178 万元
- 付费用户平均在线约 2 小时，远高于整体水平
- 付费用户 PVP 胜率 71.13% vs 非付费 38.03%；PVE 平均胜率 90.1%

## 许可与数据版权

仓库代码采用 MIT 许可证（见 [LICENSE](LICENSE)），仅作学习交流用途。数据集版权归 tap4fun 所有，勿用于商业用途。
