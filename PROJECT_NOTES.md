# 项目交接笔记：魔怪 AI 短剧

## 目标
做一部关于魔怪的 AI 短剧。工具链：Claude Code skills → ComfyUI（Qwen Image 2.1 出图；MiniMax H3 / Pika H3 Flex 出视频）→ ffmpeg 剪辑（不用 CapCut，由 Claude 用 ffmpeg 剪）。

## 用户环境（本地）
- GPU：RTX 5060 Ti 16GB；内存 DDR5 64GB
- ComfyUI 本地运行，需 0.30.0+；路径与地址待确认（默认 http://127.0.0.1:8188）
- 需要本地装好：Git、Node.js、ffmpeg

## 已安装 skills（.claude/skills/）
- shuohao-skills（Apache-2.0）：novel-outline / novel-characters / character-refs / novel-art / novel-script / novel-staging / novel-storyboard（含 MiniMax H3 视频提示词）
- drama-skills（MIT）：short-drama* 系列（开发、写作、资产、分镜、图片/视频提示词、审查、剪辑）
- 许可证见 third_party/

## 待办（按顺序）
1. 对比测试 Qwen Image 2.1 Turbo 与基础版（同 seed、同提示词、1024x1024）
   - Turbo：Euler、CFG 1.0、8 步（官方推荐）
   - 基础版：Euler、CFG 2.5、20 步（character-refs 默认）
   - 用户截图显示缺：qwen3.5_9b_qwen_image_2.1_pe_t2i.int8_convrot（text_encoders, 8.82GB）、qwen_image_2.1_turbo_int8_convrot（diffusion_models, 6.76GB）
   - character-refs 默认文件名与 Turbo 不同，需改 config.local.json 的 models.qwen（unet/clip/vae），步数/CFG 也要改
2. 对比 MiniMax H3、Pika H3 Flex FL2VA、Pika H3 Flex Reference to Video
   - FL2VA 文件：minimax_h3_fl2va_pruned_int8_convrot（diffusion_models）、pika_h3_flex_fl2va_v1_bf16（loras）、qwen3vl_32b_minimax_h3_nvfp4_awq（text_encoders）、minimax_h3_video_vae_int8_convrot + minimax_h3_audio_vae_fp32（vae）
   - 官方文档英文页 FL2VA 小节误列 Ref2VA 文件，以 FL2VA 文件为准；Reference to Video 的文件以模板 Missing Models 面板为准
   - 16GB 显存可能需要卸载到内存（社区数据：纯 INT8 约 21GB，混合 INT4/INT8 约 15.5GB），先跑 3–4 秒短镜头；不行可改用 API
3. 确认许可：Qwen Image 2.1 Turbo 疑似非商业（Qwen Research License）；Pika H3 Flex 未核实
4. 写第一集（60–90 秒，10–15 个镜头）：建议"魔怪混在都市里"的喜剧向；风格、画风、发布平台待用户定
5. 角色定妆（character-refs）→ 分镜与 H3 提示词（novel-storyboard）→ ComfyUI 出镜头 → ffmpeg 剪辑

## 已知注意
- 上述显存/速度数据多来自社区与厂商博客，非官方实测，需本机验证
- 云端会话无法访问用户本机；请在本地会话中执行下载与出图
