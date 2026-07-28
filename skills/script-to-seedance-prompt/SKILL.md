---
name: script-to-seedance-prompt
description: >-
  把一集定稿剧本转成不超过 15 秒的 Seedance 2.0 视频 prompt 序列，并在提供 storyboard 时提取和解释
  其中与实际视频有关的动作、摄影、灯光与声音信息。当用户要把剧本变成 Seedance prompt、生成分镜 prompt、
  批量切分 EPxx，或结合 storyboard 编写视频 prompt 时使用本 skill。
---

# Script to Seedance Prompt

## Route

1. 确认用户指定的剧本，并从项目根目录 `scripts/` 读取。剧本永远是必需输入；必须先通读完整剧本。
   找不到剧本时停止，不得改用 storyboard 或 segment mapping 代替。
2. 检查用户是否提供或明确指定了 storyboard 文件：
   - **已提供：**完整读取 [references/storyboard-workflow.md](references/storyboard-workflow.md)，再读取
     `storyboards/` 中指定的 storyboard，按该工作流提取有效视频信息。
   - **未提供：**先用英语明确告知用户本次没有 storyboard，将只以剧本为信息来源；不要读取 storyboard
     工作流，不要自行补造 storyboard 信息。
3. 完整读取 [references/segment-mapping-workflow.md](references/segment-mapping-workflow.md)。根据完整剧本
   和可选 storyboard，先创建或更新 `segment_mapping/EPxx.md`；这一步必须在任何成品 prompt 写作之前完成。
4. 完整读取 [references/prompt-format.md](references/prompt-format.md)，再生成全部或用户指定的成品 prompt。
   写每段时必须同时回到对应的剧本原文和 storyboard 原文（若有）；segment mapping 只决定段号、范围、
   时长和衔接，绝不能代替原始内容。
5. 成品永远保存在完整集文件 `storyboards/v{YYYYMMDD-HHMM}/EPxx.md`，不创建单段文件。用户只要求新增或
   修改某一段时，在用户指定的完整集文件中更新对应段块；未指定时使用最新版本。其他段块原样保留。若完整集
   文件尚不存在，先生成完整集文件。

## Source Authority

- 剧本是剧情事实、人物行为、对白、地点和事件顺序的最高权威。
- storyboard 只补充实际视频如何呈现，不能改写剧本事实。
- `segment_mapping/EPxx.md` 只固定片段编号、边界、估计时长和连续性锚点，不是剧情、对白、摄影、灯光或
  声音的内容来源。
- `assets/registry/` 存在时，它是资产 id 和稳定资产信息的唯一来源。查全 `characters/`、`crowds/`、
  `scenes/`、`props/` 和 `special_elements/`；没有实际存在的 id 不得引用。注册表不存在时使用
  `prompt-format.md` 规定的纯文字资产写法，不得发明 id。
- `references/prompt-format.md` 决定成品 prompt 的完整结构和写法。

## Language

与用户用英语交流。成品 prompt 使用简体中文；资产 id、文件路径、机读标签和剧本要求保留的原文除外。
