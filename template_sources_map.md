## 模板字段与信息源映射（对应 fin/template.txt）

说明：逐条对应模板 A–I 的字段，列出主要信息源、是否免费、以及获取方式（API/爬虫/手动上传）。所列示例来源参考 `fin/info_source.txt`，并补充常用公开渠道（EDGAR、Yahoo Finance、FRED 等）。

### Header: Ticker • Exchange • Sector • Geography • Fiscal year‑end • Last update
- 主要信息源：
  - SEC EDGAR（公司基本信息/报表抬头，Fiscal year-end）：免费｜API+爬虫
  - 公司官网/IR（交易所、地域、行业描述）：免费｜爬虫/人工上传
  - Yahoo Finance / yfinance（Ticker、交易所、行业分类）：免费（非官方）｜API
  - Alpha Vantage（基本信息/行情）：免费（有速率限制）/付费｜API
  - 付费：Bloomberg、Capital IQ、Factset、LSEG、Morningstar：付费｜API/终端

### A. Quick Business Summary
- 字段：业务简述、单一最大价值驱动、近季/年变化
- 主要信息源：
  - 10-K/20-F、10-Q、年报/季报 MD&A、Business 段：免费（EDGAR）｜API+爬虫
  - 投资者演示（Investor Presentation）、新闻稿：免费｜爬虫/上传
  - 财报电话会实录（Earnings Transcript）：部分免费（公司网站/部分媒体），付费（Factset/Capital IQ/Bloomberg/SeekingAlpha Pro）｜爬虫/订阅
  - 新闻聚合：NewsAPI、GDELT：免费（有额度）｜API；付费：Bloomberg News、Factiva｜终端/API

### B. Business Model（≤80字 + 图）
- 字段：Who pays / For what / How often；GTM；护城河简述
- 主要信息源：
  - 10-K/20-F（Customers、Revenue recognition、Segments）：免费（EDGAR）｜API+爬虫
  - 招股书 S-1 / 投资者日演示：免费｜爬虫/上传
  - 行业研究/卖方报告：付费（S&P NetAdvantage、Capital IQ、Bloomberg、Morningstar、EMIS）｜平台/下载
  - 第三方评测/生态文档（开发者平台、定价页）：免费｜爬虫
  - 获取方式说明：以爬虫/上传为主，结构化信息可从 EDGAR XBRL 提取（API）。

### C. Fundamental Metrics
- 字段：Revenue 拆分、Gross Margin、FCF、分部节点（ARPU/流失/座位/利用率等）、P/E、EPS
- 主要信息源：
  - EDGAR XBRL（Income Statement/Balance Sheet/Cash Flow、分部披露）：免费｜API
  - Yahoo Finance / yfinance（历史价格、P/E、EPS）：免费（非官方）｜API
  - Alpha Vantage（价格、部分基本面）：免费/付费｜API
  - Financial Modeling Prep / Twelve Data / Tiingo：免费额度/付费｜API
  - 付费：Bloomberg、Capital IQ、Factset、LSEG、Morningstar Direct：付费｜API/终端
  - 备注：分部 KPI 多见于管理层披露/演示材料，通常需爬虫/上传；口径需校验。

### D. News / Sentimental Analysis（按核心单元）+ CAC/GP12/Payback/LTV/敏感性
- 字段：情绪与主题、CAC、12月毛利/回收期、LTV、敏感性（流失±2pp、价格±5%）
- 主要信息源：
  - 新闻：NewsAPI、GDELT（免费/额度）｜API；付费：Bloomberg News、Factiva｜API/终端
  - CAC/LTV/分部毛利：公司披露（S-1、投资者演示、MD&A）｜免费（爬虫/上传）；卖方报告｜付费
  - 若未披露：需基于公开数据与假设估算（需标注假设与来源）
  - 价格/流失敏感性：自定义模型；原始数据来自 C、D 节中的来源

### E. Quality Snapshot（护城河/周期性/会计质量/治理红旗）
- 主要信息源：
  - 护城河与周期性：行业研究与公司披露（10-K 业务、竞争、风险因素）：免费｜爬虫/上传；付费卖方报告
  - 会计质量：会计政策、收入确认、资本化与 SBC%（附注、MD&A）：免费（EDGAR）｜API+爬虫
  - 治理红旗：双层股权、关联交易、重述：公司章程/治理报告、8-K/DEF 14A、会计通知：免费（EDGAR）｜API+爬虫；付费数据库

### F. KPI Mini‑Chart（8 季度：Revenue、GM、FCF margin、ROIC）
- 主要信息源：
  - 季报 10-Q/年报 10-K（季度/年度口径）：免费（EDGAR）｜API
  - 价格/市值（若用于 ROIC 变体）：Yahoo Finance/Alpha Vantage：免费（非官方/限额）｜API
  - 图表生成：QuickChart（免费有额度）/matplotlib/plotly：免费｜API/本地

### G. Valuation Summary（DCF/Comps/SoTP；区间与敏感性）
- 主要信息源：
  - 市场数据：价格、Shares、EV/EBITDA、P/E：Yahoo/Alpha Vantage/FMP：免费/付费｜API；付费：Bloomberg/Capital IQ/Factset
  - 财务预测/指引：管理层指引（演示/电话会）、卖方一致预期：免费（部分）/付费｜爬虫/平台
  - WACC 输入：
    - 无风险利率：FRED（UST）｜免费｜API
    - Beta：Yahoo（近似）｜免费｜API；精确 Beta：Bloomberg/Capital IQ｜付费
    - 市场风险溢价/国家风险：Aswath Damodaran 数据｜免费｜爬虫/API
  - SoTP：分部信息与同业估值：EDGAR 分部披露 + 同业数据源（同上）

### H. Risks & “What would make us wrong?”
- 主要信息源：
  - 10-K/20-F 风险因素、MD&A：免费（EDGAR）｜API+爬虫
  - 新闻/监管动态：NewsAPI、GDELT、官方公告（8-K）｜免费｜API
  - 卖方/行业报告：付费（S&P、Bloomberg、EMIS 等）

### I. Sources & Confidence（链接+锚点、置信度、覆盖说明）
- 主要信息源：上述所有来源的原始链接与页/段落锚点；检索命中与引用聚合来自内部索引与日志。
- 获取方式：内部引用管理（RAG 检索器元数据）+ 生成时强制插入引用。

---

### 汇总：免费 vs 付费、API vs 爬虫（快速参考）

| 模块 | 关键字段 | 免费可得 | 付费增强 | 获取方式 |
|---|---|---|---|---|
| Header | Ticker/交易所/行业/FYE | EDGAR、Yahoo/Alpha Vantage | Bloomberg/Capital IQ/Factset | API + 爬虫 |
| A | 业务、驱动、变化 | EDGAR、IR、新闻 | 卖方报告、终端资讯 | 爬虫 + API |
| B | 商业模式、GTM、护城河 | EDGAR、S-1、IR | 卖方深研 | 爬虫/上传 |
| C | 收入/GM/FCF、P/E、EPS | EDGAR XBRL、Yahoo/AV/FMP | Bloomberg/CIQ/Factset | API |
| D | 情绪、CAC/LTV | NewsAPI/GDELT，CAC/LTV常需披露或估算 | 卖方/终端 | API + 爬虫 |
| E | 会计质量、治理 | EDGAR 披露 | 付费治理数据库 | API + 爬虫 |
| F | 8 季度 KPI | EDGAR、Yahoo/AV | Bloomberg/CIQ 时间序列 | API |
| G | 估值/敏感性 | FRED/Yahoo/AV + 自研模型 | 付费一致预期/精确 Beta | API + 计算 |
| H | 风险 | EDGAR、新闻 | 卖方/监管数据库 | API + 爬虫 |
| I | 引用/置信度 | 内部日志/检索元数据 | — | 内部生成 |

### 取得难度与替代方案提示
- CAC/LTV/分部毛利：许多公司未披露；可在 S-1、投资者日材料、SaaS 公司 FAQ 寻找；否则基于公开口径+假设估算，必须显式标注假设。
- 分部 KPI（ARPU/流失/座位/载客率等）：常在演示/电话会口径披露；需爬虫与半结构化解析。
- 精确 Beta、卖方一致预期、详细同业比较：通常需要付费终端或数据服务。


