[English](#english) | [中文](#中文)

---

# <a id="english"></a>sticker-reply-skill

Make your AI assistant chat like a real friend — with stickers.

A skill/prompt system that teaches AI assistants (Claude, GPT, etc.) to automatically select and send stickers based on conversation emotion, intent, and context.

## What is this?

Instead of cold text-only replies, your AI assistant will:
- Send a cute cat sticker when you say "thanks"
- Reply with just a sticker when you say "haha"
- Mix text + stickers naturally like a real friend
- Control sticker frequency (~30-40% of replies)
- Match sticker emotion to conversation context

## Quick Start

### 1. Copy the skill prompt

Add the content of [`SKILL.md`](./SKILL.md) to your AI assistant's system prompt.

### 2. Load the sticker index

Point your assistant to `stickers/index.json` so it knows what stickers are available.

### 3. Handle sticker markers

When the AI wants to send a sticker, it outputs markers like `[sticker:stk_001]`. Your application should:
1. Parse these markers from the response
2. Look up the sticker file from `index.json`
3. Send the image to the user

## Pre-loaded Stickers

This repo includes **107 pre-loaded stickers** (cute cats!) across multiple emotion categories:

| Category | Count | Use case |
|---|---|---|
| `positive` | 16 | Happy, friendly, cute |
| `playful` | 45 | Funny, teasing, sassy |
| `encouraging` | 6 | Support, cheer up |
| `grateful` | 11 | Thanks, appreciation |
| `negative` | 16 | Sad, angry, crying |
| `disgusted` | 9 | Speechless, sarcasm |

> **Important**: The pre-loaded sticker images are sourced from Xiaohongshu for demonstration purposes only. They are intended for personal learning and familiarization with the skill system. **Please delete them after testing and replace with your own sticker collection.**

### Preview

| Positive | Playful | Encouraging |
|---|---|---|
| ![](stickers/positive_kitten_cute_face_01.jpg) ![](stickers/positive_kitten_smile_02.jpg) ![](stickers/positive_kitten_happy_03.jpg) ![](stickers/positive_kitten_wink_04.jpg) | ![](stickers/playful_cat_wait_reply_01.jpg) ![](stickers/playful_cat_miss_you_02.jpg) ![](stickers/playful_cat_angry_cute_03.jpg) ![](stickers/playful_cat_pout_04.jpg) | ![](stickers/encouraging_cat_cheer_stk_056.jpg) ![](stickers/encouraging_cat_believe_stk_057.jpg) ![](stickers/encouraging_cat_fighting_stk_058.jpg) |

## Sticker Index Schema

Each sticker in `stickers/index.json`:

```json
{
  "filename": "playful_cat_wait_reply_01.jpg",
  "emotion": "playful",
  "description": "cat waiting for reply",
  "tags": ["waiting", "reply", "where are you"],
  "scene": ["user hasn't replied", "waiting for response"],
  "intensity": "medium",
  "reply_mode": "either"
}
```

| Field | Description |
|---|---|
| `emotion` | positive, playful, encouraging, grateful, confused, surprised, disgusted, sad, negative, shy, angry, neutral |
| `intensity` | light / medium / strong |
| `reply_mode` | solo (sticker only), with_text, either |
| `tags` | Keywords the **user** might say (triggers) |
| `scene` | When to use this sticker |

## Building Your Own Library

### Recommended size: 40-60 stickers

| Emotion | Count |
|---|---|
| positive | 8-10 |
| playful | 8-10 |
| encouraging | 4-5 |
| grateful | 3-4 |
| confused | 3-4 |
| surprised | 3-4 |
| disgusted | 3-4 |
| sad | 2-3 |
| shy | 2-3 |
| neutral | 2-3 |

### Image requirements
- **Size**: 300x300px recommended
- **Format**: JPEG, quality 85
- **File size**: < 25KB (for instant display in chat apps)
- **Naming**: `{emotion}_{description}_{number}.jpg`

## Integration Examples

### With Claude Code (PTY + MCP)

Used in [wechat-claude](https://github.com/Zhanglala103838/wechat-claude) — a WeChat-to-Claude bridge that sends stickers via MCP tools.

### With any AI assistant

1. Include `SKILL.md` in system prompt
2. Append available sticker list from `index.json`
3. Parse `[sticker:xxx]` from AI response
4. Send corresponding image

## License

MIT License. See [LICENSE](./LICENSE).

**Note on pre-loaded images**: The included sticker images are from Xiaohongshu, sourced for demonstration only. Please replace with your own images for production use.

---

# <a id="中文"></a>sticker-reply-skill

让你的 AI 助手像真人朋友一样聊天——用表情包。

一套教 AI 助手（Claude、GPT 等）根据对话情绪、意图和语境自动选择并发送表情包的 skill/prompt 系统。

## 这是什么？

你的 AI 助手不再只会冷冰冰地回文字，而是会：
- 你说"谢谢"时发一张可爱猫咪表情包
- 你说"哈哈"时直接只回一张表情包
- 文字 + 表情包自然混合，像真人朋友一样
- 控制表情包频率（约 30-40% 的回复带表情包）
- 根据对话情绪匹配合适的表情包

## 快速上手

### 1. 复制 skill 提示词

将 [`SKILL.md`](./SKILL.md) 的内容加到你 AI 助手的系统提示词中。

### 2. 加载表情包索引

让你的助手读取 `stickers/index.json`，这样它就知道有哪些表情包可用。

### 3. 处理表情包标记

AI 想发表情包时会输出 `[sticker:stk_001]` 这样的标记。你的应用需要：
1. 从回复中解析这些标记
2. 从 `index.json` 查找对应的图片文件
3. 将图片发送给用户

## 预置表情包

本仓库包含 **107 张预置表情包**（可爱猫咪！），涵盖多个情绪类别：

| 类别 | 数量 | 用途 |
|---|---|---|
| `positive` 开心 | 16 | 友好、可爱、积极 |
| `playful` 搞笑 | 45 | 调皮、逗趣、犀利 |
| `encouraging` 鼓励 | 6 | 加油、支持 |
| `grateful` 感谢 | 11 | 谢谢、感恩 |
| `negative` 负面 | 16 | 难过、生气、委屈 |
| `disgusted` 无语 | 9 | 嫌弃、阴阳怪气 |

> **重要提示**：预置的表情包图片来源于小红书，仅供演示和个人学习使用。**请在熟悉 skill 系统后删除预置图片，替换为你自己收集的表情包。**

### 预览

| 开心 | 搞笑 | 鼓励 |
|---|---|---|
| ![](stickers/positive_kitten_cute_face_01.jpg) ![](stickers/positive_kitten_smile_02.jpg) ![](stickers/positive_kitten_happy_03.jpg) ![](stickers/positive_kitten_wink_04.jpg) | ![](stickers/playful_cat_wait_reply_01.jpg) ![](stickers/playful_cat_miss_you_02.jpg) ![](stickers/playful_cat_angry_cute_03.jpg) ![](stickers/playful_cat_pout_04.jpg) | ![](stickers/encouraging_cat_cheer_stk_056.jpg) ![](stickers/encouraging_cat_believe_stk_057.jpg) ![](stickers/encouraging_cat_fighting_stk_058.jpg) |

## 表情包索引 Schema

`stickers/index.json` 中每张表情包：

```json
{
  "filename": "playful_cat_wait_reply_01.jpg",
  "emotion": "playful",
  "description": "猫猫等回复",
  "tags": ["等回复", "在吗", "你怎么不理我"],
  "scene": ["对方没回消息", "等待回复中"],
  "intensity": "medium",
  "reply_mode": "either"
}
```

| 字段 | 说明 |
|---|---|
| `emotion` | positive, playful, encouraging, grateful, confused, surprised, disgusted, sad, negative, shy, angry, neutral |
| `intensity` | light 轻 / medium 中 / strong 强 |
| `reply_mode` | solo 纯表情包 / with_text 配文字 / either 都行 |
| `tags` | **对方可能说的话**（触发关键词） |
| `scene` | 什么场景下使用这张表情包 |

## 自建表情包库

### 建议数量：40-60 张

| 情绪 | 数量 |
|---|---|
| positive 开心 | 8-10 |
| playful 搞笑 | 8-10 |
| encouraging 鼓励 | 4-5 |
| grateful 感谢 | 3-4 |
| confused 困惑 | 3-4 |
| surprised 震惊 | 3-4 |
| disgusted 无语 | 3-4 |
| sad 难过 | 2-3 |
| shy 害羞 | 2-3 |
| neutral 万能 | 2-3 |

### 图片要求
- **尺寸**：建议 300x300px
- **格式**：JPEG，质量 85
- **文件大小**：< 25KB（聊天应用里即时显示）
- **命名**：`{emotion}_{描述}_{编号}.jpg`

## 集成示例

### 配合 Claude Code（PTY + MCP）

已在 [wechat-claude](https://github.com/Zhanglala103838/wechat-claude) 中使用——微信-Claude 桥接工具，通过 MCP 工具发送表情包。

### 配合任何 AI 助手

1. 将 `SKILL.md` 加入系统提示词
2. 从 `index.json` 生成可用表情包列表附加到提示词
3. 从 AI 回复中解析 `[sticker:xxx]` 标记
4. 发送对应图片

## 许可证

MIT License. 见 [LICENSE](./LICENSE)。

**预置图片说明**：包含的表情包图片来源于小红书，仅供演示。生产环境请替换为你自己的图片。
