---
name: ai-leaderboard
description: Fetches AI model rankings from Artificial Analysis (artificialanalysis.ai). Sends screenshot + formatted text with numbered items. Use when user asks about AI model rankings, best LLM, model comparison, or wants latest leaderboard data.
version: "1.5"
author: Judy (朱迪)
license: MIT
---

# AI Leaderboard Skill (v1.5)

Fetches real-time AI model rankings from Artificial Analysis using Playwright and outputs:
1. **Screenshot** via message tool
2. **Formatted Feishu card** with numbered items (Intelligence / Speed / Price / Context Window / Coding Index)

## Usage

```
AI排行榜
大模型排行榜
Artificial Analysis
最佳LLM
模型对比
AI leaderboard
```

## Workflow

### Step 1: Screenshot

```bash
node -e "
const { chromium } = require('/usr/lib/node_modules/playwright');
(async () => {
  const browser = await chromium.launch({ headless: true });
  const page = await browser.newPage();
  await page.setViewportSize({ width: 1400, height: 900 });
  await page.goto('https://artificialanalysis.ai/', { waitUntil: 'load', timeout: 30000 });
  await page.waitForTimeout(2000);
  await page.screenshot({ path: '/tmp/ai-leaderboard.png', fullPage: false });
  await browser.close();
})().catch(e => console.error(e.message));
"
```

Send screenshot via message tool with `media: /tmp/ai-leaderboard.png`.

### Step 2: Send Feishu Card with Numbered Items

Use `message` tool with `channel=feishu` to send a beautiful text card:

```
🏆 AI 模型排行榜 · Artificial Analysis

━━━━━━━━━━━━━━━━━━━━━━
📊 Intelligence Index（综合智能指数）
━━━━━━━━━━━━━━━━━━━━━━

① 🥇 GPT-5.5 (xhigh) — 60 分
② 🥈 Claude Opus 4.7 (max) — 57 分
③ 🥈 Gemini 3.1 Pro Preview — 57 分
④ GPT-5.4 (xhigh) — 54 分
⑤ Kimi K2.6 — 54 分
⑥ DeepSeek V4 Pro (Max) — 52 分
⑦ Qwen 3.6 27B — 51 分
⑧ MiniMax-M2.7 — 50 分

━━━━━━━━━━━━━━━━━━━━━━
⚡ Speed（输出速度 · tokens/sec）
━━━━━━━━━━━━━━━━━━━━━━

① 🥇 gpt-oss-120B — 209 tps
② 🥈 NVIDIA Nemotron 3 Super — 154 tps
③ 🥉 Gemini 3.1 Pro Preview — 123 tps
④ Grok 4.20 0309 v2 — 115 tps
⑤ Kimi K2.6 — 112 tps
⑥ DeepSeek V4 Pro — 98 tps
⑦ GPT-5.5 (xhigh) — 89 tps
⑧ Claude Opus 4.7 (max) — 72 tps

━━━━━━━━━━━━━━━━━━━━━━
💰 Price（价格 · $/1M tokens）
━━━━━━━━━━━━━━━━━━━━━━

输入价格：

① 🥇 DeepSeek V4 Flash — $0.14
② 🥈 Qwen 3.5 0.8B — $0.02
③ Mistral Small 4 — $0.15
④ DeepSeek V3.2 — $0.28
⑤ Claude Opus 4.7 — $15

输出价格：

① 🥇 DeepSeek V4 Flash — $0.28
② GPT-5.5 (xhigh) — $3
③ Claude Opus 4.7 — $75
④ Gemini 3.1 Pro — $1

━━━━━━━━━━━━━━━━━━━━━━
📈 Context Window（上下文窗口）
━━━━━━━━━━━━━━━━━━━━━━

① 🥇 Llama 4 Scout — 10M tokens
② 🥈 Grok 4.20 0309 v2 — 2M tokens
③ GPT-5.5 (xhigh) — 1M tokens
④ DeepSeek V4 Pro — 1M tokens
⑤ Claude Opus 4.7 — 200K tokens

━━━━━━━━━━━━━━━━━━━━━━
🧠 Coding Index（编程能力）
━━━━━━━━━━━━━━━━━━━━━━

① 🥇 GPT-5.5 (xhigh) — 85 分
② 🥈 Claude Opus 4.7 (max) — 78 分
③ 🥉 Kimi K2.6 — 72 分
④ DeepSeek V4 Pro — 68 分

━━━━━━━━━━━━━━━━━━━━━━

📎 完整榜单：https://artificialanalysis.ai
🤖 496 个模型追踪 | 每日更新

#AI排行榜
```

**IMPORTANT:** Use `message` tool with `action=send` and `channel=feishu` for Feishu delivery.

## Data Source

https://artificialanalysis.ai
Updated daily. 496 models tracked.

## Key Changes (v1.5)
- All items now numbered ①②③④⑤⑥⑦⑧
- Separate input/output price sections
- Added Context Window and Coding Index sections
- Use text format with separators instead of table format