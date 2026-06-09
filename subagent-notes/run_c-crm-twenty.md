# 角色 C 研究备忘录：CRM / 业务系统架构底座

## 结论先行

如果目标是做一个 AI 辅助销售工具，建议把 **twentyhq/twenty** 作为“客户主数据 + 销售流程 + 活动归档 + 权限/API/工作流”的候选底座，而不是把它当作一个单纯的 CRM 页面模板。Twenty 的价值在于：它已经把 CRM 的核心对象、关系、视图、权限、API、Webhooks、工作流和正在演进的 AI agents 都做成平台能力，适合作为 AI 销售系统的 system of record。

本地列表中其他仓库更像“销售/营销动作引擎”或“内容/GEO/SEO 工具包”，不适合单独承担 CRM 底座：

- `ericosiu/ai-marketing-skills`：有 `sales-pipeline`、`lead-dossier`、`outbound-engine`、`revenue-intelligence` 等销售动作能力，适合接到 Twenty 外围，负责线索识别、富集、外呼、归因、Gong 通话洞察等。
- `coreyhaines31/marketingskills`：有 `revops`、`prospecting`、`sales-enablement` 等策略/流程型技能，适合定义生命周期、评分、路由、SLA、销售物料，不是数据系统。
- `zubair-trabzada/geo-seo-claude`：内含 `geo-prospect` CRM-lite，可管理 GEO 服务销售线索和 proposal pipeline，但只是 JSON/CLI 轻量管道，领域很窄，不适合作为通用 CRM。
- `AgriciDaniel/claude-seo`、`oaker-io/wewrite`：偏 SEO 审计、公众号/内容生产，最多作为营销内容和销售证据来源，不是 CRM/客户资料/销售流水线底座。

## 1. 项目用意

### Twenty 的定位

Twenty 官方 README 将其定位为 “The #1 Open-Source CRM”，并进一步说明它给技术团队提供“构建自定义 CRM 的 building blocks”，让 CRM 能像业务代码一样构建、发布、版本化。它不是只复制 HubSpot/Salesforce 的固定字段，而是强调：

- 对象、字段、关系可以按业务建模。
- 标准 CRM 对象开箱可用。
- 自定义对象也能拥有同等的 API、视图、权限和工作流触发能力。
- 支持 Cloud、自托管、以及通过 Twenty app/SDK 方式扩展。

这对 AI 销售工具尤其关键：AI 不是只需要一个联系人表，而是需要可查询、可更新、可触发、可追踪权限边界的业务图谱。Twenty 的产品方向正好是把 CRM 从“销售软件”拉到“可编程客户业务系统”。

### Twenty 的平台形态

Twenty README 和文档展示了几层能力：

- 数据层：Objects、Fields、Relations，含标准对象和自定义对象。
- 视图层：Table、Kanban、Calendar、过滤、排序、聚合、个人/团队视图。
- 自动化层：Workflows、HTTP request、Webhook trigger、定时任务、记录变更触发、代码动作。
- 集成层：REST/GraphQL API、Metadata API、Webhooks、OAuth/Connections。
- AI 层：AI chatbot、AI agents、skills/agents、逻辑函数中的 `runAgent()`，但其中一部分仍标注为开发中、beta 或 alpha。
- 应用扩展层：Twenty Apps 可声明对象、字段、视图、页面布局、前端组件、逻辑函数、AI skills/agents。

因此，Twenty 的项目用意可概括为：**面向技术团队的开源、可扩展、可版本化 CRM 平台**，既能直接当 CRM 用，也能当作垂直业务系统的数据和流程底座。

## 2. 可复用能力

### A. 标准 CRM 对象和关系

Twenty 开箱标准对象包括：

- `Companies`：业务往来的组织/账户。
- `People`：联系人，包含联系方式和交互历史。
- `Opportunities`：商机/交易，记录阶段、金额、关联账户、预计关闭日期等。
- `Tasks`：待办和行动项，可关联 People、Companies、Opportunities 等记录。
- `Notes`：自由文本备注，可挂到 People、Companies、Opportunities 和其他记录。

标准关系包括：

- People -> Companies：多人属于一个公司。
- Opportunities -> Companies：商机属于公司。
- Opportunities -> People：商机可关联联系人。
- Notes/Tasks 这类活动对象可关联到多个业务对象，适合承载活动上下文。

这套模型已覆盖一个 AI 销售系统最基础的客户图谱：公司、联系人、商机、待办、备注、活动。

### B. 自定义对象、字段、关系

Twenty 的核心复用价值不是标准对象本身，而是可以把其他销售智能实体变成一等对象。例如：

- `Lead`：如果团队需要把“未进入商机的线索”与联系人区分开，可以创建自定义对象。
- `IntentSignal`：网站访问、招聘、融资、竞品搜索、GitHub 行为等购买信号。
- `OutboundSequence`：外呼/邮件序列定义和状态。
- `CampaignEnrollment`：某联系人进入哪个营销/销售序列，当前 step、回复状态。
- `AccountResearchDossier`：公司研究报告、技术栈、招聘信号、新闻信号、AI 摘要。
- `CallInsight`：Gong/会议录音提取出的 objection、buying signal、competitor mention。
- `LifecycleEvent`：如果需要更规范的全渠道事件流，可独立建对象，而不仅依赖 Notes/Tasks/Messages。
- `LeadScoreSnapshot`：保存每次评分版本、分数、证据、模型/规则版本，便于审计。

Twenty 的文档明确说自定义对象会获得与内置对象一致的 API endpoints、views、permissions、workflow triggers。这一点对 AI 系统非常重要，因为 AI 生成的数据不能只停留在外部 JSON；它需要进入 CRM 图谱，受权限、视图和工作流管控。

### C. 视图和 pipeline 展示

Twenty 的 Kanban view 可将任意 Select field 的值作为列。Sales Pipeline 文档明确把 Opportunities 的 Stage 字段配置为销售阶段，并建议：

- New
- Qualified
- Meeting
- Proposal
- Negotiation
- Closed Won
- Closed Lost

Kanban 支持拖拽更新阶段、显示关键字段、compact view、列聚合，比如按 Amount 求和显示每阶段 pipeline value。Table view、过滤、排序、个人/团队视图也可支持销售经理、BDR、AE 的不同工作台。

这意味着 Twenty 可直接承载销售流水线，而 AI 工具只需要把推荐、评分、下一步动作写回对应对象/字段。

### D. 工作流与业务自动化

Twenty Workflows 可以通过记录创建/更新、定时任务、Webhook、HTTP 请求、代码动作等方式自动化流程。官方文档示例包括：

- 通过 Typeform webhook 创建 People/lead。
- 定时检测 stale opportunities。
- 给即将到期或逾期的任务发提醒。
- Closed won 后触发后续动作。
- 使用 AI triage 入站邮件并自动 threaded reply。

这些能力可以复用为：

- 表单/网站访客/外部工具入站后创建或更新联系人、公司、线索。
- 线索评分达到阈值后创建任务或商机。
- 商机久未更新时提醒销售或经理。
- 入站邮件/会议后自动生成摘要、任务、下一步建议。
- Closed won 后把客户交接给 onboarding/customer success。

### E. API、Webhooks、OAuth、App 扩展

Twenty 的 API 不是固定 schema，而是由 workspace schema 生成：

- Core API：`/rest/` 和 `/graphql/`，可 CRUD People、Companies、Opportunities、自定义对象，查询、过滤、遍历关系。
- Metadata API：`/rest/metadata/` 和 `/metadata/`，可管理对象、字段、关系。
- GraphQL 支持关系遍历、batch upsert 等。
- Webhooks 会在记录 create/update/delete 时 POST 出去，覆盖标准和自定义对象。
- Logic functions 可被 HTTP、cron、database event、AI tool call、workflow action 触发。
- Apps 可声明 OAuth Connections，让逻辑函数代表用户调用第三方服务。

对 AI 辅助销售工具而言，这些集成面意味着：

- 外部 AI 服务可以通过 API 拉取客户上下文、写回评分/摘要/任务。
- Twenty 可以通过 webhook 推送变更给 AI scoring/enrichment worker。
- Twenty app 可以把部分 AI 能力嵌入工作区内部，而不只是外部服务。
- Metadata API 可用于按业务阶段自动安装/升级数据模型，但要谨慎管理 schema 迁移。

### F. 邮件、日历、活动数据

Twenty 支持连接 Google、Microsoft，以及 SMTP/CalDAV。邮件和日历可按用户配置同步，外部邮件/会议可关联到 CRM 记录，并且可以自动创建联系人和公司。关键点：

- 邮件可选择 Metadata Only、Subject and Metadata、All Email Content，适合不同隐私策略。
- 自动创建联系人时，可按邮箱域名关联或创建 Company。
- 邮件/日历同步每 5 分钟更新。
- Message 对象有 `headerMessageId`，可用于 threaded reply。
- 官方自动回复示例通过 Message、Message Participants、AI Agent、Send Email 完成入站邮件 triage 和回复。

这为“活动时间线”提供了重要来源：邮件、会议、备注、任务、AI 摘要可以共同构成客户/商机历史。

## 3. 如何承载线索、联系人、商机、任务、活动时间线

### 线索 Lead

Twenty 标准对象没有在核心对象列表中突出单独的 `Lead`，但有两种可行建模方式：

方案一：用 `People` 作为线索和联系人统一对象。

- 给 People 增加字段：`Lifecycle Stage`、`Lead Status`、`Lead Source`、`Fit Score`、`Intent Score`、`MQL Date`、`SQL Date`、`Owner`、`Last Intent Signal At`。
- 用视图区分 Raw Lead、MQL、SQL、Recycled、Disqualified。
- 适合早期团队，模型简单，避免线索转联系人时的数据迁移。

方案二：创建自定义 `Lead` 对象。

- Lead 记录表单提交、匿名访客识别、Apollo/Clay/RB2B 导入、活动报名等“尚未确认的人/公司”。
- Lead 通过关系指向 People、Companies，或在 qualify 后转换/合并为 People + Opportunity。
- 增加字段：`source`、`status`、`score`、`qualificationReason`、`disqualificationReason`、`assignedTo`、`nextAction`、`conversionDate`。
- 适合有 MQL/SQL 明确交接、营销归因、去重、合规审计需求的团队。

建议：如果是做 AI 辅助销售工具，优先使用方案二或“People + Lifecycle Stage + IntentSignal 对象”的混合方案。原因是 AI 评分和富集会生成大量中间状态，不宜直接污染联系人主记录。

### 联系人 Contact / Person

用 Twenty `People` 承载：

- 基本字段：姓名、邮箱、电话、职位、LinkedIn、地理位置。
- 关系：Company、Opportunities、Tasks、Notes、Messages、Meetings、LeadScoreSnapshots、IntentSignals。
- AI 字段：`personaSummary`、`painHypothesis`、`buyingRole`、`lastTouchSummary`、`recommendedNextAction`、`doNotContactReason`。

AI 销售工具应把 People 当成“人”的主记录，而不是把每次线索导入都生成新联系人。必须配合去重策略：邮箱、邮箱域名、LinkedIn URL、公司关系、外部系统 ID。

### 公司 Account / Company

用 Twenty `Companies` 承载：

- 基本字段：行业、规模、地点、网站、域名、年收入、技术栈、ICP 匹配度。
- 关系：People、Opportunities、Notes、Tasks、IntentSignals、AccountResearchDossier。
- AI 字段：`accountSummary`、`businessModel`、`techStackSummary`、`recentSignals`、`ICP Fit Score`、`Account Tier`、`Open Questions`。

本地 `lead-dossier` 的 account research 输出适合写入 Company 的自定义字段或关联 `AccountResearchDossier` 对象。

### 商机 Opportunity

用 Twenty `Opportunities` 承载：

- 标准字段：名称、阶段、金额、公司、联系人、预计关闭日期、owner。
- 建议阶段：New、Qualified、Meeting/Discovery、Proposal、Negotiation、Closed Won、Closed Lost。也可按照团队 motion 调整。
- AI 字段：`dealHealth`、`riskReason`、`nextBestAction`、`lastInteractionSummary`、`objections`、`competitorsMentioned`、`closePlanCompleteness`。
- 自动化：阶段久未更新提醒、阶段变化创建任务、Closed Won 自动交接、Closed Lost 记录 loss reason。

Twenty 的 Kanban + column aggregation 已能支持 sales pipeline 的核心展示；AI 层重点应放在“为什么这个商机该推进/卡住/复活”。

### 任务 Task

用 Twenty `Tasks` 承载：

- 任务类型：Call、Email、Research、Follow-up、Proposal、Manager Review、Renewal/Expansion。
- 关系：People、Companies、Opportunities。
- 字段：due date、assignee、priority、status、source、AI generated、approval required。
- 工作流：MQL 到达后创建 follow-up task；入站邮件需人工处理时建任务；商机 stale 时建 manager intervention task。

AI 生成任务时要区分“建议”和“执行”：建议型任务可以直接创建，外发邮件/改阶段/关闭商机这类高影响动作应有人工确认。

### 活动时间线 Activity Timeline

Twenty 可用多对象组合承载活动时间线：

- Messages：同步邮件，含发件人/收件人、subject、body 或 metadata、`headerMessageId`。
- Calendar Events：同步会议，并关联 People/Company。
- Notes：会议纪要、人工备注、AI 摘要、客户背景。
- Tasks：待办、完成记录、跟进动作。
- Opportunity stage changes：可通过字段更新时间和工作流记录为 Note 或自定义 event。
- 自定义 `LifecycleEvent` 或 `ActivityEvent`：如果要做跨渠道统一时间线，建议创建标准化事件对象，记录 `eventType`、`source`、`occurredAt`、`actor`、`relatedPerson`、`relatedCompany`、`relatedOpportunity`、`payload`、`summary`。

建议做 AI 销售工具时，不要只依赖 Notes 做所有活动，否则后期难以查询和归因。可以保留 Notes 作为人类可读层，同时用自定义事件对象保存结构化事实。

## 4. 与营销 / 销售推进的关系

### Twenty 在营销到销售闭环中的位置

Twenty 最适合承担中间的“客户与商机事实层”：

```
营销获客/意图识别 -> Twenty 线索/联系人/公司 -> AI 评分/富集/路由
               -> 销售任务/商机推进 -> 邮件/会议/通话洞察
               -> 商机结果/归因 -> ICP/内容/外呼策略迭代
```

营销系统和销售推进工具不应取代 CRM，它们应把数据写入 Twenty，或从 Twenty 拉上下文。

### 本地候选仓库的适配关系

#### ericosiu/ai-marketing-skills

这是最值得接到 Twenty 的外围动作层。

- `sales-pipeline`：支持 RB2B visitor -> intent scoring -> suppression -> Instantly routing；HubSpot dead deal resurrector；trigger prospector；ICP learning analyzer。
- `lead-dossier`：支持 account research、cascade enrichment、lead pipeline、real-time lead enrichment。
- `outbound-engine`：支持 cold outbound campaign、Instantly 审计、ICP、专家组评分、email sequence。
- `revenue-intelligence`：支持 Gong transcript insight、GA4 + HubSpot revenue attribution、client reporting。

集成到 Twenty 的方式：

- RB2B/Typeform/网站表单进入 Twenty webhook workflow 或外部 worker，再创建 Lead/Person/Company。
- `lead-dossier` 输出写入 Company/Person 及 `AccountResearchDossier`。
- `sales-pipeline` 的 scoring/routing 写入 LeadScoreSnapshot、Task、Owner、Lifecycle Stage。
- `outbound-engine` 只在人工批准后把联系人加入 Instantly/Lemlist/Outreach，回写 enrollment 和回复状态。
- `revenue-intelligence` 的 call insights 写入 Opportunity/CallInsight/Notes，用于 next best action。

#### coreyhaines31/marketingskills

它不是 CRM 实现，而是 RevOps 和营销方法论工具。

- `revops` 明确提出 single source of truth、lead lifecycle、MQL/SQL handoff SLA、lead scoring、routing、pipeline stages、CRM automation、dashboard。
- `prospecting`、`cold-email`、`sales-enablement`、`customer-research` 可用于生成策略、列表、邮件、销售物料。
- tools registry 记录了 HubSpot、Salesforce、Close、Apollo、Clay、RB2B、Gong、Instantly、Outreach 等工具的定位和集成方式。

适配关系：用它定义 Twenty 里的字段、阶段、SLA、评分规则、仪表盘指标；不要把它当作系统本体。

#### zubair-trabzada/geo-seo-claude

`geo-prospect` 是一个面向 GEO agency 的 CRM-lite：

- 支持 prospect new/list/show/audit/note/status/won/lost/pipeline。
- 状态包括 lead、qualified、proposal、won、lost。
- 数据存在 `~/.geo-prospects/prospects.json`，含 domain、company、contact、geo_score、audit_file、proposal_file、monthly_value、notes。

它的价值是“轻量 prospect pipeline 设计样例”：很适合参考字段和命令体验，但不适合作为通用 CRM 底座，原因是：

- 存储是单 JSON 文件，缺少多用户、权限、API、关系模型、去重、审计。
- 领域固定在 GEO 服务销售。
- 不承载邮件/日历/任务/跨对象活动时间线。

#### claude-seo 与 wewrite

这两个仓库可服务营销内容和销售证据生产：

- `claude-seo` 偏 SEO/GEO 审计、搜索与内容质量发现，可产出对客户有价值的诊断报告、销售发现、痛点证据。
- `wewrite` 偏中文内容生产、选题、风格、公众号发布，不具备 CRM 能力。

适配关系：它们可以生成 AccountResearchDossier、Proposal Evidence、Content Assets，再写入 Twenty 的 Company/Opportunity/Notes。不要让它们承担客户主数据。

## 5. 做 AI 辅助销售工具时是否建议基于 Twenty，如何集成

### 建议程度

建议基于 Twenty 做原型和中小团队版本，尤其在以下前提成立时：

- 希望自托管或保留开源可控性。
- 需要自定义 CRM 数据模型，而不是完全受 HubSpot/Salesforce 限制。
- 团队有 TypeScript/NestJS/React/Postgres 能力。
- AI 工具需要深入读写 CRM 对象、关系、任务、备注和活动。
- 愿意接受 Twenty AI agents/chatbot 仍有 alpha/beta/开发中能力，需要外部 AI 服务兜底。

不建议把 Twenty 作为唯一底座的情况：

- 企业已经深度绑定 Salesforce/HubSpot，且迁移成本不可接受。
- 需要成熟的企业级 forecast、quota、CPQ、复杂 territory、审批、审计报表。
- 需要即插即用的大量原生成熟销售生态，而不是自建集成。
- 对 AI agents 功能要求“现在就稳定生产可用”，但不愿构建外部 agent 服务。

总体判断：**Twenty 适合做 AI-native CRM 的系统底座，但 AI 销售动作层应外置/插件化，不应完全依赖 Twenty 当前内置 AI 功能。**

### 推荐架构

```
                   外部信号 / 营销系统
     Typeform, RB2B, Apollo, Clay, Ads, GA4, Website, Gong
                              |
                              v
              Ingestion / Enrichment / Scoring Workers
        lead-dossier, sales-pipeline, outbound, call insight
                              |
       REST/GraphQL API + Webhook Workflow + Twenty App Logic
                              |
                              v
                         Twenty CRM
 Companies / People / Leads / Opportunities / Tasks / Notes / Messages
 IntentSignals / AccountDossiers / CallInsights / ScoreSnapshots
                              |
                              v
                       Sales Workbench / AI Copilot
       next best action, draft emails, meeting brief, deal risk, manager alerts
```

### 数据模型建议

基于 Twenty 标准对象：

- Companies：账户主数据。
- People：联系人主数据。
- Opportunities：商机。
- Tasks：行动项。
- Notes：人工备注、AI 摘要、会议纪要。
- Messages / Calendar Events：邮件和会议活动。

新增自定义对象：

- Lead：入站/外呼前线索，未必已确认联系人。
- IntentSignal：来源、行为、分数、证据、发生时间。
- AccountResearchDossier：公司研究报告和富集结果。
- CallInsight：会议/通话中的 objection、buying signal、competitor mention、follow-up。
- CampaignEnrollment：外呼/营销序列参与记录。
- LeadScoreSnapshot：评分版本、得分、解释、触发动作。
- LifecycleEvent：统一活动事件，供 AI 检索和时间线汇总。

字段建议：

- People：lifecycleStage、leadStatus、fitScore、engagementScore、lastContactedAt、lastMeaningfulInteractionAt、buyingRole、personaSummary、doNotContact。
- Companies：accountTier、icpFitScore、industry、employeeRange、techStack、recentSignalsSummary、targetAccountOwner。
- Opportunities：stage、amount、closeDate、owner、dealHealth、riskReason、nextBestAction、lastStageChangedAt、lossReason、competitor。
- Tasks：source、aiGenerated、approvalRequired、priority、dueAt、completedAt。

### 集成方式建议

#### 1. 入站线索

- Typeform/网站表单/RB2B -> Twenty Workflow Webhook Trigger 或外部 API ingestion。
- 创建或更新 Lead/Person/Company。
- 建 IntentSignal 和 LeadScoreSnapshot。
- 达到阈值后分配 owner、创建 Task、必要时创建 Opportunity。

#### 2. 线索富集

- 外部 worker 调用 `lead-dossier`、Apollo/Clay/Clearbit、BuiltWith、Brave/Exa 等。
- 富集结果写入 Company/People 字段，完整报告写 `AccountResearchDossier`。
- 不确定或低置信字段不要覆盖主字段，先写入 “suggested fields” 或 note，由人工确认。

#### 3. AI 评分与路由

- Twenty record created/updated webhook 触发 scoring worker。
- Scoring worker 读取 People/Company/IntentSignal/历史活动。
- 写回 LeadScoreSnapshot、fitScore、engagementScore、routingReason。
- Workflow 根据分数和字段创建任务、发 Slack/Email、分配 owner。

#### 4. 销售推进

- Sales rep 在 Twenty Opportunity Kanban 中推进阶段。
- AI 根据活动时间线生成 next best action、follow-up draft、meeting brief。
- 对外发送动作保持人工批准，除非是低风险确认邮件或内部提醒。
- Stale Opportunity workflow 每日检查未更新商机，提醒 rep/manager。

#### 5. 邮件与会议

- 用 Twenty 邮箱/日历同步作为活动事实来源。
- 入站 Message created 后触发 AI triage：垃圾/新闻跳过，真实销售回复生成摘要和任务。
- 会议结束后写 Note/CallInsight，并更新 Opportunity 的 nextBestAction 和 dealHealth。

#### 6. 外呼工具

- Instantly/Lemlist/Outreach 不直接成为事实源；它们负责发送和序列执行。
- Twenty 记录 CampaignEnrollment 和关键状态：enrolled、step、reply、positive reply、meeting booked、unsubscribed。
- 回复或会议结果回写 People/Opportunity/IntentSignal。

#### 7. Revenue intelligence / 归因

- GA4、Gong、HubSpot-style attribution 工具输出统一写入 Twenty。
- 内容/活动对机会和 closed won 的影响可作为 Opportunity 的关联对象或 `AttributionTouch` 自定义对象。
- Gong/通话洞察写 `CallInsight`，再驱动 sales enablement、content gaps、objection handling。

### AI 边界与风险

需要特别注意：

- Twenty 的 AI chatbot/agents 文档显示部分功能仍处于开发中、beta 或 alpha，不宜把生产系统完全压在内置 AI 上。
- AI 自动写 CRM 容易造成脏数据，必须保留 `source`、`confidence`、`modelVersion`、`generatedAt`、`reviewStatus`。
- 邮件正文和会议内容涉及隐私，Twenty 邮件同步支持 metadata-only/subject-only/full-content，AI 处理前应按客户隐私策略选择。
- 外发邮件、改 deal stage、标记 closed lost、删除/合并记录等动作应默认人工确认。
- Webhooks 当前文档说明所有对象变更都会发送，未来才可能支持事件过滤，因此外部 worker 要自行过滤、去重、防循环。
- GraphQL/REST rate limit 为 100 requests/min，batch size 60；大规模富集和导入要做队列、批处理和退避。

### 最小可行实现路线

第一阶段：CRM 基础

- 部署 Twenty Cloud 或自托管。
- 使用 Companies、People、Opportunities、Tasks、Notes。
- 配置 Opportunities stage 和 Kanban pipeline。
- 创建 Lead、IntentSignal、AccountResearchDossier、LeadScoreSnapshot 自定义对象。

第二阶段：入站和评分

- 接 Typeform/网站表单/RB2B webhook。
- 做 Lead/Company/People 去重和创建。
- 外部 AI scoring worker 写回分数、理由、下一步任务。
- 配置 MQL -> Task/Owner/Opportunity workflow。

第三阶段：销售 copilot

- 基于 People/Company/Opportunity 页面生成 meeting brief、last touch summary、next best action。
- 接邮件/日历同步，入站邮件自动 triage 和摘要。
- 接 Gong 或 transcript 输入，生成 CallInsight。

第四阶段：外呼和闭环

- 接 Instantly/Lemlist/Outreach，写 CampaignEnrollment。
- 回复、会议、商机结果回写 Twenty。
- 用 closed-won/lost 训练或校准 ICP、评分、外呼文案。

## 最终建议

Twenty 值得作为 AI 辅助销售系统的 CRM/业务底座候选，尤其适合“开源可控 + 自定义对象 + AI agent 外挂 + 销售流程可配置”的产品方向。它不应被理解成一个现成的 AI 销售全家桶，而应作为客户事实层和流程层：

- Twenty 管对象、关系、权限、时间线、pipeline、任务和工作流。
- `ai-marketing-skills` 这类仓库管线索发现、富集、外呼、通话洞察和归因。
- `marketingskills` 管 RevOps 策略、生命周期、评分规则和销售物料。
- `geo-seo-claude`/`claude-seo`/`wewrite` 管垂直领域的营销内容、审计报告和销售证据。

我的建议是：**基于 Twenty 做系统底座，围绕它构建外部 AI sales intelligence layer；短期不要深度依赖 Twenty 尚在 alpha/beta 的 AI agents，而是通过 REST/GraphQL、Webhooks、Workflows 和 Twenty Apps 把 AI 能力逐步嵌入。**

## 主要来源

- Twenty GitHub README：`https://github.com/twentyhq/twenty`
- Twenty docs index：`https://docs.twenty.com/llms.txt`
- Twenty Data Model：`https://docs.twenty.com/getting-started/core-concepts/data-model.md`
- Twenty Objects：`https://docs.twenty.com/user-guide/data-model/capabilities/objects.md`
- Twenty Relation Fields：`https://docs.twenty.com/user-guide/data-model/capabilities/relation-fields.md`
- Twenty Set Up a Sales Pipeline：`https://docs.twenty.com/user-guide/views-pipelines/how-tos/set-up-a-sales-pipeline.md`
- Twenty Kanban Views：`https://docs.twenty.com/user-guide/views-pipelines/capabilities/kanban-views.md`
- Twenty APIs：`https://docs.twenty.com/developers/extend/api.md`
- Twenty Webhooks：`https://docs.twenty.com/developers/extend/webhooks.md`
- Twenty Calendar & Emails：`https://docs.twenty.com/user-guide/calendar-emails/overview.md`
- Twenty Logic Overview：`https://docs.twenty.com/developers/extend/apps/logic/overview.md`
- Twenty Skills & Agents：`https://docs.twenty.com/developers/extend/apps/logic/skills-and-agents.md`
- Twenty AI Chatbot：`https://docs.twenty.com/user-guide/ai/capabilities/ai-chatbot.md`
- Twenty AI Agents：`https://docs.twenty.com/user-guide/ai/capabilities/ai-agents.md`
- Twenty Auto-Reply to Inbound Emails：`https://docs.twenty.com/user-guide/workflows/how-tos/crm-automations/auto-reply-to-inbound-emails.md`
- 本地仓库：`work/research-repos/ai-marketing-skills`
- 本地仓库：`work/research-repos/marketingskills`
- 本地仓库：`work/research-repos/geo-seo-claude`
- 本地仓库：`work/research-repos/claude-seo`
- 本地仓库：`work/research-repos/wewrite`
