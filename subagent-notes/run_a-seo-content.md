# 角色 A 研究备忘录：SEO/GEO/AI Marketing/内容增长仓库对 AI 辅助销售工具的启发

研究日期：2026-06-10  
角色：A，SEO/内容增长研究员  
研究对象：
- zubair-trabzada/geo-seo-claude，本地克隆提交 `9eec32f`，2026-05-26
- AgriciDaniel/claude-seo，本地克隆提交 `dabfc1a`，2026-05-25
- coreyhaines31/marketingskills，本地克隆提交 `7f4af1e`，2026-05-29
- ericosiu/ai-marketing-skills，本地克隆提交 `a9f1100`，2026-05-27
- oaker-io/wewrite，本地克隆提交 `e30a6df`，2026-06-01

资料来源：联网浅克隆 GitHub 仓库并读取 README、SKILL.md、docs、references、scripts、工具注册表与关键 Python/Node 脚本。未改动任何源代码。

## 一句话结论

这 5 个仓库展示了三类可迁移能力：第一类是 GEO/SEO 诊断与站点优化，把“被搜索引擎和 AI 引擎看见”转成可评分、可交付、可复盘的系统；第二类是营销与销售技能编排，把产品定位、内容、获客、RevOps、销售物料放到同一套工作流里；第三类是内容生产闭环，尤其是 `wewrite` 对中文公众号从热点、选题、素材、写作、SEO、配图、排版、发布、复盘的全流程封装。对 AI 辅助销售工具最关键的启发是：不要只做“写邮件/写话术”，而要做“市场信号发现 -> 账户诊断 -> 价值假设 -> 个性化内容 -> 合规触达 -> CRM/销售动作 -> 收入读回”的闭环。

## 可直接借鉴的产品架构

建议把 AI 辅助销售工具拆成 7 个模块：

1. 信号发现层：GSC、Ahrefs/DataForSEO、站点抓取、AI 引擎可见性、访问者识别、招聘/融资/竞品新闻、销售通话等。
2. 账户诊断层：对目标公司站点做 SEO/GEO/内容/技术/结构化数据/转化体验诊断，形成“为什么现在值得找他”的证据。
3. 机会评分层：用 Impact x Confidence、GEO Score、Intent Score、ICP Fit、Speed-to-lead、Deal Resurrect Score 等多维评分决定优先级。
4. 内容与话术层：基于诊断证据生成邮件、LinkedIn 私信、销售 one-pager、提案、demo talk track、竞品 battle card。
5. 销售工作流层：线索去重、压制名单、路由到 campaign、CRM 阶段、跟进任务、复活旧 deal、自动创建销售素材。
6. 质量与合规层：专家面板评分、AI 写作痕迹检查、事实校验、来源记录、CAN-SPAM/GDPR/平台 ToS 约束、人工审批门。
7. 收入读回层：用 HubSpot/Salesforce、GA4、Gong、GSC、outbound 平台数据判断动作是否真的提升回复率、会议率、pipeline、成交与内容辅助收入。

## 1. zubair-trabzada/geo-seo-claude

GitHub：<https://github.com/zubair-trabzada/geo-seo-claude>

### 用意/目标

该仓库定位为 “GEO-first, SEO-supported”，核心目标是帮助网站适配 ChatGPT、Claude、Perplexity、Gemini、Google AI Overviews 等 AI 搜索/回答引擎，而不只是传统 Google 排名。它把 GEO 拆成可执行的 Claude Code skill：`/geo audit`、`/geo quick`、`/geo citability`、`/geo crawlers`、`/geo llmstxt`、`/geo brands`、`/geo schema`、`/geo proposal`、`/geo prospect` 等。

它的业务意图也很明显：不只是做诊断工具，而是服务 GEO agency 的销售闭环。仓库内包含 CRM-lite prospect pipeline、proposal 生成、monthly delta report、white-label 配置、client-ready report 与 PDF 报告模板，说明作者面向“用 GEO 审计卖咨询/代运营服务”的商业场景。

### 可复用能力

- GEO 评分框架：总体 GEO Score = AI Citability 25% + Brand Authority 20% + Content E-E-A-T 20% + Technical 15% + Schema 10% + Platform Optimization 10%。
- AI 可引用性评分：用内容块维度评估回答质量、自包含程度、可读结构、统计密度、唯一性信号。
- AI crawler 检查：检测 robots.txt 对 GPTBot、ClaudeBot、PerplexityBot、OAI-SearchBot、Googlebot 等是否开放。
- llms.txt 分析与生成：把站点结构、核心页面、AI crawler 友好信息包装成机器可读文件。
- 品牌提及扫描：强调 YouTube、Reddit、Wikipedia、LinkedIn、review 平台等第三方实体信号。
- 结构化数据模板：Organization、LocalBusiness、Article/Author、Software/SaaS、Product/Ecommerce、Website SearchAction。
- 多 agent 审计编排：AI visibility、platform analysis、technical、content、schema 并行处理。
- 销售化资产：prospect JSON、pipeline status、proposal 文档、monthly comparison、白标配置、PDF 报告。

### 与市场营销/销售推进的关系

该仓库最适合做“诊断式销售”。销售人员可以先跑一个 quick audit，把目标客户站点的 GEO Score、AI crawler 被阻塞、无 llms.txt、无第三方提及、schema 不完整、内容不可引用等问题转成具体痛点，然后输出 proposal。

它把营销线索推进从“你需要 SEO 服务”升级成“你的站点在 AI 搜索里不可见，且我们能指出原因”。这比泛泛的 SEO pitch 更容易形成 urgency，因为 AI 搜索变化提供了市场叙事，评分报告提供了证据，proposal 提供了下一步商业方案。

### 对 AI 辅助销售工具的启发

- 把销售触发点产品化：例如“你的关键页面无法被 AI crawler 看到”“你缺少可被引用的 answer block”“你的竞品在 Reddit/YouTube/AI 搜索中有实体优势”。
- 每个线索不只存联系方式，还要存诊断分数、审计日期、痛点、报告链接、建议报价、下一步动作。
- 可用 “低分 = 强销售机会” 的方式做 lead scoring。比如 GEO Score < 55 自动建议生成 proposal。
- 销售工具可以输出“客户可读”的问题截图、评分表、优先级 roadmap，而不是只给 SDR 内部备注。
- 将报告、提案、月度 delta 串起来，可支持从首次触达到续约/复购的完整顾问服务。

### 风险/不足

- 部分权重和相关性判断较强依赖作者假设，并非全部来自可复现实验。比如品牌提及与 AI citation 的相关性、各平台权重，应在产品中标为“诊断假设”而非保证。
- llms.txt 仍是新兴标准，不应宣传为稳定排名因子。对 Google AI Overviews 影响尤其要谨慎。
- 品牌提及扫描容易受平台 API、登录、反爬与数据新鲜度限制。
- LLM 子 agent 评分存在非确定性，若作为销售报价依据，需加入置信区间或人工复核。
- 该仓库更偏 agency workflow，对 SaaS 自助式销售工具还需要进一步产品化 UI、权限、CRM 集成与多租户数据隔离。

## 2. AgriciDaniel/claude-seo

GitHub：<https://github.com/AgriciDaniel/claude-seo>

### 用意/目标

这是一个更完整、更传统 SEO 与 AI 搜索兼容的 Claude Code SEO 操作系统。README 中强调 25 个 sub-skills、18 个 specialist agents、技术 SEO、E-E-A-T、Schema.org、AI search/GEO、本地 SEO、电商、国际化、Google API、DataForSEO、Ahrefs、SE Ranking、Profound、Bing Webmaster、Unlighthouse 等扩展。

它的定位不是单一 GEO 服务，而是“用 agent 并行执行完整 SEO 审计，并输出可证伪、基于一手指南的建议”。与 `geo-seo-claude` 相比，它更重视 Google 官方文档、质量门、schema deprecation、Core Web Vitals、GSC/GA4/CrUX 等真实数据。

### 可复用能力

- 多层 SEO skill 架构：主 orchestrator 路由到 audit、page、technical、content、schema、sitemap、images、geo、local、maps、google、backlinks、cluster、sxo、drift、ecommerce、hreflang、plan、programmatic、competitor-pages 等。
- 行业识别：SaaS、本地服务、电商、publisher、agency，并据此调整审计重点。
- SEO Health Score：Technical 22%、Content 23%、On-page 20%、Schema 10%、Performance 10%、AI Search 10%、Images 5%。
- 可证伪建议框架：每条建议要附 first-principle observation、依赖关系、失败判定、leading indicator。
- Google API 分层集成：PageSpeed/CrUX、Search Console、Indexing API、GA4、Keyword Planner。
- 渲染与安全能力：Playwright headless renderer 处理 SPA，SSRF/DNS rebinding 测试、URL safety。
- 内容简报能力：`seo-content-brief` 包含 SERP 分析、竞品过滤、搜索意图、keyword density、meta、information gain、E-E-A-T、内部链接。
- SEO drift：为后续监控基线变化提供思路。
- 扩展数据源：DataForSEO、Firecrawl、Ahrefs、SE Ranking、Profound、Bing Webmaster、Unlighthouse。

### 与市场营销/销售推进的关系

该仓库适合做“高可信度的审计型售前支持”。它不仅能发现问题，还强调每条建议如何验证失败，这对销售推进很关键：客户常常不信“最佳实践”，但更容易接受“如果 28 天后 GSC 点击/position/CTR 没改善，我们就知道这条建议没奏效”。

它还可以帮助销售团队生产细分行业的 SEO plan、content brief、competitor comparison page、local SEO plan、ecommerce audit。这些都是销售漏斗中高价值资产：用于 discovery call、proposal、QBR、续费复盘。

### 对 AI 辅助销售工具的启发

- 把“建议”升级为“实验”：AI 销售工具给出 outreach 建议时，也应定义 leading indicator 和失败条件，比如 14 天内 positive reply rate 未提升则回滚话术。
- 对每条销售动作建立依赖图：例如先修站点 pricing 可读性，再做 agentic buyer pitch；先补 schema，再做 GEO 触达。
- 对不同业务类型用不同 playbook：SaaS 讲集成和定价页，本地商家讲 GBP/NAP/reviews，电商讲 product schema 和 Merchant Center。
- 内容简报可直接转化为销售物料简报：竞品差距、信息增益、E-E-A-T、内部链接可以对应到“客户为什么应该相信我们”的证据链。
- SEO drift 思路可迁移成 sales messaging drift：监控竞品、客户页面、市场叙事、AI citation 变化，自动提醒销售更新话术。

### 风险/不足

- 功能面很宽，安装、凭证、扩展较复杂。作为销售工具内核，需要抽象出轻量流程，避免让销售团队面对 20 多个命令。
- 对 Google 官方姿态更谨慎，和市场上“GEO 独立红利”的叙事存在张力。销售时不能同时夸大 GEO 魔法，又声称遵循 Google 指南。
- 完整数据能力依赖 API 凭证，免费/离线模式的结论会较粗糙。
- 多 agent 并行输出可能产生重复、冲突或过度建议，需要一个“销售可执行优先级压缩器”。
- SEO 工具链结果并不天然等于销售机会，需要结合 ICP、预算、组织触发信号和决策人可达性。

## 3. coreyhaines31/marketingskills

GitHub：<https://github.com/coreyhaines31/marketingskills>

### 用意/目标

该仓库是面向 AI agents 的跨平台营销技能库，适配 Claude Code、OpenAI Codex、Cursor、Windsurf 等。它不是一个单一 app，而是一套营销操作知识库和工具注册表，覆盖 SEO、AI SEO、内容策略、CRO、copywriting、cold email、email lifecycle、prospecting、RevOps、sales enablement、pricing、launch、analytics、programmatic SEO、schema、competitors、customer research 等。

它的核心设计是：`product-marketing` 是基础上下文，其他技能在执行前先读取产品定位、受众、差异化和消息框架。这让营销和销售动作不再各自 improvisation，而是共享同一套 GTM 语义。

### 可复用能力

- 产品营销上下文优先：所有技能先读取 `.agents/product-marketing.md` 或类似文件。
- AI SEO skill：解释 Google AI Overviews、ChatGPT、Perplexity、Claude、Gemini、Copilot 的来源选择差异；强调结构、权威、存在感三大支柱。
- SEO audit skill：传统技术 SEO、on-page、内容质量、国际化、schema 检测限制与工具建议。
- Content strategy：从客户问题、销售异议、支持工单、论坛、竞品、关键词数据中规划内容支柱和 topic cluster。
- Programmatic SEO：模板页、目录页、比较页、location pages、integration pages、glossary 等 12 类 playbook。
- Prospecting：SaaS、B2B、Local SMB 三条分支，强调 ICP、候选池、证据化资格判断、Hot/Warm/Cold/Skip 评分、合规。
- Sales enablement：销售 deck、one-pager、objection handling、ROI calculator、demo scripts、case study briefs、proposal、playbook、persona cards。
- RevOps：lead lifecycle、MQL/SQL、scoring、routing、pipeline stage、CRM 自动化、dashboard。
- Tools registry：GA4、GSC、Semrush、Ahrefs、DataForSEO、Apollo、Clay、ZoomInfo、HubSpot、Salesforce、Outreach、RB2B、Gong 等集成指南和 CLI 映射。

### 与市场营销/销售推进的关系

该仓库最像“AI CMO/RevOps 助手的技能底座”。它把营销从内容生产扩展到销售推进：先定义定位，再做内容策略，再做 SEO/AI SEO 获取需求，再 prospecting 找线索，再 cold-email 和 sales enablement 触达，再 RevOps 路由和度量。

对销售推进尤其有价值的是，`prospecting` 明确要求每个 Hot lead 有购买信号和 source URL；`sales-enablement` 要把价值主张转成不同 buyer 的 one-pager、deck、objection doc、demo talk track；`revops` 要把 MQL-to-SQL handoff、speed-to-lead、routing、stage hygiene 纳入系统。

### 对 AI 辅助销售工具的启发

- 应建立一个“产品营销上下文文件”作为所有销售生成动作的根上下文，避免不同 SDR/AE/agent 写出不同定位。
- 销售工具不应只输出邮件，还应按漏斗阶段输出不同资产：prospecting list、account dossier、cold email、follow-up、one-pager、ROI calculator、proposal、objection response。
- Lead scoring 应要求证据 URL 和信心等级，防止 agent 编造线索理由。
- 合规应内置在 prospecting 阶段，而不是等发送前才检查。
- 可借鉴三分支 prospecting：SaaS/B2B/Local SMB 的信号、来源、合规风险、联系渠道都不同。
- 工具注册表是好范式：AI 销售产品也应有“可用数据源和操作能力 registry”，让 agent 知道什么时候用 CRM、enrichment、GSC、Gong、email verifier、sales engagement。

### 风险/不足

- 多数 skill 是框架和知识流程，不一定包含可直接运行的完整自动化脚本。落地时需要把“建议步骤”工程化。
- 一些 AI SEO 统计和平台行为描述可能随时间变化很快，需要定期更新和来源标注。
- 工具 registry 很广，但每个集成都需要真实凭证、权限、速率限制和数据合规处理。
- skill 之间可能有重叠，例如 SEO audit、AI SEO、content strategy、programmatic SEO，需要产品层做路由和去重。
- 作为开源技能库，不负责用户具体行业的法律合规边界。销售工具产品化时需要更强的审计日志和权限控制。

## 4. ericosiu/ai-marketing-skills

GitHub：<https://github.com/ericosiu/ai-marketing-skills>

### 用意/目标

该仓库是更“可执行脚本化”的 AI marketing/sales workflow 集合。README 明确说这些不是 prompts，而是 workflows、scripts、scoring algorithms、expert panels、automation pipelines。它覆盖 Growth Engine、Sales Pipeline、Content Ops、Outbound Engine、SEO Ops、Finance Ops、Revenue Intelligence、Conversion Ops、Podcast Ops、Team Ops、Sales Playbook、Autoresearch、Deck Generator、YouTube 竞争分析、X 长文等。

相比 `marketingskills` 的跨 agent 知识库，该仓库更偏“运营自动化脚本包”：例如 RB2B visitor -> suppression -> campaign routing -> Instantly，Gong transcript -> objections/buying signals/content topics，GA4 + HubSpot -> revenue attribution，GSC/Ahrefs -> content attack brief。

### 可复用能力

- SEO Ops：`content_attack_brief.py` 结合 content fingerprint、Ahrefs、GSC、competitor gaps、decaying pages，按 Impact x Confidence 排序关键词机会，并分配 auto/semi/team 执行路径。
- GSC client：striking distance keywords、pages、trend、device split、verified properties。
- Trend Scout：Google Trends RSS、HN、Reddit、X/Brave、YouTube outlier 等趋势来源。
- Sales Pipeline：RB2B webhook ingest、suppression pipeline、Instantly router、deal resurrector、trigger prospector、ICP learner。
- RB2B -> Instantly router：intent scoring、agency detection、seniority rank、source site detection、campaign routing、Instantly enrollment。
- Lead Dossier：account research、cascade enrichment、full lead pipeline、real-time lead enrichment。
- Outbound Engine：Instantly audit、ICP definition、expert panel recursive scoring、sequence copy、infrastructure capacity math、人审后再写入。
- Content Ops：expert panel、content quality gate、editorial brain、quote miner、content transform、scoring rubrics、learned rejection patterns。
- Revenue Intelligence：Gong insight extraction、content-to-revenue attribution、client report generator、anomaly flags。
- Sales Playbook：value-based pricing pre-call briefing、tiered packaging、call analyzer、pricing pattern library。
- 安全与遥测：PII sanitizer、pre-commit hook、opt-in telemetry、local analytics。

### 与市场营销/销售推进的关系

该仓库直接覆盖销售推进的多个环节：

- 匿名访问者识别后进入 outbound：识别访问 pricing/demo/case-study 等高意图页面的人，压制不该触达的对象，再路由到对应 campaign。
- 旧 deal 复活：从 HubSpot closed-lost 或沉睡机会中找复活信号。
- 触发式 prospecting：招聘、融资、agency search 等外部信号触发销售动作。
- ICP 自学习：从 approve/reject 或 win/loss 反馈中修正目标客户定义。
- 通话洞察回流内容：Gong 中的 objections、buying signals、competitor mentions 直接生成内容主题和 follow-up。
- 收入归因：用 GA4/HubSpot 把内容与 pipeline/revenue 连接起来。

这已经非常接近 AI 辅助销售工具的后端工作流原型。

### 对 AI 辅助销售工具的启发

- 触达前必须有 suppression pipeline：查客户、退订、已在 campaign、已在 CRM、同公司更高级联系人等，避免重复骚扰和伤害品牌。
- Intent score 可由访问页面决定：pricing/contact/demo/case-study 比 blog/podcast 权重大很多。
- Route to campaign 不应一刀切：agency、general、不同来源站点、不同角色、不同意图应路由到不同 sequence。
- 生成销售话术前先跑 account dossier 和 ICP fit，不要只靠邮箱和 title。
- 销售工具的“AI 写作”要有专家面板评分和递归改进机制，目标不是看起来像 AI 写的漂亮话，而是达到可发送质量门。
- 人工审批门很重要。`outbound-engine` 明确不自动推送到 Instantly，先生成文档供人审。这是 B2B 销售自动化的安全设计。
- 收入读回是核心壁垒。没有 HubSpot/Gong/GA4/outbound readback，AI 销售工具只能停留在生成器；有读回，才能自学习。

### 风险/不足

- 依赖大量第三方 API：HubSpot、Instantly、RB2B、Gong、Ahrefs、GA4、Brave、email validation 等，真实部署成本和权限复杂度高。
- 部分脚本是业务特定配置，默认 keyword/topic、agency detection、campaign routing 都需要重写，否则误判严重。
- 自动把访问者加入 outbound campaign 存在合规和品牌风险，需要明确 opt-out、合法利益、地区规则、数据来源授权。
- cold outbound 的 deliverability 风险高，任何错误的 lead validation、过度个性化或高频发送都会损害域名信誉。
- 使用 subprocess/curl 等方式调用 API，作为产品内核需要重构为可审计、可重试、可观测的服务层。
- Opt-in telemetry 虽然隐私友好，但在企业客户环境中仍需清晰禁用和数据边界说明。

## 5. oaker-io/wewrite

GitHub：<https://github.com/oaker-io/wewrite>

### 用意/目标

`wewrite` 是中文微信公众号文章全流程 AI skill，覆盖热点抓取、选题评分、框架选择、素材采集、内容增强、写作、SEO 优化、AI 配图、微信排版、发布草稿、效果复盘、范文风格库和学习用户修改。它兼容 Claude Code、OpenClaw，并通过生成 Codex prompt 兼容 OpenAI Codex CLI。

它关注的不是传统网站 SEO，而是微信生态内的内容增长：搜一搜 SEO、标题打开率、摘要、标签、完读率、公众号合规、排版兼容、AIGC/低创风险、微信草稿箱发布。

### 可复用能力

- 中文内容生产管线：8 步固定流程，从环境配置到收尾历史写入。
- 热点抓取：微博、头条、百度热搜等来源。
- 关键词评分：`seo_keywords.py` 用百度和 360 搜索建议作为中文搜索需求 proxy。
- 选题评分：10 个选题，含热点选题和常青选题，结合历史去重与 SEO。
- 写作框架：痛点、故事、清单、对比、热点解读、纯观点、复盘等。
- 内容增强：角度发现、密度强化、细节锚定、真实体感，且按框架匹配。
- 写作 persona：midnight-friend、warm-editor、industry-observer、sharp-journalist、cold-analyst 等。
- 范文风格库：从用户已发布文章提取 SICO 式 few-shot 风格指纹。
- 学习飞轮：学习用户改稿，形成 playbook 与 history。
- SEO 规则：标题 20-28 中文字、摘要 120 UTF-8 字节、关键词前 200 字出现、3-5 次自然出现、H2 加权、5 个标签。
- 质量验证：humanness_score、禁用词、句长方差、真实素材、每个 H2 的具体细节。
- 微信排版引擎：Markdown 到微信兼容 HTML，修复外链、CJK 空格、列表、暗黑模式、内联 CSS、容器语法。
- 公众号合规：禁止诱导分享/关注、夸大收益、标题党、搬运、低价值 AIGC。

### 与市场营销/销售推进的关系

`wewrite` 可复用到“内容驱动销售”的中文市场场景，尤其是个人 IP、咨询服务、AI 工具、B2B 服务、创始人号、销售型公众号。它解决的是从选题到发布的效率问题，更重要的是把“个人经验、真实素材、风格一致性、平台合规、复盘学习”纳入流程。

对销售推进来说，它可以支持：

- 生成面向目标行业的教育型内容，培养信任。
- 根据销售异议写公众号文章，作为 SDR/AE 跟进时的“非硬广资料”。
- 为客户案例、复盘、行业观点生成适合微信生态传播的版本。
- 根据阅读、分享、完读数据优化后续选题和销售叙事。

### 对 AI 辅助销售工具的启发

- 中文销售内容不能简单翻译英文 cold email 框架。需要适配微信、公众号、私域、长文、案例、观点、合规表达。
- 对 B2B 内容，应该强制加入“编辑锚点”：让销售/创始人补充真实经历、客户细节、行业判断，降低低价值 AIGC 风险。
- 风格库和学习用户修改非常适合销售工具：每个 AE/创始人都可以有自己的语气模型，而不是统一模板。
- 标题/摘要/标签/完读率优化可迁移到销售资料：例如 LinkedIn post、邮件 subject、one-pager headline、proposal executive summary 都需要相同的“打开率 + 信任感”优化。
- 内容历史和表现数据可反哺销售话术：哪个 framework、persona、topic、closing_type 带来更高阅读和咨询，应影响下一轮 outreach。

### 风险/不足

- README 和部分文件在当前终端显示存在编码乱码，但中文结构和文件内容仍可辨识；产品化时需要确保 UTF-8 端到端。
- `seo_keywords.py` 用百度/360 suggestions 作为 popularity proxy，不能等同真实搜索量、竞争度或转化价值。
- 微信规则变化快，合规和推荐机制需要持续更新。
- 自动写作虽然加入真实素材约束，但如果 WebSearch 不可用或用户不补充真实经验，仍可能生成泛化内容。
- 平台发布需要公众号 appid/secret，企业部署时要处理凭证安全、权限、草稿误发风险。
- 公众号生态与 SaaS/B2B outbound 的直接连接不如 CRM/Email 明确，需要额外设计线索捕获和归因机制。

## 跨仓库共性观察

### 1. 从“内容生成”转向“证据生成”

五个仓库都不满足于简单生成文案。`geo-seo-claude` 和 `claude-seo` 要抓页面、schema、robots、GSC、CrUX、品牌提及；`marketingskills` 要 source URL 和资格证据；`ai-marketing-skills` 要 GSC/Ahrefs/Gong/HubSpot/GA4；`wewrite` 要真实素材、来源、个人经验。AI 销售工具也应把“证据”放在第一位：为什么找这个客户，为什么现在，为什么这个痛点是真的。

### 2. 评分系统是销售自动化的核心接口

可复用评分包括：

- GEO Score：衡量站点对 AI 引擎的可见性。
- SEO Health Score：衡量整体搜索健康。
- Impact x Confidence：衡量关键词/内容机会。
- Intent Score：衡量访问者购买意图。
- Hot/Warm/Cold/Skip：衡量 prospecting 优先级。
- Expert Panel Score：衡量内容/话术可发送质量。
- Value-based Pricing Score：衡量销售通话是否围绕价值。
- Humanness/low-quality risk score：衡量内容是否像低价值 AIGC。

这些分数应统一进入 AI 销售工具的队列和看板。

### 3. AI 搜索与销售正在合流

GEO/AI SEO 不只是流量问题，也影响销售：未来买家可能让 ChatGPT/Perplexity/AI agent 比较供应商。若定价、案例、产品能力、schema、第三方评价、Reddit/G2/YouTube 内容不可被 AI 读取，销售会在买家接触前就输掉 shortlist。

因此 AI 辅助销售工具应给客户或自己提供“agent-readable selling surface”：

- `/pricing.md`
- `/features.md`
- `/comparison/[competitor].md`
- `/case-studies.md`
- Organization/Product/SoftwareApplication schema
- 清晰的 FAQ、对比表、用例页、行业页
- G2/Trustpilot/YouTube/Reddit/LinkedIn/Wikipedia 等第三方实体信号

### 4. 人工审批门不是阻碍，而是商业安全

`ai-marketing-skills` 的 outbound engine 明确先生成文档，不自动写入 Instantly；`wewrite` 通过编辑锚点要求用户加入真实话；`claude-seo` 强调可证伪与质量门。AI 销售工具也应默认 human-in-the-loop：自动研究和起草，关键外发、CRM 写入、campaign enrollment、报价承诺必须审批。

### 5. 数据读回决定长期壁垒

最有价值的设计是 `ai-marketing-skills` 的 closed-loop analytics 和 revenue intelligence。AI 销售工具若能把每条话术、每个触发信号、每种内容资产与回复率、会议率、SQL、pipeline、closed-won 连接起来，就能形成自学习系统。否则只是一个文案助手。

## 对 AI 辅助销售工具的功能建议

### MVP 优先级

第一阶段建议做 5 个能力：

1. Account Signal Dossier：输入域名，输出站点/SEO/GEO/内容/竞品/技术/招聘/新闻/CRM 信号摘要。
2. Opportunity Score：融合 ICP fit、intent、GEO/SEO gap、预算代理信号、联系人可达性，输出 Hot/Warm/Cold/Skip。
3. Evidence-based Outreach：邮件/LinkedIn/电话开场必须引用 1-2 个真实证据，附 source URL。
4. Sales Asset Generator：为 Hot account 生成 one-pager、objection handling、ROI hypothesis、proposal outline。
5. Readback Loop：把 outbound 平台、CRM、Gong/会议记录、GA4/GSC 的结果回写到 playbook，判断哪些触发信号和话术有效。

### 数据模型建议

每个 account 至少包含：

- domain
- company_name
- industry
- ICP fit fields
- contacts
- public evidence URLs
- website diagnostics
- SEO/GEO score
- AI visibility notes
- intent events
- competitor mentions
- current tools/tech stack
- pain hypotheses
- recommended offer
- generated assets
- outreach status
- CRM status
- outcome metrics
- last verified date
- compliance lineage

### 销售动作生成原则

- 不允许无证据个性化。每条个性化必须来自可追溯来源。
- 不允许夸大 GEO/SEO 或 AI visibility 的确定性。使用“可能”“诊断显示”“建议验证”。
- 不允许自动外发高风险内容。尤其是 cold email、LinkedIn、报价、法律/医疗/金融行业。
- 默认给销售人员一个“为什么这个线索现在值得跟”的摘要，而不是只生成长文。
- 默认提供下一步动作：run audit、send email、book call、create proposal、route to nurture、skip。

## 主要风险清单

1. 数据新鲜度风险：SEO、AI 搜索、平台规则、API 能力变化非常快，需要版本化知识库。
2. 伪精确风险：GEO Score、AI visibility、keyword opportunity 容易看起来像精确科学，但很多是启发式评分。
3. 合规风险：visitor identification、cold outbound、email enrichment、LinkedIn/Google Maps 数据使用都有地区法律和 ToS 风险。
4. 品牌风险：过度自动化触达会产生重复、冒犯、错误个性化、错误称谓、错发竞品信息。
5. 凭证风险：GSC、GA4、HubSpot、Gong、Instantly、Ahrefs 等凭证权限高，需要最小权限、加密、审计。
6. 幻觉风险：LLM 生成素材、销售理由、竞品比较时必须有来源约束和人工复核。
7. 归因风险：内容、SEO、outbound、销售通话对 revenue 的贡献很难单因子归因，需要保留 caveats。
8. 平台依赖风险：Google、微信、Instantly、HubSpot、Gong、Ahrefs、DataForSEO 等 API 或政策变化会影响能力。
9. 本地脚本产品化风险：多个仓库脚本适合 demo/agency 内部使用，但正式产品需要队列、重试、日志、权限、监控、多租户隔离。
10. 中英文场景差异：英文 B2B outbound 和中文私域/公众号/微信生态的内容与合规差异很大，不应共用一套模板。

## 建议的最终产品定位

不要定位成“AI 销售邮件生成器”。更有潜力的定位是：

“AI Revenue Research & Sales Activation Copilot”：自动发现销售机会，诊断账户和市场信号，生成证据驱动的销售动作，并通过 CRM/通话/营销数据持续学习。

一句中文表达：

“让销售在联系客户前，就知道客户哪里有问题、为什么现在该聊、该用什么证据开场、后续哪套内容能推进成交，并且每次触达结果都会反哺下一次判断。”

## 仓库对比速览

| 仓库 | 最强能力 | 最适合迁移到销售工具的部分 | 主要不足 |
|---|---|---|---|
| zubair-trabzada/geo-seo-claude | GEO 审计与 agency 销售闭环 | 站点 GEO 诊断、prospect pipeline、proposal | 权重和 GEO 叙事需谨慎验证 |
| AgriciDaniel/claude-seo | 全面 SEO 操作系统与可证伪建议 | 多 agent 审计、Google/GSC/CrUX 数据、content brief、drift | 功能复杂，需简化为销售可用流程 |
| coreyhaines31/marketingskills | 跨 agent 营销/销售技能库 | product marketing context、prospecting、sales enablement、RevOps | 多为知识流程，脚本化不足 |
| ericosiu/ai-marketing-skills | 可执行增长/销售自动化脚本 | RB2B routing、lead dossier、outbound expert panel、Gong/revenue attribution | API 依赖和合规风险高 |
| oaker-io/wewrite | 中文公众号内容生产闭环 | 中文内容增长、风格学习、编辑锚点、微信 SEO/合规 | 微信生态专用，搜索量 proxy 较粗糙 |

## 最值得优先实现的 10 个小功能

1. 输入域名生成 SEO/GEO sales trigger 摘要。
2. robots.txt + AI crawler access 检查，并转成销售开场。
3. pricing/demo/case-study 页面可读性和 agent-readable 检查。
4. 竞品 comparison gap：客户没有而竞品有的对比页、案例页、schema、G2/YouTube/Reddit 信号。
5. GSC striking-distance + content decay 自动生成“内容刷新销售机会”。
6. RB2B/站内访问 intent score + suppression + campaign routing。
7. Gong/会议纪要提取 objections，并自动生成 follow-up 内容。
8. Expert panel 对外发邮件和 one-pager 打分，低于阈值不允许发送。
9. Product marketing context 文件作为所有销售内容的根上下文。
10. Readback dashboard：每种触发信号和话术对应回复率、会议率、SQL、pipeline。

## 给其他研究角色的协作提示

- 如果角色 B 做产品/系统架构，可重点接上“7 层模块”和“数据模型建议”。
- 如果角色 C 做销售策略，可重点接上“诊断式销售”“value-based pricing”“objection -> content”。
- 如果角色 D 做工程实现，可重点评估 API 凭证、队列、日志、重试、权限、多租户隔离。
- 如果角色 E 做合规/风险，可重点审查 visitor identification、email enrichment、cold outbound、平台 ToS、AI 生成事实校验。

