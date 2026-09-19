# MATCH ME CLEVER — ARCHITECTURE

> 长期架构设计文档 / Architecture Decision Document  
> 项目：Match Me Clever  
> 当前阶段：V1.1.5 设计 → V1.2 架构研究  
> GitHub Source of Truth：`main`

---

# 0. 文档定位

本文件与：

`MATCH_ME_CLEVER_PROJECT_STATE.md`

配套使用，但职责不同。

## Project State

回答：

> **项目现在做到哪里了？**

包括：
- 当前版本
- 已完成事项
- 未完成事项
- Open Questions
- 下一步

## Architecture

回答：

> **项目为什么这样设计？哪些东西不能随便改变？**

包括：
- 系统边界
- 模块职责
- 数据流
- 核心抽象
- 架构原则
- 长期演进方向
- 不可破坏的设计决策

---

# 1. 项目核心定位

Match Me Clever 是一个：

> **面向个人求职的、多来源、抗单点故障、具备职位语义理解和生命周期判断能力，并通过 Career Engine 将真实职位与个人长期职业发展进行匹配的 AI 求职助手。**

它不是单纯：

- 招聘网站聚合器
- 爬虫
- 简历生成器
- 自动投递机器人
- 企业信息数据库

核心价值链：

```text
多来源职位发现
        ↓
职位语义理解
        ↓
职位标准化
        ↓
职位生命周期判断
        ↓
公司招聘活动理解
        ↓
个人职业匹配
        ↓
Career Insight
```

---

# 2. 第一性原则

## Principle 01 — Career Engine 独立于数据来源

招聘平台会变化：

- API 会变化
- 页面会变化
- 登录机制会变化
- Anti-bot 会变化
- 数据字段会变化
- 平台可能关闭某些访问方式

因此：

> Career Engine 不能依赖任何一个招聘平台。

错误：

```text
BOSS Job
    ↓
BOSS-specific Matching Logic
```

正确：

```text
BOSS
51Job
Zhaopin
Liepin
Lagou
Greenhouse
Lever
Public Employment
User Import
        ↓
     RawJob
        ↓
NormalizedJob
        ↓
 Career Engine
```

---

# 3. Principle 02 — Source Failure Tolerant

目标不是：

> 把每个平台的反爬都破解。

目标是：

> **任何一个 Source 挂掉，系统仍然能够工作。**

例如：

```text
BOSS unavailable
        ↓
51Job ───────┐
Zhaopin ────┤
Public ─────┤──→ Career Engine
Greenhouse ─┤
Lever ──────┤
User Import ┘
```

系统应该：

- 感知 Source 故障
- 标记 degraded / unavailable
- 尝试其他 Source
- 保留 cache
- 支持 User Import

---

# 4. Principle 03 — 不与 Anti-Bot 对抗

项目采用：

> **Source-failure tolerant**

而不是：

> **Anti-bot fighting**

禁止把架构建立在：

- CAPTCHA bypass
- 登录绕过
- 风控绕过
- Cookie 偷取
- 浏览器 Cookie 导出
- 隐藏 API 破解
- 未授权自动化

之上。

如果一个 Source：

```text
challenged
```

就明确记录：

```text
challenged
```

而不是假装：

```text
0 jobs
```

---

# 5. Principle 04 — Source Facts 与 AI Inference 分离

系统必须区分：

```text
Observed Fact
      ↓
Evidence
      ↓
Inference
```

例如：

### Fact

JD 明确写：

> Global team

可以记录：

```text
globalTeam = true
evidence = explicit
```

### Inference

AI 认为：

> 该岗位可能具有国际协作属性。

应该记录为：

```text
inferred
```

而不是把推断伪装成招聘方事实。

---

# 6. Principle 05 — 缺失证据 ≠ False

这是整个 Company Intelligence 的关键原则。

例如：

JD 没有写：

> English required

不能：

```text
englishRequired = false
```

应该：

```text
englishRequired = unknown
```

同样：

公司没有公开说明是否跨国：

```text
multinational = unknown
```

而不是：

```text
multinational = false
```

---

# 7. Principle 06 — Original 永远保留

任何标准化都不能破坏 Source Original。

例如：

```text
titleOriginal
descriptionOriginal
locationOriginal
salaryOriginal
```

标准化后：

```text
title
skills
responsibilities
careerDirection
```

但：

> Original 永远不能被 AI 翻译或标准化文本覆盖。

---

# 8. Principle 07 — Translation ≠ Original

翻译只是：

> Understanding Aid

不是：

> Source of Truth

数据应该：

```text
Original
+
Translated
+
Normalized
```

三者并存。

---

# 9. Principle 08 — 一个 Canonical Concept System

整个项目只允许一个概念标准化体系：

```text
concepts.ts
    ↓
conceptKey()
    ↓
normalizeConcept()
```

例如：

```text
跨境电商运营
Cross-border E-commerce Operations
Cross-border E-commerce Specialist
```

可以映射到统一概念。

禁止：

> V1.2 再建立第二套技能词典。

---

# 10. Principle 09 — User Preference 与 Source Fact 分离

例如用户：

> 希望进入外企。

这是：

```text
Career Profile
```

而：

> 公司是外商独资

这是：

```text
Company Fact
```

不能混在一个字段中。

正确：

```text
Company Fact
      ↓
Company Intelligence
      ↑
Career Profile Preference
      ↓
Career Engine
```

---

# 11. Principle 10 — Existence ≠ Active Opportunity

页面存在：

> 不等于职位仍在招聘。

必须区分：

```text
Page Exists
Job Exists
Job Active
Job Fresh
```

一个职位可能：

```text
page = exists
availability = stale
```

也可能：

```text
page = exists
availability = removed
```

---

# 12. Principle 11 — Freshness ≠ Availability

两个维度必须分开。

## Availability

回答：

> 这个机会是否仍然存在？

```ts
type JobAvailability =
  | "open"
  | "deadline_passed"
  | "removed"
  | "stale"
  | "unknown"
```

## Freshness

回答：

> 这个职位的信息有多新？

```ts
type JobFreshness =
  | "very_fresh"
  | "fresh"
  | "normal"
  | "aging"
  | "stale"
```

例如：

```text
open + aging
```

是合法状态。

---

# 13. Principle 12 — 不使用统一的 30/60 天过期规则

不同 Source 的生命周期机制不同。

优先使用：

- publishedAt
- updatedAt
- refreshedAt
- applicationStartAt
- applicationDeadline
- validUntil
- sourceReportedStatus

只有证据不足时才进行有限推断。

---

# 14. Principle 13 — Job-first Company Discovery

项目的公司发现策略是：

> **Job Discovery → Company Discovery**

而不是：

> Search Engine → Company → Jobs

原因：

- 搜索引擎更容易曝光大型、高知名度企业
- 中小企业可能没有完善官网
- 中小企业大量依赖国内招聘平台
- 用户真正需要的是适合自己的职位
- 当前招聘岗位本身就是当前招聘活动的重要证据

---

# 15. Principle 14 — Search Engine 是补充，不是中国职位数据库核心

搜索引擎适合：

- 公司官网
- Company Career Page
- 补充验证
- 公司背景
- 公开信息

但不应该成为：

> 中国招聘职位核心数据库。

核心 Job Discovery：

- BOSS
- 51Job
- Zhaopin
- Liepin
- Lagou
- Public Employment
- Company Career Pages
- User Import

---

# 16. Principle 15 — 不追求招聘平台数据库镜像

Match Me Clever 不应该成为：

> “中国所有职位数据库”。

目标是：

> **为当前用户发现、理解和匹配有效机会。**

因此：

- 不需要保存所有职位
- 不需要永久保存所有完整 JD
- 不需要复制整个招聘平台
- 不需要追求全量同步

---

# 17. 总体架构

```text
┌──────────────────────────────────────────────┐
│                 Job Sources                  │
│                                              │
│ BOSS / 51Job / Zhaopin / Liepin / Lagou      │
│ Public Employment / Career Pages             │
│ Greenhouse / Lever / User Import             │
└──────────────────────┬───────────────────────┘
                       ↓
              ┌─────────────────┐
              │ Source Adapters  │
              └────────┬────────┘
                       ↓
                  ┌──────────┐
                  │  RawJob  │
                  └────┬─────┘
                       ↓
          ┌───────────────────────────┐
          │ Job Understanding V1.1.5  │
          │ Language / Translation    │
          │ Semantic Extraction       │
          │ Concept Normalization     │
          │ International Signals    │
          └────────────┬──────────────┘
                       ↓
              ┌────────────────┐
              │ NormalizedJob  │
              └───────┬────────┘
                      ↓
          ┌───────────┴────────────┐
          ↓                        ↓
 ┌──────────────────┐      ┌────────────────────┐
 │ Career Engine    │      │ Company Intelligence│
 │ Immediate Fit    │      │ Company Profile     │
 │ Growth Value     │      │ Hiring Activity     │
 └────────┬─────────┘      └──────────┬─────────┘
          └──────────────┬────────────┘
                         ↓
              Personalized Career Insight
```

---

# 18. Layer 1 — Source Layer

负责：

> 获取 / 接收职位数据。

不负责：

- 职业匹配
- 用户偏好
- Career Growth
- 最终推荐结论

Source Adapter 只需要把不同来源转换成：

```text
RawJob
```

---

# 19. Layer 2 — Raw Job Layer

RawJob 是：

> Source Truth

建议：

```ts
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

---

# 20. Layer 3 — Job Understanding

V1.1.5 新增。

负责：

- Language Detection
- Translation
- Semantic Extraction
- Title Normalization
- Skill Extraction
- Responsibility Extraction
- Career Direction
- International Signals
- English Requirement
- Evidence Level

它回答：

> “这个 JD 在语义上讲了什么？”

而不是：

> “这个职位适不适合用户？”

---

# 21. Layer 4 — Normalized Job

NormalizedJob 是：

> 给下游系统使用的标准化职位对象。

建议包含：

```text
title
company
location
workMode
employmentType
salary
skills
responsibilities
industry
careerDirection
internationalEnvironment
companyType
englishRequirement
lifecycle
original
```

---

# 22. Layer 5 — Lifecycle

Lifecycle 独立于 Semantic Understanding。

原因：

> “职位讲什么”和“职位现在是否有效”是两个不同问题。

Lifecycle 负责：

- published
- updated
- refreshed
- deadline
- removed
- stale
- availability
- freshness
- activity evidence

---

# 23. Layer 6 — Deduplication

Dedup 应发生在：

> Career Engine 之前。

原因：

如果重复职位直接进入 Career Engine：

```text
same job
same company
same JD
```

可能产生：

- 重复结果
- 错误的职位数量
- 公司招聘活动被放大
- 用户重复看到同一机会

---

# 24. Layer 7 — Active Opportunity Pool

只有经过：

```text
Existence
+
Freshness
+
Activity
+
Zombie Filter
```

之后，才进入：

> Active Opportunity Pool

然后：

```text
Active Opportunity
↓
Career Engine
```

---

# 25. Layer 8 — Company Intelligence

公司层不应该依赖单个职位。

基本路径：

```text
Job
 ↓
SourceCompany
 ↓
Same-platform Other Jobs
 ↓
Recruitment Activity
 ↓
Company Profile
 ↓
Company Intelligence
```

---

# 26. SourceCompany 与 CanonicalCompany

必须区分。

## SourceCompany

平台上的公司实体。

例如：

```text
BOSS Company ID = 123
51Job Company ID = ABC
```

不能直接认为：

```text
123 == ABC
```

因为：

> Platform IDs are source-specific.

---

# 27. Canonical Company

未来如果需要跨平台合并：

```text
BOSS Company
51Job Company
Zhaopin Company
Liepin Company
        ↓
Canonical Company
```

这是：

> Cross-platform Entity Resolution

属于后续能力。

不是 V1.2 必做。

---

# 28. Company Job Aggregation

V1.2 的目标之一：

```text
Job
 ↓
Company
 ↓
Same-platform Other Jobs
```

例如：

```text
XX科技有限公司

├── AI视觉设计师
├── 内容运营
├── 产品运营
├── 电商运营
└── 产品助理
```

价值：

- 了解公司当前招聘活动
- 发现同公司其他适合职位
- 帮助用户看到更多机会
- 为 Company Intelligence 提供当前证据

但不能因此直接断言：

> 公司主营业务一定是某方向。

---

# 29. Company Profile

回答：

> “这家公司是谁？”

包括：

- Name
- Industry
- Location
- Company Size
- Business Description
- Source References

---

# 30. Company Intelligence

回答：

> “这家公司对当前用户有什么意义？”

包括：

- 当前观察到的招聘数量
- 最近招聘活动
- 多职位关系
- 国际化信号
- 用户相关岗位
- Evidence / Confidence

---

# 31. Observed Active Jobs

必须使用：

> Observed Active Jobs

而不是：

> Total Company Jobs

例如：

```text
Observed active jobs: 8
```

代表：

> 当前来源观察到 8 个符合当前生命周期判断的岗位。

不代表：

> 公司总共只有 8 个岗位。

---

# 32. Career Profile

Career Profile 只描述：

> User

包括：

- Education
- Experience
- Skills
- Career Directions
- Locations
- Work Mode
- Priorities
- Deal Breakers
- Long-term Goals
- Company Preferences

---

# 33. Company Preference

公司偏好应该独立于 Company Facts。

建议：

```ts
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

---

# 34. International Environment

不能只用：

```text
foreignCompany = true
```

应该拆开：

```text
Company Type
+
Global Team
+
Overseas Business
+
English Usage
+
Cross-border Collaboration
```

这样可以表达：

> 国内公司 + 全球团队

和：

> 外资公司 + 国际化工作环境

并不完全是同一回事。

---

# 35. Career Engine

Career Engine 是核心业务逻辑。

它负责：

> User ↔ Job

以及必要的：

> User ↔ Company / Career Context

匹配。

---

# 36. Career Engine 不负责

不负责：

- 从 BOSS 抓数据
- 判断某平台是否被封
- 翻译 JD
- 解析网页 HTML
- 获取公司页面
- 判断页面是否被 CAPTCHA 拦截
- 读取 Cookie
- 决定 Source 是否授权

这些属于上层 Source / Understanding / Infrastructure。

---

# 37. Immediate Fit

回答：

> “现在适不适合？”

重点：

- Skills
- Experience
- Responsibilities
- Location
- Work Mode
- Job Requirements

---

# 38. Career Growth Value

回答：

> “未来有没有价值？”

重点：

- Skill accumulation
- Transferable skills
- Career direction
- AI exposure
- Product / Content / Operations growth
- Industry outlook
- New capability exposure

---

# 39. Immediate Fit 与 Growth Value 必须独立

不能因为：

> “这个职位很有发展”

就认为：

> “现在很适合”。

也不能因为：

> “现在很适合”

就认为：

> “未来一定有价值”。

---

# 40. Feedback

Feedback 是：

> User Signal

不是：

> 自动修改 Career Profile 的命令。

例如：

```text
Rejected
```

只代表：

> Application outcome = rejected

不能直接解释：

> User dislikes this kind of job.

如果系统认为反馈可能反映偏好：

```text
Feedback
↓
Profile Update Suggestion
↓
User Confirmation
↓
Career Profile
```

---

# 41. V1.1.5 Architecture

```text
RawJob
   ↓
Language Detection
   ↓
Translation
   ↓
Semantic Extraction
   ↓
Concept Normalization
   ↓
International Signals
   ↓
NormalizedJob
   ↓
Existing Career Engine
```

关键：

> V1.1.5 是理解层，不是新的匹配引擎。

---

# 42. V1.1.5 数据边界

### Input

```text
RawJob
```

### Output

```text
NormalizedJob
```

### 不直接输入

```text
User Preference
```

### 不直接输出

```text
Recommended / Not Recommended
```

这样可以保持：

> Understanding 与 Matching 解耦。

---

# 43. V1.2 Architecture

```text
Sources
 ↓
Adapters
 ↓
RawJob
 ↓
Job Understanding
 ↓
Normalize
 ↓
Dedup
 ↓
Lifecycle
 ↓
Active Opportunity Pool
 ↓
Career Engine
```

同时：

```text
Job
 ↓
Company
 ↓
Same-platform Company Jobs
 ↓
Company Intelligence
```

---

# 44. Source Adapter 抽象

建议统一：

```ts
interface JobSourceAdapter {
  searchJobs(
    query: JobSearchQuery
  ): Promise<FetchResult>

  getJob?(
    sourceJobId: string
  ): Promise<FetchResult>

  getCompany?(
    sourceCompanyId: string
  ): Promise<FetchResult>

  getCompanyJobs?(
    sourceCompanyId: string
  ): Promise<FetchResult>
}
```

---

# 45. FetchResult

必须支持：

```ts
type FetchResult = {
  status:
    | "success"
    | "partial"
    | "blocked"
    | "challenged"
    | "unavailable"

  jobs: RawJob[]

  evidence?: {
    pageAccessible: boolean
    structuredDataAvailable: boolean
    resultCount?: number
  }
}
```

关键：

```text
success + 0
```

与：

```text
challenged + 0
```

完全不同。

---

# 46. Source Health

Source 是动态系统。

因此需要：

```ts
type SourceHealth = {
  sourceId: string

  status:
    | "healthy"
    | "degraded"
    | "unavailable"

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

---

# 47. Circuit Breaker

如果一个 Source 连续失败：

```text
healthy
 ↓
degraded
 ↓
unavailable
```

停止无意义重复请求。

恢复成功后：

```text
unavailable
 ↓
degraded
 ↓
healthy
```

---

# 48. Cache

Cache 的目的：

- 减少重复请求
- Source 暂时不可用时提供最近数据
- 支持增量更新
- 降低维护压力

但：

> Cache 数据必须带观察时间。

不能把旧数据伪装成实时数据。

---

# 49. Incremental Sync

使用：

> Content Hash

判断 JD 是否变化。

## 未变化

更新：

```text
observedAt
fetchedAt
```

而不必重复创建完整职位版本。

## 已变化

创建新 snapshot：

```text
Raw Snapshot
↓
Normalize
↓
Lifecycle
↓
Career Engine
```

---

# 50. Raw Snapshot

用于：

> Future Re-normalization

例如：

V1.2 的解析方式：

```text
description → skills
```

未来 V1.4 改进：

```text
description → skills + responsibilities + seniority
```

如果保存了 Raw Snapshot：

> 可以重新 Normalize，而无需重新访问 Source。

---

# 51. Tombstone

过期职位保留最小记录：

```text
source
sourceJobId
URL
company
title
firstSeen
expiredAt
reason
```

作用：

> 防止已经确认失效的职位再次被误认为新机会。

---

# 52. Source Lifecycle 差异

不同 Source 可以有不同信号。

例如：

```text
Greenhouse
→ updated_at

51Job
→ issueDate

Liepin
→ refresh / pubTime

Public Employment
→ publish / update / valid date
```

系统应该：

> Source-specific signal → Common Lifecycle Model

而不是：

> Common rule → force every Source

---

# 53. Source Capability Levels

Company Job Aggregation 使用：

```text
L0 Source exists but unverified
L1 Job discovery
L2 Job → Company
L3 Company → Other Jobs
L4 Company Jobs + Pagination
L5 Company Jobs + Lifecycle
L6 Stable API / Licensed
```

V1.2 Production Company Aggregation 条件：

> BOSS / 51Job / Zhaopin 中至少 2 个达到 L5。

---

# 54. 为什么不要求所有 Source 同时达到 L5

因为：

- Source capability 不同
- Access policy 不同
- 页面结构不同
- Lifecycle 数据完整程度不同

架构应该允许：

```text
BOSS = L5
51Job = L5
Zhaopin = L4
Liepin = L3
Lagou = L2
```

系统仍然可以工作。

---

# 55. Domestic Sources 的长期定位

五个平台全部保留：

```text
BOSS
51Job
Zhaopin
Liepin
Lagou
```

不是所有平台都必须：

> 同时达到相同技术能力。

它们是：

> Independent Source Adapters

---

# 56. Public Employment Sources 的定位

与国内招聘平台并行：

```text
Domestic Recruitment Platforms
          +
Public Employment
          +
Company Career Pages
          +
Stable APIs
          +
User Import
```

不是：

> Public Employment 替代招聘平台。

---

# 57. Stable Sources 的长期演进

架构支持：

```text
Experimental Source
        ↓
Validated
        ↓
Official / Licensed Source
        ↓
Stable Adapter
```

Branch 2 的作用是：

> 降低长期维护成本。

但：

> 不删除 Branch 1。

---

# 58. User Import 的架构地位

User Import 是：

> Permanent Fallback

它不只是临时开发工具。

如果：

```text
所有自动 Source unavailable
```

用户仍然可以：

```text
Paste JD
↓
RawJob
↓
Job Understanding
↓
Career Engine
```

因此项目不会因为某个招聘平台关闭接口而失去核心能力。

---

# 59. Four Strategic Branches

## Branch 1

Personal Job Search Experiment / Core Job Discovery

负责：

> 找真实职位。

## Branch 2

Stable / Long-term Data Sources

负责：

> 降低 Source 依赖风险。

## Branch 3

Company Intelligence

负责：

> 从职位进入公司层理解。

## Branch 4

Portfolio / Case Study

负责：

> 把整个系统包装成可展示的工程项目。

四条是：

> 并行战略方向。

不是：

> 互相替代的版本阶段。

---

# 60. 为什么 Company Discovery 必须从 Job 开始

系统真正关心的是：

> “哪些公司现在正在招与你相关的人？”

而不是：

> “网上有哪些大公司？”

因此：

```text
Job Discovery
↓
Company Discovery
↓
Company Recruitment Activity
```

比：

```text
Search Engine
↓
Company Directory
↓
Jobs
```

更符合个人求职场景。

---

# 61. Cross-platform Company Resolution 的长期原则

不能简单：

```text
companyName === companyName
```

未来可能使用：

- Unified Social Credit Code
- Official Domain
- Source Company ID
- Address
- Phone
- Description Similarity

并建立：

> Evidence-based Entity Resolution

但：

> V1.2 不需要完整实现。

---

# 62. 数据模型之间的关系

```text
RawJob
  ↓
NormalizedJob
  ↓
Career Engine

RawJob
  ↓
SourceCompany
  ↓
CompanyProfile
  ↓
Company Intelligence

CareerProfile
  ↓
Career Engine

CompanyPreference
  ↓
Career Engine
```

---

# 63. 不允许的依赖方向

禁止：

```text
Career Engine
↓
BOSS Adapter
```

禁止：

```text
Career Profile
↓
Raw Source Filter
```

禁止：

```text
Translation
↓
overwrite Original
```

禁止：

```text
Company Inference
↓
pretend as Source Fact
```

---

# 64. 推荐依赖方向

```text
Source
 ↓
RawJob
 ↓
Understanding
 ↓
NormalizedJob
 ↓
Lifecycle / Dedup
 ↓
Career Engine
```

以及：

```text
Job
 ↓
SourceCompany
 ↓
Company Intelligence
```

而：

```text
Career Profile
       ↓
Career Engine
       ↑
NormalizedJob
```

---

# 65. Version Boundary

## V1.1

稳定：

> Career Matching Foundation

## V1.1.5

增加：

> Job Understanding Foundation

不改变：

> Career Matching

## V1.2

增加：

> Real Job Discovery Infrastructure

不改变：

> Career Engine

## V1.3+

增加：

> Advanced Company Intelligence

---

# 66. V1.1.5 必须保护的东西

```text
Career Engine
Matching Formula
Immediate Fit
Career Growth Value
Career Profile semantics
Mock Jobs
Canonical Concepts
Original Job Text
```

---

# 67. V1.2 必须保护的东西

除了 V1.1.5 的全部内容，还必须保护：

```text
Source abstraction
RawJob
NormalizedJob
Lifecycle separation
Source health
User Import
```

---

# 68. 未来扩展不能破坏核心

未来即使增加：

- LinkedIn-like sources
- International job boards
- Freelance platforms
- Internship sources
- Campus jobs
- Government jobs
- Company career pages

都应该只新增：

```text
Adapter
```

而不是：

```text
Rewrite Career Engine
```

---

# 69. 架构成功标准

如果未来：

```text
BOSS API changes
```

只需要：

```text
Fix BossAdapter
```

而不是：

```text
Rewrite Career Engine
```

如果：

```text
Translation provider changes
```

只需要：

```text
Fix Translation Provider
```

而不是：

```text
Rewrite Matching
```

如果：

```text
Company Intelligence changes
```

也不应该：

```text
Rewrite Source Layer
```

---

# 70. 长期演进图

```text
V1.1
Career Matching
      ↓
V1.1.5
Job Understanding
      ↓
V1.2
Real Job Discovery
      ↓
V1.2+
Company Job Aggregation
      ↓
V1.3+
Company Intelligence
      ↓
Future
Career Intelligence System
```

---

# 71. 最终架构愿景

未来 Match Me Clever 可以从：

```text
“找工作”
```

逐步发展为：

```text
Job Discovery
      +
Job Understanding
      +
Company Intelligence
      +
Career Matching
      +
Career Growth Intelligence
```

但：

> 不需要现在一次性实现全部能力。

---

# 72. Architecture Decision Record

## ADR-001 — Career Engine 与 Source 解耦

**Decision:** Accepted

原因：

避免单一平台锁定。

---

## ADR-002 — RawJob 保留 Original

**Decision:** Accepted

原因：

保证 Source Truth 和未来重新解析能力。

---

## ADR-003 — Challenge 不等于 Zero

**Decision:** Accepted

原因：

避免 Source 风控造成错误结论。

---

## ADR-004 — Lifecycle 独立建模

**Decision:** Accepted

原因：

职位内容与职位有效性是不同维度。

---

## ADR-005 — Job-first Company Discovery

**Decision:** Accepted

原因：

更适合个人求职，降低对大公司搜索可见性的依赖。

---

## ADR-006 — Company Job Aggregation 先做 Same-platform

**Decision:** Accepted

原因：

比 Cross-platform Entity Resolution 简单、可靠、可控。

---

## ADR-007 — Cross-platform Company Resolution 延后

**Decision:** Accepted

原因：

身份解析复杂度高，不是 V1.2 核心目标。

---

## ADR-008 — User Import 是永久 Fallback

**Decision:** Accepted

原因：

保证 Source failure 不会让产品失去核心能力。

---

## ADR-009 — Facts / Inference 分离

**Decision:** Accepted

原因：

避免 AI 推断伪装成招聘方事实。

---

## ADR-010 — Foreign Company Preference 不直接等于 Score Bonus

**Decision:** Accepted

原因：

用户偏好与公司事实应先分离，再由 Career Engine 统一解释。

---

## ADR-011 — 一个 Canonical Concept System

**Decision:** Accepted

原因：

避免多套技能 / 概念词典导致匹配结果不一致。

---

## ADR-012 — Source Resilience 优先于 Anti-bot Bypass

**Decision:** Accepted

原因：

长期维护性、安全性、架构稳定性高于短期抓取成功率。

---

# 73. 当前架构中最重要的边界

```text
┌───────────────────────────┐
│       Source Layer        │
│ “Where does data come from?”│
└─────────────┬─────────────┘
              ↓
┌───────────────────────────┐
│   Job Understanding       │
│ “What does this JD mean?” │
└─────────────┬─────────────┘
              ↓
┌───────────────────────────┐
│   Company Intelligence    │
│ “What do we know about    │
│    this hiring context?”  │
└─────────────┬─────────────┘
              ↓
┌───────────────────────────┐
│      Career Profile       │
│    “Who is the user?”     │
└─────────────┬─────────────┘
              ↓
┌───────────────────────────┐
│      Career Engine        │
│ “How does this fit the    │
│        user?”             │
└───────────────────────────┘
```

---

# 74. 最重要的不可破坏架构规则

1. **Career Engine 不依赖任何招聘平台。**
2. **Source Adapter 不负责职业匹配。**
3. **RawJob 永远保留原始信息。**
4. **Translation 永远不能覆盖 Original。**
5. **只有一套 Canonical Concept Normalization。**
6. **Facts、Evidence、Inference 分离。**
7. **缺失证据不是 False。**
8. **Page Exists 不等于 Active Opportunity。**
9. **Freshness 与 Availability 分开。**
10. **Challenge / Blocked 不等于 Zero Jobs。**
11. **用户偏好不污染 Source Facts。**
12. **User Import 必须长期存在。**
13. **单一 Source 挂掉不能导致系统失效。**
14. **Company Job Aggregation 优先 Same-platform。**
15. **Cross-platform Company Resolution 延后。**
16. **不为了新功能重写核心 Career Engine。**
17. **不把项目做成招聘平台数据库镜像。**
18. **不以绕过 Anti-bot 作为系统能力。**
19. **Source-specific lifecycle rules 不应被统一规则强行覆盖。**
20. **所有重要 AI 判断都应尽可能保留 Evidence / Confidence。**

---

# 75. Architecture Review Checklist

以后每增加一个功能，先问：

### 数据

- 是否保留 Original？
- 是否需要 Raw Snapshot？
- 是否能重新 Normalize？
- 是否污染 Source Fact？

### Source

- 是否需要新增 Adapter？
- 是否有 Access Policy？
- 失败时是什么状态？
- 是否会把 Challenge 错误解释为 Zero？

### Understanding

- 是否使用现有 Canonical Concept？
- 是否区分 Translation 与 Original？
- 是否区分 Fact 与 Inference？

### Company

- 是否需要 SourceCompany？
- 是否需要 CompanyProfile？
- 是否误把 SourceCompany 当 CanonicalCompany？

### Matching

- 是否真的需要修改 Career Engine？
- 是否改变 Immediate Fit？
- 是否改变 Career Growth Value？
- 是否改变现有用户行为？

如果答案是：

> “为了这个新 Source 必须修改 Career Engine”

首先应该重新检查架构，而不是立即修改 Engine。

---

# 76. 最终架构判断标准

一个新功能如果满足：

```text
新增能力
+
不破坏现有模块
+
可以替换 Source
+
可以回退
+
保留原始数据
+
证据可追溯
+
不会污染 Career Engine
```

则通常符合 Match Me Clever 的长期架构。

---

# END OF ARCHITECTURE
