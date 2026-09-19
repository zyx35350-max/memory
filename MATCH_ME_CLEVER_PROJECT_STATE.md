# MATCH ME CLEVER --- PROJECT STATE

> 项目控制文件 / Project Control File 最后整理：2026-09-15
> 当前阶段：V1.1.5 设计与 V1.2 研究阶段
> GitHub：`https://github.com/zyx35350-max/match-me-clever`

## 0. 文件用途与信息优先级

这是 Match Me Clever 的项目状态控制文件，用于在当前对话结束、新开
ChatGPT 对话、开发工具额度耗尽或上下文丢失后恢复项目。

信息优先级： 1. GitHub `main` 当前实际代码：代码事实 Source of Truth 2.
本文件：项目状态、架构决策、未完成事项、不可破坏约束 3. 当前 ChatGPT
对话：临时讨论与当前工作上下文 4.
未写入本文件的旧讨论：不得自动视为最终决策

如果代码与本文件冲突，不猜测；先检查 GitHub `main`，再更新本文件。

------------------------------------------------------------------------

# 1. 项目定位

**Match Me Clever** 是一个面向个人求职的 AI 求职助手。

核心不是简单的职位搜索器、招聘网站聚合器、简历生成器或自动投递机器人，而是：

> 多来源职位发现 + 职位语义理解 + 个性化职业匹配 + 职业成长判断 +
> 公司招聘情报

核心目标：帮助用户找到"适合现在的我，同时对未来职业发展有价值"的职位，而不是单纯找到更多职位。

------------------------------------------------------------------------

# 2. 版本状态

## V1.1 --- Completed

核心：Career Profile、Career Matching Foundation、Career
Engine、Immediate Fit、Career Growth
Value、Feedback、双语概念规范化基础。

## V1.1.1 --- Completed / Closed

已处理并验证：Education、Years of Experience、Preferred Locations、Work
Mode、localStorage migration、profile bridge、feedback
语义边界、production build、GitHub `main`。

已确认目标值： - Education: Associate degree / 大专 - Years Experience:
1 - Preferred Locations: Shenzhen / Huiyang / Zhuhai - Work Mode: Any

**注意：**后续一次公开 GitHub 检查曾发现 `career-data.ts`
默认值似乎又出现旧值（Bachelor、4
years、Shenzhen/Guangzhou/Remote）。这是待重新核验的状态冲突，不得猜测或静默修改。

## V1.1.5 --- Current

名称：**Job Language & Understanding Foundation**

目标：让真实世界的中文、英文、中英混合 JD 在进入现有 Career Engine
前完成语言识别、必要翻译、语义抽取、概念规范化和国际化信号提取。

原则：**不重写 Career Engine，不改变现有匹配公式。**

## V1.2 --- Architecture / Research

目标：**Real Job Discovery + Source Resilience + Job Lifecycle +
Deduplication + Company Job Aggregation**。

------------------------------------------------------------------------

# 3. 开发工具状态

-   GitHub `main`：代码 Source of Truth
-   Lovable：免费额度已耗尽
-   Bolt.new：已成功从 GitHub 导入，但当前额度也已耗尽
-   当前：以研究、架构、数据模型、验收标准为主，暂不强行进入代码修改

------------------------------------------------------------------------

# 4. 用户 Career Profile --- 已确认

## 工作经历

### 深圳市欧易通网络科技有限公司 --- 内容运营 --- 2025.03--2025.08

-   eBay 日常运营，300+ SKU
-   标题、关键词、卖点、价格优化
-   通过组合销售、折扣等处理 20+ 滞销产品
-   Promoted Listings，日预算约 \$10--50
-   出价、曝光、点击、花费分析；部分 CTR +10%
-   促销、优惠券、海报
-   订单、退货、客户咨询、Excel
-   正向评价率 \>90%

### 深圳曦橡科技有限公司 --- 跨境电商运营 --- 2025.09--2026.07

-   欧洲/美国 DIY、Craft、Home Art、Holiday Cultural Products 市场研究
-   硅胶、树脂、石膏模具研究；小众/季节性机会、竞品分析
-   SKU 曝光、转化、销售、排名；标题、关键词、卖点、详情、Listing 优化
-   销售、库存、供应链协调；预测、库存预警、补货、滞销库存
-   海外艺术/家居趋势；竞品/Influencer Benchmarking
-   差异化产品开发；外观/重量优化
-   独立负责 TEMU 全托管店；约 800+ orders/day；类目 Top 15

## 教育

深圳信息职业技术学院；大专 / Associate
degree；物联网技术应用；2022--2025。

## 技能

-   Cross-border E-commerce Operations / 跨境电商运营
-   Overseas Market Research / 海外市场研究
-   Product Selection / 选品
-   Product Development / 产品开发
-   E-commerce Operations / 电商运营
-   Content Operations / 内容运营
-   AI Visual / AI 视觉
-   Visual Design / 视觉设计
-   Photoshop / PS
-   AI Tools
-   Video / Poster related skills
-   Basic Programming
-   AI-assisted workflow / AI 工具效率

## 职业方向

-   D：产品开发 / 选品
-   E：内容 / 新媒体
-   F：AI 相关
-   G：视觉设计 / AI 视觉

## 地点 / 工作方式

Preferred Locations：Shenzhen、Huiyang、Zhuhai。 Work Mode：Any（On-site
/ Hybrid / Remote）。Remote 对项目/作品集方向有吸引力；Hybrid 可接受。

## 判断标准

重要性：成长、行业前景、薪资、可迁移技能、工作时间。

Deal Breakers：无意义加班、高重复低成长、没有发展空间。

## 3 年目标

能力明显提升、职业方向清晰、拥有自己的项目/作品/核心技能、做市场需要且自己认可的工作、AI
能力强、有想法、有创造力、有前瞻性。

## 新增明确偏好：外企 / 国际化环境

用户明确表达有意愿进入外企/跨国公司。不能因为"海外市场研究""跨境电商"经历而自动推断这一偏好；它是显式
Career Preference 维度。

应拆成： - Company Type：Foreign-owned、Multinational、International
Company、Domestic Private、State-owned、Public
Company、Startup、Unknown - International Environment：Global
Team、Overseas Business、English Usage、Cross-border Collaboration -
User Preference：Preferred / Acceptable / Avoid

不要只设计 `wantForeignCompany = true`。

------------------------------------------------------------------------

# 5. Career Engine --- 核心边界

Career Engine 是单一匹配引擎，必须与招聘来源解耦。

``` text
Job Data
  ↓
Normalized Job
  ↓
Career Engine
  ↓
Immediate Fit + Career Growth Value
  ↓
Personalized Result
```

## Immediate Fit

回答"这个职位现在适不适合我？"，关注当前技能、经验、职责、地点、工作方式、职位要求。

## Career Growth Value

回答"这个职位对未来职业发展有没有价值？"，关注技能积累、可迁移能力、职业方向、AI
能力、产品/内容/运营等长期能力、行业前景和新能力暴露。

## 明确禁止

V1.1.5/V1.2 不得重写 Career Engine、随意修改匹配公式、改变 Immediate Fit
/ Career Growth Value 定义，或让新 Source 直接进入核心匹配逻辑。

## Feedback

`rejected` 只代表申请结果为
rejected，不能自动解释为用户不喜欢该职位。Feedback 若影响
Profile，应形成建议并由用户确认，不能静默改变偏好。

------------------------------------------------------------------------

# 6. V1.1 双语概念基础

当前已有 `concepts.ts`、`conceptKey()`、`normalizeConcept()`。

原则：**整个项目只能有一个 Canonical Concept Normalization System。**

已有双语概念示例： - Cross-border E-commerce Operations ↔ 跨境电商运营 -
Overseas Market Research ↔ 海外市场研究 - Product Selection ↔ 选品

Career Profile 可保留 `name` / `nameOriginal`；Career Engine 通过
`normalizeConcept()` 做概念匹配。

------------------------------------------------------------------------

# 7. V1.1.5 --- Job Language & Understanding Foundation

## 数据流

``` text
Raw Job
 → Language Detection
 → Translation（if useful）
 → Semantic Extraction
 → Concept Normalization
 → International Signals
 → NormalizedJob
 → Existing Career Engine
```

## Language

``` ts
type JobLanguage = "zh" | "en" | "mixed" | "unknown"
```

## Translation

``` ts
titleTranslated?: string
descriptionTranslated?: string
```

永远保留 Original；翻译不能覆盖原文，翻译不是 Source of Truth。

## Semantic Extraction

提取：Job Title、Skills、Responsibilities、Career
Direction、Experience、Education、Work Mode、Employment Type、Language
Requirements、International Environment Signals。

## Title Normalization

例如"海外电商运营 / 跨境电商运营 / Cross-border E-commerce Specialist /
International E-commerce Operations"应能够进入相同或相关 canonical
concept，但原始职位名称必须保留。

## International Signals

``` ts
internationalEnvironment?: {
  overseasBusiness?: boolean
  globalTeam?: boolean
  englishUsage?: boolean
  crossBorderCollaboration?: boolean
}
```

这些是职位/公司事实信号，不是用户偏好。

## English Requirement

独立为：`required | preferred | unknown`。JD
未提英语不能推断为不需要，应为 `unknown`。

## Company Type

``` ts
type CompanyType =
  | "foreign_owned"
  | "multinational"
  | "international_company"
  | "domestic_private"
  | "state_owned"
  | "public_company"
  | "startup"
  | "unknown"
```

可有 `confidence?: number`。

## Evidence Level

``` ts
type EvidenceLevel = "explicit" | "strong" | "inferred" | "unknown"
```

缺失证据 ≠ false。公司名带"国际"、英文 JD、海外客户等都不能单独证明
multinational / foreign-owned。

## V1.1.5 Non-goals

-   不重写 Career Engine
-   不改 Matching Formula
-   不改 Immediate Fit / Career Growth Value
-   不做 BOSS/51Job/Zhaopin Adapter
-   不做跨平台 Company Entity Resolution
-   不做完整 Company Intelligence
-   不自动判断"这家公司适不适合用户"
-   不删除/修改 Mock Jobs
-   不用翻译替换原文
-   不建立第二套概念规范化系统
-   不做无证据公司类型推断

## Acceptance Tests

-   中文 JD → `zh`；英文 → `en`；中英混合 → `mixed`
-   中英文等价职位表达 → 同一 canonical concept
-   明确 global team → `globalTeam=true`，但不能因此判断 multinational
-   明确 English required → `englishRequirement=required`
-   未提英语 → `unknown`
-   公司名含"国际" → company type `unknown`

------------------------------------------------------------------------

# 8. V1.2 --- Real Job Discovery

## 核心架构

``` text
Sources
 → Discovery
 → RawJob
 → V1.1.5 Job Understanding
 → Normalize
 → Dedup
 → Existence Check
 → Freshness Check
 → Activity Check
 → Zombie Filter
 → Active Opportunity Pool
 → Career Engine
 → User
```

## RawJob

``` ts
type RawJob = {
  source: string
  sourceJobId?: string
  sourceCompanyId?: string
  sourceUrl: string
  titleOriginal: string
  companyOriginal: string
  locationOriginal?: string
  salaryOriginal?: string
  descriptionOriginal: string
  publishedAtOriginal?: string
  updatedAtOriginal?: string
  refreshedAtOriginal?: string
  deadlineOriginal?: string
  statusOriginal?: string
  fetchedAt: string
}
```

RawJob 是 Source Truth。

## NormalizedJob

``` ts
type NormalizedJob = {
  id: string
  source: string
  sourceJobId?: string
  sourceUrl: string
  title: string
  company: string
  location: string[]
  workMode: WorkMode
  employmentType: EmploymentType
  salary?: { min?: number; max?: number; currency?: string; period?: string }
  skills: string[]
  responsibilities: string[]
  industry?: string
  careerDirection?: string[]
  aiRelevance?: number
  growthPotential?: number
  original: { title: string; description: string; location?: string; salary?: string }
  normalizedAt: string
  lifecycle?: {
    publishedAt?: string
    updatedAt?: string
    applicationDeadline?: string
    availability: "open" | "deadline_passed" | "removed" | "stale" | "unknown"
    freshness: "very_fresh" | "fresh" | "normal" | "aging" | "stale"
  }
}
```

## Source Types

``` ts
type JobSourceType =
  | "official_api"
  | "licensed_provider"
  | "company_career"
  | "public_web"
  | "unofficial_adapter"
  | "user_import"
```

## Access Policy

``` ts
type AccessPolicy =
  | "official_api"
  | "licensed"
  | "public_manual"
  | "restricted_automation"
  | "unknown"
```

技术上能访问 ≠ 有权自动化访问。

## FetchResult

``` ts
type FetchResult = {
  status: "success" | "partial" | "blocked" | "challenged" | "unavailable"
  jobs: RawJob[]
  evidence?: {
    pageAccessible: boolean
    structuredDataAvailable: boolean
    resultCount?: number
  }
}
```

最重要规则：`challenged` / `blocked` 不能被解释为"没有职位"。

------------------------------------------------------------------------

# 9. Job Lifecycle / Zombie / Tombstone

不要使用简单的"30 天过期"或"60 天过期"作为全局规则。

优先使用： - publishedAt - updatedAt - refreshedAt -
applicationStartAt - applicationDeadline - validUntil -
sourceReportedStatus

Availability：

``` ts
type JobAvailability = "open" | "deadline_passed" | "removed" | "stale" | "unknown"
```

Freshness：

``` ts
type JobFreshness = "very_fresh" | "fresh" | "normal" | "aging" | "stale"
```

Availability 与 Freshness 必须分开。

Activity Evidence：

``` ts
type ActivityEvidence = {
  sourceCount: number
  recentUpdate: boolean
  validDateActive: boolean
  crossSourceMatch: boolean
  companyCareerMatch: boolean
}
```

Lifecycle Signal Quality：

``` ts
type LifecycleSignalQuality = "strong" | "moderate" | "weak" | "none" | "unknown"
```

Activity Signals：

``` ts
activitySignals: {
  publishedAt?: string
  updatedAt?: string
  refreshedAt?: string
  recruiterActiveAt?: string
  sourceReportedStatus?: string
  observedAt: string
}
```

只有经过 Existence + Freshness + Activity + Zombie Filter 后，才进入
Active Opportunity Pool。

Zombie Job =
页面仍存在，但实际招聘机会已经结束、失效、被移除或无法证明仍有效。

Expired Tombstone
最少保存：source、sourceJobId、URL、company、title、firstSeen、expiredAt、reason。用途是防止旧页面重新出现时被当作新职位。

------------------------------------------------------------------------

# 10. Snapshot / Incremental Sync

``` ts
type RawJobRecord = {
  source: string
  sourceJobId?: string
  sourceUrl: string
  fetchedAt: string
  rawTitle: string
  rawCompany: string
  rawLocation?: string
  rawSalary?: string
  rawDescription: string
  rawPayload?: unknown
}
```

保存足够信息以便未来重新 Normalize，但不要成为招聘平台数据库镜像。

使用 content hash： - JD 未变化：更新 observation time / fetchedAt
等观察信息 - JD 改变：保存新 snapshot、重新 Normalize、重新判断
lifecycle

------------------------------------------------------------------------

# 11. Source Resilience

目标是 **Source-Failure Tolerant**，不是 **Anti-Bot Fighting**。

单一来源挂掉不能导致系统挂掉：

``` text
BOSS unavailable
 → 其他 Source 继续
 → User Import 继续
 → Career Engine 继续
```

SourceHealth：

``` ts
type SourceHealth = {
  sourceId: string
  status: "healthy" | "degraded" | "unavailable"
  lastSuccessfulFetch?: string
  lastFailedFetch?: string
  consecutiveFailures: number
  latencyMs?: number
  itemCount?: number
  freshness?: number
  capabilityHealth?: {
    jobDiscovery?: boolean
    companyDiscovery?: boolean
    companyVerification?: boolean
  }
}
```

机制：cache、retry、backoff、circuit breaker、source health、incremental
sync、dedup、raw snapshot、fallback、user import。

禁止：绕 CAPTCHA、绕登录限制、绕 anti-bot、读取/导出浏览器
Cookies、未经授权批量抓取受限制平台。

------------------------------------------------------------------------

# 12. 四条战略分支（必须保留）

## Branch 1 --- Personal Job Search Experiment / Core Job Discovery

真正帮助用户找工作。核心：BOSS、51Job、Zhaopin、Liepin、Lagou、官方公共就业、Company
Career Pages、User Import。

## Branch 2 --- Stable / Long-term Data Sources

逐步采用 Official APIs、Licensed Providers、Company
Integrations、稳定公开数据接口。

**Branch 2 不替代 Branch 1，而是逐渐替换不稳定 Adapter。**

## Branch 3 --- Company Intelligence

`Job → Company → Other Current Jobs → Recruitment Activity → Company Intelligence`。

不是做完整企业百科。

## Branch 4 --- Portfolio / Case Study

展示 Multi-source discovery、Source resilience、Semantic
normalization、Lifecycle awareness、Personalized matching、Company
intelligence。

------------------------------------------------------------------------

# 13. Company Discovery --- 当前确定的方向

核心转变：

> **Job Discovery → Company Discovery**

原因：搜索引擎过度曝光大公司；用户竞争力有限；中小公司可能有适合职位；小公司未必有成熟官网；中国中小企业大量依赖国内招聘平台；公司名称/注册经营范围未必反映当前业务；当前招聘岗位是当前招聘活动的重要证据。

搜索引擎是 Supplementary；国内招聘平台是 Core Job Discovery。

------------------------------------------------------------------------

# 14. Company Aggregation

### Level 1 --- V1.2 必须

`Job → Company`

### Level 2 --- V1.2 目标

`Job → Company → Same-platform Other Jobs`

### Level 3 --- Future

`BOSS Company ↔ 51Job Company ↔ Zhaopin Company ↔ Liepin Company`

Level 3 是 Cross-platform Entity Resolution，不作为 V1.2 必做。

SourceCompany：

``` ts
type SourceCompany = {
  source: string
  sourceCompanyId?: string
  nameOriginal: string
  url?: string
  descriptionOriginal?: string
  locationOriginal?: string
  industryOriginal?: string
  fetchedAt: string
}
```

CompanyProfile：

``` ts
type CompanyProfile = {
  id: string
  canonicalName?: string
  sourceRefs: { source: string; sourceCompanyId?: string; url?: string }[]
  observedFacts: {
    industry?: string
    locations?: string[]
    companySize?: string
    businessDescription?: string
  }
  recruitmentActivity?: {
    activeJobCount?: number
    recentJobCount?: number
    sourceCount?: number
    lastObservedAt?: string
  }
  inferredSignals?: {
    businessDirections?: string[]
    hiringFocus?: string[]
  }
  updatedAt: string
}
```

Company Profile = "这家公司是谁？"；Company Intelligence =
"这家公司现在对用户意味着什么？"

Company identity
evidence：统一社会信用代码、官方域名、官方公司页、招聘平台 Company ID
较强；地址、电话、名称相似度、描述相似度较弱。

V1.2 不做完整企业实体解析，但必须保存 sourceCompanyId 和 source URL。

CompanyJobProvider：

``` ts
interface CompanyJobProvider {
  getCompanyJobs(sourceCompanyId: string): Promise<FetchResult>
}
```

Production threshold：BOSS / 51Job / Zhaopin 中至少 2 个达到 L5。

``` text
L0 Source exists but unverified
L1 Job discovery
L2 Job → Company
L3 Company → Other Jobs
L4 Company Jobs + Pagination
L5 Company Jobs + Lifecycle
L6 Stable API / Licensed
```

公司岗位数量必须表述为 **Observed active
jobs**，不能把来源观察数量写成公司全部岗位。

------------------------------------------------------------------------

# 15. 国内核心招聘平台

五个必须保留： 1. BOSS直聘 2. 51Job / 前程无忧 3. 智联招聘 4. 猎聘 5.
拉勾

不要求五个平台技术实现完全相同。

## BOSS

Core domestic source；experimental unofficial adapter；restricted
automation until authorization is clear。
有职位搜索、公司搜索、校园/海外搜索、职位详情、公司页面；Job ID /
Company ID 可用于 Company Intelligence。必须特别处理 risk control /
challenge；不绕 CAPTCHA。

## 51Job

Core domestic
source；experimental。支持多维高级搜索、职位详情、公司信息；可能出现
Access Verification / WAF。Challenge ≠ Zero Jobs。

## Zhaopin

Core domestic source；experimental。可涉及 Job ID、Company
ID、Title、Company、Company Size、Company
URL、Industry、Financing、Location、Salary、Education、Experience、Employment
Type、Category、Recruit Count、Skills、Benefits、Description、Posted
Date 等。旧 JSON 可能因风险控制返回空结构，不能视为真实 0。

## Liepin

Core domestic source；experimental。具有刷新时间筛选（1 day / 3 days / 1
week / 1 month）以及 `pubTime` / refresh time 等生命周期信号。Refresh ≠
guaranteed open recruitment；可能出现 soft 404、challenge、rate limit。

## Lagou

保留；second-batch
experimental。存在搜索、公司、校园、刷新机制；不锁死旧 endpoint / 旧 API
方案。

------------------------------------------------------------------------

# 16. 官方 / 公共就业来源

这些与国内商业招聘平台并行，不能替代它们。

## 中国公共招聘网

Official public employment
source，P1。具备地区、岗位、单位类型、行业、工作性质、学历、薪资、发布日期、有效日期等信息；生命周期信号较强。页面存在不代表职位一定有效。

## 国家大学生就业服务平台（ncss.cn）

Official national student employment ecosystem；包含
jobs、internships、campus recruitment、联合招聘、SOEs、public
institutions
等。使用条款对商业使用、下载、复制、再利用存在限制；未经授权不得假设可批量自动抓取。

## 12333 / 全国就业公共服务平台

Discovery Hub / Source
Registry；连接公共招聘、中央/国家招聘、就业在线、地方服务等，不应简单理解为单一职位数据库。

## 就业在线

Official public employment
service；有企业招聘、人才搜索、面试管理、求职搜索、简历等；API
尚未确认。

## 广东公共就业招聘平台

Official public employment source；支持 Job Search、Job
Posting、Application、Recruitment Events；API 尚未确认。

## 深圳政府开放数据

Potential stable data source / future API
candidate。已发现企业招聘岗位信息 CSV 等机器可读数据及 Developer
Center；"存在数据集"不等于招聘数据已有公开 API。后续确认
API、License、Update frequency、Usage permission、Coverage。

## 深圳人力资源生态服务平台

Official HR
ecosystem；需确认是独立职位池还是主要镜像广东公共就业平台，避免重复
ingestion。

## 深i人才

Shenzhen SASAC-related official
ecosystem；有职位、公司、招聘活动、热门行业、招聘信息、简历等；使用政府资源及可信数据。再发布/使用边界需确认。

## 珠海人力资源网

P2。当前有职位、稳定 detail
ID、salary、experience、education、location、hiring
count、description、company、updated
date。存在测试/非投递性质职位，因此未来应有 Job Quality
Signal，而非简单删除。

## 惠青直聘

P3。历史官方信息表明与惠州人社招聘数据有关；当前技术入口、API、ID、时间戳、status
尚未充分验证。不得与商业"惠州直聘"混淆。

------------------------------------------------------------------------

# 17. 稳定国际公司 Career Page 来源

V1.2 P1 对照组：Greenhouse、Lever、Company Career Pages。

意义：验证稳定 source architecture，并作为未来长期来源候选。

------------------------------------------------------------------------

# 18. Source 开发优先级

这是**开发优先级**，不是来源价值排名。

### P0

-   User Import
-   Existing V1.1 Career Engine

### P1

-   BOSS
-   51Job
-   Zhaopin
-   中国公共招聘网
-   Greenhouse
-   Lever
-   BOSS / 51Job / Zhaopin Company Intelligence research

### P2

-   Liepin
-   Lagou
-   Guangdong public employment
-   Shenzhen HR ecosystem
-   深i人才
-   珠海人力资源网

### P3

-   惠青直聘

------------------------------------------------------------------------

# 19. User Import --- 永久 fallback

用户可粘贴 JD、导入职位、保存 Source URL，直接进入：

``` text
RawJob
 ↓
V1.1.5 Job Understanding
 ↓
NormalizedJob
 ↓
Career Engine
```

即使所有自动 Source 都不可用，项目仍然可工作。

------------------------------------------------------------------------

# 20. Deduplication

-   D01：同 Source + 同 Job ID → same job
-   D02：同 URL → same job candidate
-   D03：同公司同职位 → Company aggregation
-   D04：同 Job ID 但 JD 内容变化 → new snapshot / re-normalize
-   D05：内容未变化 → update observation only
-   D06：过期职位重新出现 → Tombstone / lifecycle protection

------------------------------------------------------------------------

# 21. V1.2 Test Plan

## Job Discovery

-   J01 Keyword Search → real jobs
-   J02 City Filter → correct city
-   J03 Job Detail
-   J04 Stable Job ID
-   J05 Company ID
-   J06 Source URL
-   J07 Pagination
-   J08 Multiple Conditions
-   J09 True Zero Result → `success + 0`
-   J10 Risk Control → `challenged`，不能是 `success + 0`

## Company

-   C01 Job → Company
-   C02 Company ID
-   C03 Company URL
-   C04 Company Name
-   C05 Company Info
-   C06 Company Jobs
-   C07 Same Company Proof
-   C08 Job ID
-   C09 Company Job Pagination
-   C10 True Empty
-   C11 Challenge ≠ Empty
-   C12 Partial → `partial`

## Lifecycle

-   L01 Published
-   L02 Updated
-   L03 Refresh
-   L04 Deadline
-   L05 Source Status
-   L06 Stale
-   L07 Expired
-   L08 Removed
-   L09 Unknown
-   L10 No universal 30/60-day rule

## Resilience

-   R01 Source Down
-   R02 Timeout
-   R03 Challenge
-   R04 Partial
-   R05 Retry
-   R06 Backoff
-   R07 Circuit Breaker
-   R08 Recovery
-   R09 Health
-   R10 Cache

## Dedup

-   D01 Same Source Job
-   D02 Same URL
-   D03 Same Company Job
-   D04 Changed JD
-   D05 Unchanged JD
-   D06 Expired Job Reappears

## Company Intelligence

-   CI01 Company Profile
-   CI02 Observed Active Job Count（不能声称 Total）
-   CI03 Recent Hiring
-   CI04 Facts vs Inference
-   CI05 Multiple Current Jobs
-   CI06 User Relevance
-   CI07 Foreign Company / International Signal
-   CI08 Uncertainty

## Company Preference

-   CP01 Company Nature
-   CP02 Foreign-owned / Multinational
-   CP03 HQ Location
-   CP04 China Entity
-   CP05 International Team
-   CP06 English Requirement
-   CP07 Global Collaboration
-   CP08 Preference Match
-   CP09 No Evidence = Unknown
-   CP10 User Override

------------------------------------------------------------------------

# 22. 核心架构边界

``` text
Source
  ↓
Raw Facts
  ↓
Job Understanding
  ↓
Normalized Job
  ↓
Company Intelligence
  ↓
Career Engine
  ↓
Personalized Fit
```

Source 负责找数据；Job Understanding 负责理解职位；Company Intelligence
负责理解公司/招聘活动；Career Profile 负责理解用户；Career Engine
负责用户与职位/公司相关信息的匹配。

**不要让 Source Adapter 进入 Career Engine。**

例如禁止 `if source === "boss"` 后改变 matching score。

正确：

``` text
BOSS → RawJob → NormalizedJob → Career Engine
```

同样不要让 Career Profile 直接控制
Source；例如"想进外企"不能直接等于"只搜索外企"。应为：

``` text
Source Discovery
 ↓
Facts
 ↓
Company Type / International Signals
 ↓
Career Profile Preference
 ↓
Career Engine
```

------------------------------------------------------------------------

# 23. Company Preference 数据结构方向

``` ts
type CompanyPreference = {
  preferredCompanyTypes?: CompanyType[]
  acceptableCompanyTypes?: CompanyType[]
  excludedCompanyTypes?: CompanyType[]
  internationalEnvironment?: {
    preferred?: boolean
    language?: string[]
    globalTeam?: boolean
  }
  notes?: string
}
```

V1.1.5
先建立数据层；不急于强行加入评分。不要因为外企偏好直接给职位强行加分；用户偏好与公司事实保持分离。

------------------------------------------------------------------------

# 24. 产品原则

1.  不是职位越多越好，而是有效、相关、有职业价值的职位越多越好。
2.  不是抓取越强越好，而是 Source 越稳定、合规、可替换越好。
3.  不是公司越大越好，而是有价值的公司都应有机会被发现。
4.  页面存在 ≠ Active Opportunity。
5.  Facts / Evidence / Inference 必须分开。
6.  不为了新功能重写核心引擎。
7.  New data 应适配 Career Engine，而不是反过来。

------------------------------------------------------------------------

# 25. Adapter 统一接口方向

``` ts
interface JobSourceAdapter {
  searchJobs(query: JobSearchQuery): Promise<FetchResult>
  getJob(sourceJobId: string): Promise<FetchResult>
  getCompany?(sourceCompanyId: string): Promise<FetchResult>
  getCompanyJobs?(sourceCompanyId: string): Promise<FetchResult>
}
```

未来可能包括：BossAdapter、51JobAdapter、ZhaopinAdapter、LiepinAdapter、LagouAdapter、GreenhouseAdapter、LeverAdapter、PublicEmploymentAdapter、UserImportAdapter。

------------------------------------------------------------------------

# 26. Adapter Failure 原则

例如 BOSS 被 challenge：

``` text
SourceHealth = degraded
FetchResult = challenged
```

而不是：

``` text
jobs = []
 → Career Engine = no jobs
```

------------------------------------------------------------------------

# 27. Portfolio / Case Study 叙事

以后可以将项目描述为：

> A resilient, multi-source, lifecycle-aware, personalized AI career
> matching system.

技术故事：

``` text
Multi-source
 + Source resilience
 + Semantic normalization
 + Lifecycle awareness
 + Company intelligence
 + Personalized matching
```

而不是简单描述成"一个爬虫"。

------------------------------------------------------------------------

# 28. Open Questions

以下尚未最终定案：

-   OQ01 BOSS 当前自动化访问的具体授权边界
-   OQ02 51Job 当前自动化访问的授权边界
-   OQ03 Zhaopin 当前自动化访问的授权边界
-   OQ04 Liepin 当前自动化访问的授权边界
-   OQ05 Lagou 当前自动化访问的授权边界
-   OQ06 深圳政府招聘数据是否存在可合法使用的公开 API
-   OQ07 深圳人力资源生态服务平台是否有独立职位池
-   OQ08 深i人才的数据使用/再发布边界
-   OQ09 珠海人力资源网完整 lifecycle / offline 机制
-   OQ10 惠青直聘当前技术数据入口
-   OQ11 Company Type 如何达到可靠 Evidence Level
-   OQ12 Cross-platform Company Entity Resolution 的未来实现方式

------------------------------------------------------------------------

# 29. 当前 GitHub 状态注意事项

V1.1.1 曾验证的目标值：Associate degree、1
year、Shenzhen/Huiyang/Zhuhai、Any。

后续一次公开 GitHub 检查曾发现 `src/lib/career-data.ts` 默认值似乎又出现
Bachelor、4 years、Shenzhen/Guangzhou/Remote。**必须重新检查
`main`，不得根据旧对话直接修改。**

代码恢复时至少检查： 1. `src/lib/career-data.ts` 2. `profile-bridge.ts`
3. `career-engine.ts` 4. `concepts.ts` 5. migration / localStorage
相关逻辑

确认实际状态后再决定是否修复。

------------------------------------------------------------------------

# 30. 版本关系

``` text
V1.1
└── Career Matching Foundation
      ↓
V1.1.5
└── Job Understanding Foundation
      ↓
V1.2
├── Real Job Discovery
├── Source Resilience
├── Job Lifecycle
├── Deduplication
└── Company Job Aggregation
      ↓
V1.3+
└── Company Intelligence
```

## V1.1 → V1.1.5

Reuse：Career Profile、Career
Engine、`normalizeConcept()`、`conceptKey()`、canonical bilingual
taxonomy、`name/nameOriginal`、Immediate Fit、Career Growth
Value、Feedback、Mock Jobs。

Add：RawJob、JobLanguage、translation fields、semantic
extraction、title/skill/responsibility normalization、international
signals、Company Type、confidence、English requirement、Evidence Level。

Do not change：Career Engine、matching formula、Immediate Fit、Career
Growth Value、V1.1 behavior、original job text、concept normalization
system、Mock Jobs。

## V1.2 → V1.3+

V1.2 重点是可靠找到职位并送进 Career Engine；V1.3+ 才进一步做跨平台
Company Entity Resolution、招聘趋势、业务证据、公司级职业情报等。

------------------------------------------------------------------------

# 31. 正式工作顺序

``` text
1. 读取本文件
2. 检查 GitHub main 实际代码
3. 确认当前版本
4. 确认 Open Questions
5. 完成 V1.1.5 设计
6. 定义 V1.1.5 Acceptance Tests
7. 再进入代码
8. V1.1.5 完成后重新验证
9. 进入 V1.2 Source Implementation
```

不要在研究阶段因为发现新网站就立即写
Adapter；先评估数据价值、稳定性、访问授权、Job ID、Company
ID、Lifecycle、分页、challenge、重复、维护成本以及是否能独立于 Career
Engine。

------------------------------------------------------------------------

# 32. 每个版本完成后的固定动作

1.  Build
2.  Test
3.  检查关键文件
4.  Git commit
5.  Push GitHub
6.  检查 GitHub `main`
7.  更新本文件
8.  记录 Completed / Changed / Not Changed / Known Issues / Next Step

------------------------------------------------------------------------

# 33. 新 Chat 恢复项目的标准指令

> **继续 Match Me Clever 项目。请先读取
> `MATCH_ME_CLEVER_PROJECT_STATE.md`，再检查 GitHub `main`
> 当前代码状态，不要直接修改 Career Engine。从项目当前状态继续。**

V1.1.5：

> **继续 Match Me Clever V1.1.5。先读取
> `MATCH_ME_CLEVER_PROJECT_STATE.md`，确认 Job Language & Understanding
> Foundation 的设计和 Non-goals，然后继续 Acceptance Test /
> 数据结构设计。不要修改 Career Engine。**

V1.2：

> **继续 Match Me Clever V1.2。先读取
> `MATCH_ME_CLEVER_PROJECT_STATE.md`，检查 GitHub `main`，然后从 Source
> Specification / Adapter / RawJob / Lifecycle 开始，不要改变 Career
> Engine。**

------------------------------------------------------------------------

# 34. 总架构图

``` text
                    ┌──────────────────────┐
                    │    Career Profile    │
                    │   User Preferences   │
                    └──────────┬───────────┘
                               │
                               ↓
┌──────────────┐       ┌──────────────────────┐
│ Job Sources  │──────→│       Raw Job        │
└──────────────┘       └──────────┬───────────┘
                                  │
                                  ↓
                       ┌──────────────────────┐
                       │ Job Understanding    │
                       │      V1.1.5          │
                       └──────────┬───────────┘
                                  │
                                  ↓
                       ┌──────────────────────┐
                       │   Normalized Job     │
                       └──────────┬───────────┘
                                  │
                    ┌─────────────┴─────────────┐
                    ↓                           ↓
          ┌──────────────────┐       ┌────────────────────┐
          │  Career Engine   │       │ Company Intelligence│
          └────────┬─────────┘       └──────────┬─────────┘
                   │                            │
                   └─────────────┬──────────────┘
                                 ↓
                       ┌──────────────────────┐
                       │ Personalized Career │
                       │       Insight        │
                       └──────────────────────┘
```

------------------------------------------------------------------------

# 35. 一句话定义

> **Match Me Clever
> 是一个面向个人求职的、多来源、抗单点故障、具备职位语义理解和生命周期判断能力，并通过
> Career Engine 将真实职位与个人长期职业发展进行匹配的 AI 求职助手。**

------------------------------------------------------------------------

# 36. 十条不可破坏原则

1.  GitHub `main` 是代码事实 Source of Truth。
2.  Career Engine 与 Source Adapter 解耦。
3.  RawJob 永远保留原始职位信息。
4.  原文、翻译、标准化概念不能混为一谈。
5.  Existence ≠ Active Opportunity。
6.  Challenge / Blocked ≠ Zero Jobs。
7.  Facts / Evidence / Inference 必须分开。
8.  用户偏好不能污染 Source Facts。
9.  一个 Source 挂掉，整个系统不能挂。
10. 新功能优先适配现有架构，而不是为了新功能重写核心架构。

------------------------------------------------------------------------

# 37. 当前下一步

## 最高优先级：V1.1.5

先完成 Job Language & Understanding Foundation 的最终设计： 1.
最终数据结构 2. Language Detection 3. Translation fields 4. Semantic
Extraction 5. Title normalization 6. Skill normalization 7.
Responsibility normalization 8. International signals 9. Company Type
10. English requirement 11. Evidence Level 12. Acceptance Tests 13.
不改变 Career Engine 的边界确认

## 随后：V1.2

``` text
Source Specification
 ↓
RawJob
 ↓
NormalizedJob
 ↓
User Import
 ↓
Core Sources
 ↓
Lifecycle
 ↓
Dedup
 ↓
Resilience
 ↓
Company Aggregation
 ↓
Company Intelligence Foundation
```

------------------------------------------------------------------------

# 38. 当前状态总览

``` text
Project
└── Match Me Clever

V1.1
└── Career Matching Foundation
    STATUS: Completed

V1.1.1
└── Profile / Migration / Bridge fixes
    STATUS: Completed

V1.1.5
└── Job Language & Understanding Foundation
    STATUS: Designing / Researching

V1.2
└── Real Job Discovery
    ├── Source Resilience
    ├── Job Lifecycle
    ├── Deduplication
    └── Company Job Aggregation
    STATUS: Architecture / Research

V1.3+
└── Company Intelligence
    STATUS: Future
```

------------------------------------------------------------------------

# END OF PROJECT STATE
