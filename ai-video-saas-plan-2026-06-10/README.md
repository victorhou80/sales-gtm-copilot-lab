# AI 视频 SaaS 落地方案资料包

生成日期：2026-06-10  
目标：把今天关于「小店主 / 电商 / 小博主 AI 视频生成产品」的讨论整理成可执行资料包。

## 核心结论

这个项目应该做成 **手机端入口 + 云端生成 + 自助 SaaS**，而不是客户本地 GPU 工具，也不是代运营服务。

推荐主架构：

```text
手机端 H5 / 小程序
  -> 上传商品图、店铺图、短视频素材、录音
  -> 选择模板、确认脚本、提交生成

云端后端
  -> GPT-5.5 生成脚本、分镜、标题、封面文案、合规检查
  -> TTS 生成配音
  -> InfiniteTalk / 数字人模型生成口播片段
  -> WAN / Seedance 生成高级动态镜头
  -> FFmpeg / Remotion 合成
  -> 超分到 1080p
  -> 插帧 / 转码到 30fps
  -> 返回下载和发布辅助文案
```

商业上最重要的约束：

```text
轻视频可以大量给。
数字人口播必须限分钟。
WAN / Seedance 高级镜头必须按秒或点数扣费。
不能卖「无限高级 AI 视频生成」。
```

## 推荐路线

第一阶段不要租常驻云 GPU，不要自研大视频模型。

先使用：

- RunPod WAN 2.6 I2V / T2V：普通高级视频镜头。
- RunPod InfiniteTalk：数字人口播 MVP。
- GPT-5.5：脚本、分镜、提示词、标题、封面文案、合规检查。
- TTS：中文配音。
- FFmpeg / Remotion：字幕、商品图、转场、模板合成。
- RIFE / Real-ESRGAN / 其他工具：1080p 超分和 30fps 后处理。
- fal.ai Seedance：高级镜头加购，不作为普通套餐主成本。

## 为什么不是纯视频生成

1 分钟或 5 分钟成片不应该理解为「模型一次生成 1 分钟 / 5 分钟视频」。

合理结构是：

```text
成片 = 脚本 + 配音 + 字幕 + 商品素材 + 店铺素材 + 数字人口播 + 少量 AI 高级镜头 + 后期包装
```

这样用户看到的是完整商业视频，而你的成本不会被全片 AI 视频生成拖死。

## 资料包文件

- [01-product-positioning.md](01-product-positioning.md)：产品定位、目标用户、视频类型。
- [02-technical-architecture.md](02-technical-architecture.md)：云端架构、手机端入口、任务队列、模型分层。
- [03-model-strategy.md](03-model-strategy.md)：WAN、InfiniteTalk、Seedance、GPT Image 2、JoyAI-Echo 的定位。
- [04-cost-and-profit-model.md](04-cost-and-profit-model.md)：成本、收益、套餐、净利润模型。
- [05-cloud-gpu-and-api-vendors.md](05-cloud-gpu-and-api-vendors.md)：云 GPU / 模型 API 选择。
- [06-compliance-tax-risk.md](06-compliance-tax-risk.md)：合规、税务、AI 标识、肖像声音授权、广告法风险。
- [07-marketing-and-self-media.md](07-marketing-and-self-media.md)：自媒体推流、试做包、冷启动。
- [08-mvp-roadmap.md](08-mvp-roadmap.md)：30/60/90 天执行路线。
- [09-open-questions.md](09-open-questions.md)：上线前还要验证的问题。
- [data/cost_model.csv](data/cost_model.csv)：成本收益测算表。
- [data/provider_price_reference.csv](data/provider_price_reference.csv)：供应商价格参考。

## 一句话判断

这个项目可以做，但要按 SaaS 和生产流水线做：

```text
低成本轻视频撑订阅收入
数字人口播限额
高级 AI 镜头点数化
手机端负责采集和提交
云端负责生成和后处理
自媒体样片负责低成本获客
合规和税务从第一版就纳入成本
```

