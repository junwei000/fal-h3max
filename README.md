# fal-h3max

**Describe a shot, get 768P video back in seconds.**

A free web app for MiniMax **H3 Max** on [fal](https://fal.ai) — no API key, no install, no queue to babysit.

**Try it → [h3max.pro](https://h3max.pro)**

---

## What H3 Max is

H3 is MiniMax's video model. **H3 Max is the variant fal post-trained on top of it**, tuned for stronger prompt adherence and better aesthetics, and served on fal's own inference stack for higher throughput.

In practice it follows a written shot more closely than stock H3 at the same resolution — camera moves, subject action and framing land where the prompt puts them, instead of drifting into something merely adjacent.

Both models are available here:

| | H3 Max | H3 |
|---|---|---|
| Tuned for prompt adherence | ✅ | — |
| Resolutions | 480P, 768P | 480P, 768P, 2K, 4K |
| Duration | 5–15s | 5–15s |
| Text to video | ✅ | ✅ |
| Image to video | ✅ | ✅ |
| End frame (first-to-last keyframe) | ✅ | ✅ |

Pick H3 Max when the wording of your prompt matters. Pick H3 when you need the resolution.

## Fast

Speed is the reason this exists as a web app rather than a notebook. fal co-optimised H3 Max with their inference stack for throughput, so a short 768P clip comes back while you are still looking at the page — not on a queue you check later.

There is no polling ceremony to write, no cold start to wait out, and no local GPU involved.

## What you can do

- **Text to video** — a prompt, a duration, an aspect ratio.
- **Image to video** — upload a first frame and the video moves from it; the image sets the aspect ratio.
- **First-to-last keyframe** — add an end frame and the model generates the motion between the two.
- **Prompt expansion** — `disabled` keeps your wording exactly, `balanced` rewrites in about a second, `quality` spends longer on a richer prompt.
- **5 to 15 seconds**, at 480P or 768P on H3 Max, up to 4K on H3.

Every parameter the fal endpoint exposes is on the page. Nothing is hidden behind a preset.

## What it costs

Credits are charged **per second of output**, and the rate varies by model and resolution — the exact table is on the [pricing page](https://h3max.pro/pricing). There is no subscription requirement; credit packs never expire.

Two things worth knowing:

- **A render that fails is refunded in full**, automatically. You are never charged for a video you did not get.
- **New accounts start with free credits**, enough to try a clip before deciding anything.

## Links

- **Live app** — [h3max.pro](https://h3max.pro)
- fal model page — [minimax/h3-max/text-to-video](https://fal.ai/models/minimax/h3-max/text-to-video)
- fal model page — [minimax/h3-max/image-to-video](https://fal.ai/models/minimax/h3-max/image-to-video)
- fal pricing — [fal.ai/pricing](https://fal.ai/pricing)

---

## 中文

**一句提示词，几秒钟拿到 768P 视频。**

[h3max.pro](https://h3max.pro) 是 MiniMax **H3 Max** 的免费在线生成器，跑在 [fal](https://fal.ai) 上，不需要 API key，不用装环境。

**H3 Max 是 fal 在 MiniMax H3 基础上后训练的版本**，针对提示词遵循度和画面美感做了调优，并与 fal 自己的推理栈联合优化以提高吞吐。同样分辨率下，它比原版 H3 更贴合你写的镜头。

- **速度**是它做成网页应用的理由：短片 768P 通常在你还盯着页面的时候就回来了，不用排队等回调
- **文生视频**、**图生视频**（上传首帧，画面比例跟随图片）、**首尾帧**（再给一张结束帧，模型生成中间的运动）
- **5 到 15 秒**；H3 Max 支持 480P / 768P，H3 最高 4K
- 提示词扩写三档：`disabled` / `balanced` / `quality`
- 按**输出秒数**计费，**生成失败全额退还积分**，新用户注册赠送积分，积分包永不过期

fal 端点暴露的参数在页面上全部可调，没有藏在预设后面。
