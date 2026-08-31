# fal-h3max

**A 5-second 768p clip in under 3 seconds.**

Notes on **MiniMax H3** and **H3 Max**, the video models behind [h3max.pro](https://h3max.pro) — what they are, what fal changed, and the numbers each party published.

Everything below is sourced from [MiniMax's H3 announcement](https://www.minimax.io/blog/minimax-h3) and [fal's H3 Max page](https://fal.ai/minimax-h3-max). The performance figures are **their published claims, not independent measurements**.

---

## The base model: MiniMax H3

H3 is not a video model with extras bolted on. MiniMax describes it as a **general-purpose multimodal generation model** that takes text, images, video and audio as one unified context and generates across the same set.

For video that means **up to 15 seconds at 2K, with native stereo sound** — the audio is generated jointly with the picture rather than dubbed on afterwards. Voice, sound effects and music are modelled together instead of by separate expert models, which is the part MiniMax argues was holding the previous generation back.

It also does image-to-image, image-to-video, audio-to-audio, audio-video-to-audio-video, multi-shot sequences, motion transfer between videos, and text and brand rendering that survives the generation.

### How it is built

| Piece | What it does |
|---|---|
| **H3-Contextual Omni Representation** | Language as the bridge that unifies otherwise separate tasks. Source material runs through ~100K tokens of inference, distilled to ~4K on average. |
| **H3-VAE tokenizer** | Redesigned from scratch for reconstruction quality — a **4× gain in effective sequence length**. |
| **H3-Omni Transformer** | Splits the understanding and generation workloads apart, for **~30% more throughput**. |
| **In-context Regeneration** | The base model regenerates its own low-resolution output up to 2K while keeping the original multimodal context intact. |

MiniMax puts H3's cost at **under a third of mainstream models per second at 2K**, and **under half the price of mainstream 720p at 768p**. They also say model weights are planned for open release "in the coming days, subject to applicable laws and regulations."

## What fal did: H3 Max

H3 Max is not a hosting arrangement. fal **post-trained the base model on significant new data**, tuned for prompt adherence and aesthetics, and spent "a huge portion of our post-training compute on verifiable RL tasks."

The part that explains the speed is architectural: fal designed **H3 Max around their own in-house inference engine**, which they have spent four years optimising for diffusion models. The model and the thing that runs it were shaped together.

Their stated order of priorities: **quality first, then push speed as far as it goes without giving any of it back.**

### The trade

| | H3 Max | H3 |
|---|---|---|
| Built for | Speed and prompt adherence at 768p | Range |
| Resolution | 480p, 768p | 2K |
| Reference-to-video, video editing | — | ✅ |
| Native audio | — | ✅ |

H3 Max gives up resolution and the editing modes to be fast at 768p. If you need 2K or reference-to-video, that is stock H3's job.

## Speed

fal's published figures for H3 Max:

- **A 5-second 768p clip renders in under 3 seconds** — roughly **2.5 seconds** of that is inference
- **A 15-second clip takes around 15 seconds**
- **~35× the throughput** of the official MiniMax H3 endpoint
- **~15× faster** than models of comparable quality, on average

The second number is the one that changes how the thing feels to use: a render finishes faster than it takes to read the prompt back. That is the difference between a tool you sit in front of and a job you check on later.

## Benchmarks

Both are human-preference Elo leaderboards, and H3 Max sits first on both:

| Leaderboard | Elo | Detail |
|---|---|---|
| **Design Arena** | 1,341 | 1st |
| **Artificial Analysis** | 1,201 | 1st, 95% CI ±11 over 2,177 samples |

## Specs

| | |
|---|---|
| **Durations** | 5–15 seconds |
| **Resolutions** | 480p, 768p (default) |
| **16:9 output** | 1344×768 at 24 fps |
| **Aspect ratios** (text-to-video) | 21:9, 16:9, 4:3, 1:1, 3:4, 9:16 |
| **Endpoints** | text-to-video, image-to-video (optional end frame) |

Reference-to-video was listed as arriving later in the same week as launch.

## Pricing

**$0.08 per second at 768p** — $4.80 a minute, so a 15-second clip is **$1.20**.

fal launched it at **50% off for the first 14 days** ($0.04/second, $0.60 for 15 seconds). Check the [model page](https://fal.ai/minimax-h3-max) for what is current before quoting these.

## Try it

[**h3max.pro**](https://h3max.pro) runs both models with every parameter the endpoints expose — no API key, no install. Credits are charged per second of output, a failed render is refunded in full, and new accounts start with free credits.

---

## 中文

**5 秒 768p 视频，3 秒内出片。**

这是 [h3max.pro](https://h3max.pro) 背后两个模型的资料整理：**MiniMax H3** 和 **H3 Max**。以下内容全部来自 [MiniMax 的 H3 发布博客](https://www.minimax.io/blog/minimax-h3)和 [fal 的 H3 Max 页面](https://fal.ai/minimax-h3-max)，**性能数字是他们各自公布的说法，不是独立实测**。

### H3：底座模型

H3 不是一个「视频模型加了点别的」，MiniMax 把它定位成**通用多模态生成模型**——文本、图像、视频、音频作为同一份上下文进去，也从同一套里生成出来。

落到视频上就是**最长 15 秒、2K 分辨率、原生立体声**——声音和画面是一起生成的，不是事后配上去的。人声、音效、音乐被放在一起建模，而不是各用一个专家模型，MiniMax 认为这正是上一代的瓶颈所在。

架构上有四块：**H3-Contextual Omni Representation**（用语言当桥梁统一各类任务，素材经约 10 万 token 推理、平均压到约 4K token）、**H3-VAE 分词器**（重做，有效序列长度提升 **4 倍**）、**H3-Omni Transformer**（把理解和生成两类负载拆开，吞吐提升约 **30%**）、**In-context Regeneration**（把自己的低分辨率结果重新生成到 2K，同时保留原始多模态上下文）。

价格方面 MiniMax 称：2K 每秒成本**不到主流模型的三分之一**，768p **不到主流 720p 的一半**。模型权重计划「在未来几天内」开放。

### H3 Max：fal 做了什么

不是简单托管。fal **用大量新数据对底座做了后训练**，专门调提示词遵循度和画面美感，并把「很大一部分后训练算力花在了可验证的 RL 任务上」。

速度的真正来源是架构层面的：fal **围绕自家推理引擎来设计 H3 Max**——这套引擎他们针对扩散模型优化了四年。模型和跑它的东西是一起长出来的。他们自述的优先级是：**先保质量，再把速度推到不损失质量为止。**

代价是取舍：H3 Max 放弃了 2K、参考视频和视频编辑，换 768p 下的速度和遵循度。要 2K 或参考视频生成，那是原版 H3 的活。

### 速度（fal 公布数字）

- **5 秒 768p 片段 3 秒内出片**，其中推理约 **2.5 秒**
- **15 秒片段约 15 秒**
- 吞吐约为 MiniMax 官方 H3 端点的 **35 倍**
- 相较同等质量的模型平均**快 15 倍**

第二个数字才是真正改变使用体感的：出片比你把提示词读一遍还快。这是「坐在那儿用的工具」和「提交完过会儿回来看」的区别。

### 榜单

两个都是人类偏好 Elo 榜，H3 Max 都排第一：**Design Arena** Elo **1,341**；**Artificial Analysis** Elo **1,201**（95% 置信区间 ±11，2,177 个样本）。

### 规格与价格

时长 5–15 秒；分辨率 480p / 768p（默认 768p）；16:9 输出 1344×768 @ 24fps；文生视频支持 21:9 / 16:9 / 4:3 / 1:1 / 3:4 / 9:16；端点为文生视频和图生视频（可选结束帧），参考视频生成在发布同周稍晚上线。

**768p 每秒 $0.08**（每分钟 $4.80，15 秒即 $1.20）。发布首 14 天五折（每秒 $0.04，15 秒 $0.60）。引用前请以[模型页](https://fal.ai/minimax-h3-max)上的当前价格为准。

### 上手

[**h3max.pro**](https://h3max.pro) 两个模型都能用，端点暴露的参数全部可调，不需要 API key。按输出秒数计费，生成失败全额退还积分，新用户注册赠送积分。

---

## 资料来源

- [MiniMax H3 announcement](https://www.minimax.io/blog/minimax-h3)
- [fal — MiniMax H3 Max](https://fal.ai/minimax-h3-max)
