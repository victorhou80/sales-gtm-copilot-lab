# 云 GPU 与模型 API 选择

## 第一原则

MVP 阶段不要先租常驻 GPU。

推荐：

```text
先用已经配好模型和 GPU 的 API。
跑出 50-300 条真实样片和用户订单后，再决定哪些流程值得自建。
```

## 阶段选择

| 阶段 | 方案 | 目标 |
|---|---|---|
| MVP | RunPod Public Endpoints + fal.ai + GPT-5.5 + TTS | 最快验证效果和付费 |
| Beta | RunPod Serverless / Modal 自建 worker | 降低稳定高频任务成本 |
| 成熟期 | 常驻 L40S / 4090 + serverless 峰值 | 控成本、保速度 |

## 模型 API

### RunPod Public Endpoints

适合：

- WAN 2.6 I2V。
- WAN 2.6 T2V。
- InfiniteTalk。
- 快速接入，不管底层 GPU。

优点：

- 已配好模型。
- 不用处理 CUDA、驱动、权重、环境。
- 适合 MVP。

缺点：

- 单价通常比自建高。
- 受 endpoint 可用性和排队影响。
- 自定义能力有限。

### fal.ai

适合：

- Seedance。
- 高级视频模型。
- GPT Image 2 等图像模型。
- 快速比较多个模型。

优点：

- 像模型超市。
- 每个模型通常有 playground、schema、价格和代码示例。
- 适合快速试错。

缺点：

- 高级视频模型成本高。
- 价格和 endpoint 变化较快。
- 境外 API 合规和财税凭证要注意。

## 云 GPU 平台

### RunPod

适合：

- ComfyUI。
- WAN / RIFE / Real-ESRGAN 工作流。
- Serverless worker。
- 临时 Pod 调试。

参考价格量级：

| GPU | 价格量级 |
|---|---:|
| L4 24GB | 约 $0.39/小时 |
| RTX 4090 24GB | 约 $0.69/小时 |
| L40S 48GB | 约 $0.86/小时 |
| A100 80GB | 约 $1.39/小时 |
| H100 | 约 $2.89/小时 |

### Modal

适合：

- Python serverless GPU。
- 按秒计费。
- 自建可控 worker。

特点：

- 工程体验好。
- 不用不花钱。
- 适合任务不稳定的早期产品。

### Vast.ai

适合：

- 低成本测试。
- 批量非敏感任务。
- 研发试验。

注意：

- 机器来源和稳定性差异大。
- 数据安全要谨慎。
- 不建议一开始承载敏感客户素材。

### 国内云和国内 GPU 租赁

可选：

- 阿里云 GPU。
- 腾讯云 GPU。
- 火山引擎 GPU。
- AutoDL。
- 矩池云。
- 趋境云。

适合：

- 国内合规。
- 需要发票。
- 面向中国大陆商家。
- 备案和支付更顺。

缺点：

- 常见价格比海外弹性平台贵。
- 模型镜像和工作流可能要自己处理。

## 何时租常驻 GPU

判断规则：

```text
每天 GPU 实际使用 < 4 小时：
继续用 API / serverless。

每天 GPU 实际使用 4-10 小时：
考虑 RunPod Serverless 或临时 Pod。

每天 GPU 实际使用 > 10 小时：
考虑常驻 4090 / L40S。

每天接近 24 小时都有任务：
常驻 L40S + serverless 峰值扩容。
```

## 推荐采购顺序

第一批：

```text
RunPod WAN 2.6
RunPod InfiniteTalk
fal Seedance
OpenAI GPT-5.5
TTS
Cloudflare R2 / OSS / COS
FFmpeg / Remotion CPU worker
```

第二批：

```text
把最常用、最稳定、最贵的环节迁到 RunPod Serverless / Modal。
```

第三批：

```text
常驻 L40S / 4090。
专门跑数字人、超分、插帧和稳定工作流。
```

## 第一笔预算建议

不要一上来月租 GPU。

建议：

| 项目 | 预算 |
|---|---:|
| RunPod / fal 模型 API 测试额度 | ¥1000-3000 |
| GPT-5.5 API | ¥300-1000 |
| TTS 测试 | ¥200-1000 |
| 存储 / 后端 / 域名 | ¥300-1000 |
| 失败重抽预留 | ¥1000-2000 |

总计：

```text
¥3000-7000 可以做出第一批 MVP 样片和内测。
```

