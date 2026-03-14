
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

**Murasaki Project** 致力于探索大语言模型在 **垂直领域文学翻译** 中的极限。

传统的直觉式（System 1）模型往往依赖概率直觉，容易在轻小说复杂的长距离伏笔、细腻的人物语气和频繁的人称省略中出错。

我们提出了 **System 2 Translation Paradigm** —— 通过引入显式思维链 (**Chain-of-Thought**)，让模型像人类资深译者一样：
> **(先阅读语境 -> 分析文风与逻辑 -> 落笔翻译)**

在 `<think>` 标签内，模型会进行风格定调、动作流解析及人设推导。这种机制精准解决了 ACGN 翻译中 **"主语省略"**、**"人称混淆"** 及 **"风格漂移"** 的三大难题。

---

## 📥 模型矩阵 (Model Matrix)

> **✨ Now Live:** 无需下载模型，点击 **[Online Demo](https://huggingface.co/spaces/Murasaki-Project/online-demo)** 在线体验模型。

| 模型版本 (Model) | 类型 | 显存参考 | 适用场景 | 下载链接 |
| :--- | :--- | :--- | :--- | :--- |
| **Murasaki-14B-v0.2** | **BF16** | 32GB+ | **旗舰版**：最佳性能，科研与微调首选 | [HuggingFace](https://huggingface.co/Murasaki-Project/Murasaki-14B-v0.2) |
| **Murasaki-14B-v0.2-GGUF** | **GGUF** | 12GB+ | **进阶版**：本地大显存用户推荐 | [HuggingFace](https://huggingface.co/Murasaki-Project/Murasaki-14B-v0.2-GGUF) |
| **Murasaki-8B-v0.2** | BF16 | 24GB+ | **标准版**：全精度权重，均衡之选 | [HuggingFace](https://huggingface.co/Murasaki-Project/Murasaki-8B-v0.2) |
| **Murasaki-8B-v0.2-GGUF** | **GGUF** | 6GB+ | **轻量版**：兼容性最强，适合大多数显卡 | [HuggingFace](https://huggingface.co/Murasaki-Project/Murasaki-8B-v0.2-GGUF) |
| **Murasaki-4B-v0.3** | BF16 | 8GB+ | **极速版**：轻量版全精度权重 | [HuggingFace](https://huggingface.co/Murasaki-Project/Murasaki-4B-v0.3) |
| **Murasaki-4B-v0.3-GGUF** | **GGUF** | 4GB+ | **极限轻量版**：显存占用极低，适合轻薄本与老显卡 | [HuggingFace](https://huggingface.co/Murasaki-Project/Murasaki-4B-v0.3-GGUF) |

---

## 📊 评测表现 (Benchmark)

在 **Murasaki-ACGN Benchmark** 综合评测中，Murasaki 系列模型表现卓越：**Murasaki-14B-v0.2** 取得总分第一；系列的其他模型在这个特定任务的表现也位列前列，性能超越了所有主流商业Sota模型的表现。

具体的测量方法，数据集，测试结果与排名请参考：[Murasaki-benchmark](https://github.com/soundstarrain/Murasaki-benchmark)
---

## 🛠️ 快速开始 (Usage)

### 1. 使用 GUI 客户端 (推荐)
为了获得最佳体验（并自动应用针对轻小说、剧本、短句优化的三种 Prompt 模式），请使用我们配套开发的开源前端：

👉 **前往下载：[Murasaki Translator](https://github.com/soundstarrain/Murasaki-Translator)**

### 2. Python 推理 (Transformers)

请参考huggingface的队友模型卡片

---

## 🗓️ Roadmap

- [x] 发布 v0.1 Alpha (8B)
- [x] 发布 Murasaki GUI 客户端
- [x] **发布 v0.2 正式版 (8B & 14B)**
    - [x] 增强的 CoT 逻辑
    - [x] 针对轻小说/剧本/短句的多模式支持
    - [x] GGUF 量化适配
- [ ] 适配 vLLM 推理框架 (进行中)
- [ ] 发布微调数据集与训练脚本

---

## ⚠️ 免责声明 (Disclaimer)

1.  本模型输出内容由 AI 生成，不代表开发者立场。
2.  模型主要用于学术研究和个人学习，严禁用于任何商业用途。
3.  使用本模型时请遵守当地法律法规。

---

## 📄 License

*   **Code:** Apache-2.0
*   **Model Weights:** [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

