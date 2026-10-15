# fal-h3max

**A 5-second 768p clip in under 3 seconds.**

Notes on **MiniMax H3** and **H3 Max**, the video models behind [h3max.pro](https://h3max.pro): what they are, how they differ, and the numbers behind them.

The performance figures below come from MiniMax's H3 announcement and fal's H3 Max launch. They are **the vendors' published claims, not independent measurements**.

---

## The base model: MiniMax H3

H3 is a **general-purpose multimodal generation model**. Text, images, video and audio go in as one unified context, and it can generate any of them.

For video, that means **up to 15 seconds at 2K with native stereo sound**. The audio is generated together with the picture, not dubbed on afterwards. Voice, sound effects and music are modelled jointly rather than by separate expert models.

It also covers image-to-image, image-to-video, audio-to-audio, multi-shot sequences, motion transfer between videos, and text and brand rendering that holds up in the output.

### How it is built

| Piece | What it does |
|---|---|
| **H3-Contextual Omni Representation** | Uses language as the bridge between tasks. Source material runs through ~100K tokens of inference, distilled to ~4K on average. |
| **H3-VAE tokenizer** | Rebuilt for reconstruction quality, with a **4× gain in effective sequence length**. |
| **H3-Omni Transformer** | Separates understanding and generation workloads for **~30% more throughput**. |
| **In-context Regeneration** | Regenerates its own low-resolution output up to 2K while keeping the original context. |

## The fast variant: H3 Max

H3 Max is H3 **post-trained by fal on new data**, tuned for prompt adherence and aesthetics, with much of the post-training compute spent on verifiable RL tasks. It was designed around fal's in-house diffusion inference engine, which is where the speed comes from.

The priority was **quality first, then as much speed as possible without losing it.**

### H3 Max vs H3

| | H3 Max | H3 |
|---|---|---|
| Built for | Speed and prompt adherence at 768p | Range |
| Resolution | 480p, 768p | Up to 2K |
| Reference-to-video, video editing | — | ✅ |
| Native audio | — | ✅ |

H3 Max trades resolution and editing modes for speed at 768p. For 2K or reference-to-video, use H3.

## Speed

- **5-second 768p clip in under 3 seconds** (~2.5 s of inference)
- **15-second clip in about 15 seconds**
- **~35× the throughput** of the official H3 endpoint
- **~15× faster** than models of comparable quality, on average

A render finishes faster than you can re-read the prompt. It feels like a tool you use live, not a job you check on later.

## Benchmarks

H3 Max ranks first on both human-preference Elo leaderboards:

| Leaderboard | Elo | Rank |
|---|---|---|
| **Design Arena** | 1,341 | 1st |
| **Artificial Analysis** | 1,201 | 1st (95% CI ±11, 2,177 samples) |

## Specs

| | |
|---|---|
| **Durations** | 5–15 seconds |
| **Resolutions** | 480p, 768p (default) |
| **16:9 output** | 1344×768 at 24 fps |
| **Aspect ratios** (text-to-video) | 21:9, 16:9, 4:3, 1:1, 3:4, 9:16 |
| **Modes** | Text-to-video, image-to-video (optional end frame) |

## Try it

[**h3max.pro**](https://h3max.pro) runs both H3 and H3 Max with every parameter exposed. No API key, no install. Credits are charged per second of output, failed renders are fully refunded, and new accounts get free credits.

---

## 中文

**5 秒 768p 视频，3 秒内出片。**

这里整理了 [h3max.pro](https://h3max.pro) 背后的两个视频模型：**MiniMax H3** 和 **H3 Max**。性能数据来自 MiniMax 的 H3 发布说明和 fal 的 H3 Max 发布信息，**均为官方公布数字，并非独立实测**。

### H3：底座模型

H3 是一个**通用多模态生成模型**：文本、图像、视频、音频作为同一份上下文输入，也可以生成其中任意一种。

视频方面支持**最长 15 秒、2K 分辨率、原生立体声**。声音与画面一起生成，而不是后期配音；人声、音效和音乐统一建模，不再依赖各自独立的专家模型。

此外还支持图生图、图生视频、音频生成、多镜头序列、视频间动作迁移，以及稳定的文字与品牌元素渲染。

架构由四部分组成：**H3-Contextual Omni Representation**（以语言为桥梁统一各类任务，素材经约 10 万 token 推理后平均压缩到约 4K token）、**H3-VAE 分词器**（重新设计，有效序列长度提升 **4 倍**）、**H3-Omni Transformer**（拆分理解与生成负载，吞吐提升约 **30%**）、**In-context Regeneration**（在保留原始上下文的前提下，把低分辨率结果重新生成到 2K）。

### H3 Max：更快的版本

H3 Max 是 fal 在 H3 基础上**用新数据做了后训练**的版本，重点优化提示词遵循度和画面美感，并在可验证的 RL 任务上投入了大量算力。它围绕 fal 自研的扩散模型推理引擎设计，这也是速度的来源。原则是：**先保质量，再在不损失质量的前提下把速度推到极限。**

取舍很明确：H3 Max 放弃 2K、参考视频生成和视频编辑，换来 768p 下的速度和遵循度。需要 2K 或参考视频生成时，请用 H3。

### 速度

- **5 秒 768p 片段 3 秒内出片**（推理约 **2.5 秒**）
- **15 秒片段约 15 秒**
- 吞吐约为 H3 官方端点的 **35 倍**
- 平均比同等质量模型**快 15 倍**

出片比你重读一遍提示词还快，用起来是实时工具，而不是提交后再回来看的任务。

### 榜单

H3 Max 在两个人类偏好 Elo 榜上均排名第一：**Design Arena** Elo **1,341**；**Artificial Analysis** Elo **1,201**（95% 置信区间 ±11，2,177 个样本）。

### 规格

时长 5–15 秒；分辨率 480p / 768p（默认 768p）；16:9 输出 1344×768 @ 24fps；文生视频支持 21:9 / 16:9 / 4:3 / 1:1 / 3:4 / 9:16；支持文生视频和图生视频（可选结束帧）。

### 立即体验

[**h3max.pro**](https://h3max.pro) 同时提供 H3 和 H3 Max，所有参数均可调，无需 API key、无需安装。按输出秒数计费，生成失败全额退还积分，新用户注册即送积分。
