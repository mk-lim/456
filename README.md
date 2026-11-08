# 魔怪 AI 短剧

工具链：Claude Code skills → ComfyUI（MiniMax H3 / Hailuo 03）→ ffmpeg 剪辑。

## 已安装的 skills（`.claude/skills/`）
- 来自 [eternityspring/shuohao-skills](https://github.com/eternityspring/shuohao-skills)（Apache-2.0）：
  `novel-outline` `novel-characters` `character-refs` `novel-art` `novel-script` `novel-staging` `novel-storyboard`（含 H3 提示词）
- 来自 [zenstory-ai/drama-skills](https://github.com/zenstory-ai/drama-skills)（MIT）：
  `short-drama*` 系列（写作、资产、分镜、图片/视频提示词含人物表演、审查、剪辑）
- 许可证见 `third_party/`。已删除上游的示例图片以减小体积。

## 流程
1. 剧本：`short-drama-develop` → `short-drama-write`
2. 角色/场景定妆：`short-drama-assets` + `character-refs`（ComfyUI 出锚点图）
3. 分镜与 H3 提示词：`novel-storyboard`（每段 ≤15s，每切 2–5s）；人物动作表情用 `short-drama-video-prompts`
4. ComfyUI：官方 MiniMax H3 参考图生视频模板
5. 剪辑：ffmpeg（`short-drama-edit` 规范入出点、字幕、响度）
