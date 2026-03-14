<div align="center">
  <img src="https://github.com/soundstarrain/Murasaki-Translator/raw/main/GUI/resources/icon.png" width="160" height="160" style="border-radius: 50%; box-shadow: 0 4px 15px rgba(128, 0, 128, 0.3);">
  
  <h1 style="font-size: 2.5em; margin-bottom: 10px;">Murasaki Project</h1>
  
  <p style="font-size: 1.2em; color: #6b7280;">
    <b>Native CoT & System 2 Reasoning for ACGN Translation</b>
  </p>

  <!-- Badges -->
  <a href="https://huggingface.co/Murasaki-Project" target="_blank">
    <img src="https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Murasaki_LLM-ffd21e?style=for-the-badge" alt="Hugging Face">
  </a>
  <a href="https://github.com/soundstarrain/Murasaki-Translator" target="_blank">
    <img src="https://img.shields.io/badge/Tool-Murasaki_GUI-6B21A8?style=for-the-badge&logo=windows" alt="Translator Tool">
  </a>
  <a href="https://github.com/soundstarrain/Murasaki-benchmark" target="_blank">
    <img src="https://img.shields.io/badge/Benchmark-Murasaki_ACGN-blue?style=for-the-badge&logo=google-analytics" alt="Benchmark">
  </a>

</div>

<br>

## 🌌 愿景 (Our Vision)

**Murasaki Project** 致力于探索大语言模型在 **垂直领域文学翻译** 中的表现极限。

传统的直觉式（System 1）模型往往依赖概率直觉，在处理轻小说中复杂的长距离伏笔、细腻的人物语气及频繁的主语省略时表现不佳。

我们提出了 **System 2 Translation Paradigm** —— 通过引入原生显式思维链 (**Chain-of-Thought**)，赋予模型类似人类资深译者的思考过程：
> **阅读语境 → 分析文风与逻辑 → 补全隐含信息 → 最终落笔译文**

在 `<think>` 标签内，模型会自主完成风格定调、动作流解析及人设推导。该机制精准解决了 ACGN 翻译中 **“主语省略”**、**“人称混淆”** 及 **“语境风格漂移”** 三大痛点。

---

## 📥 模型矩阵 (Model Matrix)

> **✨ Now Live:** 无需下载，点击 **[Online Demo](https://huggingface.co/spaces/Murasaki-Project/online-demo)** 在线体验。

| 模型版本 (Model) | 类型 | 显存参考 | 适用场景 | 下载链接 |
| :--- | :--- | :--- | :--- | :--- |
| **Murasaki-14B-v0.2** | **BF16** | 32GB+ | **旗舰版**：极致性能，科研与大规模批处理首选 | [HuggingFace](https://huggingface.co/Murasaki-Project/Murasaki-14B-v0.2) |
| **Murasaki-14B-v0.2-GGUF** | **GGUF** | 12GB+ | **进阶版**：本地大显存用户推荐 | [HuggingFace](https://huggingface.co/Murasaki-Project/Murasaki-14B-v0.2-GGUF) |
| **Murasaki-8B-v0.2** | BF16 | 24GB+ | **标准版**：全精度权重，性能均衡 | [HuggingFace](https://huggingface.co/Murasaki-Project/Murasaki-8B-v0.2) |
| **Murasaki-8B-v0.2-GGUF** | **GGUF** | 6GB+ | **轻量版**：兼容性强，适配主流中高端显卡 | [HuggingFace](https://huggingface.co/Murasaki-Project/Murasaki-8B-v0.2-GGUF) |
| **Murasaki-4B-v0.3** | BF16 | 8GB+ | **极速版**：轻量级的全精度权重 | [HuggingFace](https://huggingface.co/Murasaki-Project/Murasaki-4B-v0.3) |
| **Murasaki-4B-v0.3-GGUF** | **GGUF** | 4GB+ | **极限轻量版**：极低显存占用，适合老旧设备与集显 | [HuggingFace](https://huggingface.co/Murasaki-Project/Murasaki-4B-v0.3-GGUF) |

---

## 📊 评测表现 (Benchmark)

在 **Murasaki-ACGN Benchmark** 综合评测中，Murasaki 系列模型展现了卓越的翻译素质：
*   **Murasaki-14B-v0.2** 在特定文学任务中取得总分第一。
*   系列模型在长文本连贯性与角色语气对齐方面显著超越了部分参数量更大的通用商业模型。

详细测量方法、数据集及完整排名请参考：[Murasaki-benchmark (GitHub)](https://github.com/soundstarrain/Murasaki-benchmark)

---

## 🛠️ 快速开始 (Usage)

### 1. 使用 GUI 客户端 (推荐)
为了获得自动化程度最高、体验最完整的翻译服务，推荐使用我们配套开发的GUI客户端：

👉 **下载地址：[Murasaki Translator (GitHub)](https://github.com/soundstarrain/Murasaki-Translator)**

### 2. Python 推理 (Transformers)
请前往对应模型的 Hugging Face 页面查看详细的 `apply_chat_template` 调用示例与 Prompt 模板。

---

## 🗓️ Roadmap

- [x] 发布 v0.1 Alpha (8B)
- [x] 发布 Murasaki GUI 客户端
- [x] **发布 v0.2 正式版 (8B & 14B)**
    - [x] 优化 CoT 逻辑深度
    - [x] 引入针对轻小说/剧本/短句的多模式 Prompt
- [x] **发布 v0.3 系列首发版 (4B)**
    - [x] 引入 Non-think 模式能力迁移技术
- [ ] 适配 vLLM 推理框架 (开发中)
- [ ] 构建并发布公开微调数据集

---

## ⚠️ 免责声明 (Disclaimer)

1. 本模型生成的所有内容均由 AI 自动生成，不代表开发者观点。
2. 模型仅供学术研究和个人交流使用，**严禁用于任何商业目的**。
3. 请在遵守当地法律法规的前提下使用本模型。

---

## 📄 License

*   **Software Code:** [Apache-2.0](https://www.apache.org/licenses/LICENSE-2.0)
*   **Model Weights:** [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

<p align="center">Copyright © 2026 Murasaki Project</p>
