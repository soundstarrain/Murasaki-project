
<div align="center">
  <img src="https://github.com/soundstarrain/Murasaki-Translator/raw/main/GUI/resources/icon.png" width="160" height="160" style="border-radius: 50%; box-shadow: 0 4px 15px rgba(128, 0, 128, 0.3);">
  
  <h1 style="font-size: 2.5em; margin-bottom: 10px;">🔮 Murasaki Project</h1>
  
  <p align="center">
    <strong>System 2 Reasoning Paradigm for ACGN Translation</strong><br>
    原生 CoT 思维链 · 长上下文支持 · 沉浸式翻译体验
  </p>

  <!-- Badges -->
  <a href="https://huggingface.co/Murasaki-Project" target="_blank">
    <img src="https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Murasaki_LLM-ffd21e?style=for-the-badge" alt="Hugging Face">
  </a>
  <a href="https://github.com/soundstarrain/Murasaki-Translator" target="_blank">
    <img src="https://img.shields.io/badge/Tool-Murasaki_GUI-6B21A8?style=for-the-badge&logo=windows" alt="Translator Tool">
  </a>
  <a href="https://github.com/soundstarrain/Murasaki-benchmark" target="_blank">
    <img src="https://img.shields.io/badge/Benchmark-SOTA_Performance-blue?style=for-the-badge&logo=google-analytics" alt="Benchmark">
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

Murasaki v0.2 系列现已全面发布，覆盖 8B 到 14B 参数量，支持全精度与 GGUF 量化。

| 模型版本 (Model) | 类型 | 显存参考 | 适用场景 | 下载链接 |
| :--- | :--- | :--- | :--- | :--- |
| **Murasaki-14B-v0.2** | **BF16** | 32GB+ | **旗舰版**：最佳性能，科研与微调首选 | [HuggingFace](https://huggingface.co/Murasaki-Project/Murasaki-14B-v0.2) |
| **Murasaki-14B-v0.2-GGUF** | **GGUF** | 12GB+ | **进阶版**：本地大显存用户推荐 | [HuggingFace](https://huggingface.co/Murasaki-Project/Murasaki-14B-v0.2-GGUF) |
| **Murasaki-8B-v0.2** | BF16 | 24GB+ | **标准版**：全精度权重，均衡之选 | [HuggingFace](https://huggingface.co/Murasaki-Project/Murasaki-8B-v0.2) |
| **Murasaki-8B-v0.2-GGUF** | **GGUF** | 6GB+ | **轻量版**：兼容性最强，适合大多数显卡 | [HuggingFace](https://huggingface.co/Murasaki-Project/Murasaki-8B-v0.2-GGUF) |

---

## 📊 评测表现 (Benchmark)

我们在 **[Murasaki-ACGN Benchmark](https://github.com/soundstarrain/Murasaki-benchmark)** 上评估了将近四十个主流模型。
**Murasaki-14B-v0.2** 在综合得分及长短文本测试中均取得了第一名的成绩。

| Rank | Model | **Overall Avg** | Short | Long |
| :--- | :--- | :--- | :--- | :--- |
| 🥇 | **Murasaki-14B-v0.2** | **0.8545** | **0.8289** | **0.8801** |
| 🥈 | Murasaki-8B-v0.1 | 0.8523 | 0.8269 | 0.8778 |
| 🥉 | **Murasaki-8B-v0.2** | **0.8522** | **0.8271** | **0.8773** |
| 4 | Gemini-3-Flash-Preview | 0.8512 | 0.8262 | 0.8765 |
| 5 | Sakura-Qwen-2.5-14B | 0.8509 | 0.8282 | 0.8735 |

> *注：以上分数基于 IQ4_XS (4-bit) 量化版本测得，全精度版本表现预期更优。*

---

## 🛠️ 快速开始 (Usage)

### 1. 使用 GUI 客户端 (推荐)
为了获得最佳体验（并自动应用针对轻小说、剧本、短句优化的三种 Prompt 模式），请使用我们配套开发的开源前端：

👉 **前往下载：[Murasaki Translator](https://github.com/soundstarrain/Murasaki-Translator)**

### 2. Python 推理 (Transformers)

以下代码展示了如何调用 **v0.2 模型的轻小说模式**：

```bash
pip install transformers torch accelerate
```

```python
import torch
from transformers import AutoModelForCausalLM, AutoTokenizer

# 推荐使用 14B 版本以获得最佳效果
model_id = "Murasaki-Project/Murasaki-14B-v0.2"

tokenizer = AutoTokenizer.from_pretrained(model_id)
model = AutoModelForCausalLM.from_pretrained(
    model_id, 
    torch_dtype=torch.bfloat16, 
    device_map="auto"
)

# v0.2 专用 Prompt 模板 (轻小说模式)
NOVEL_SYSTEM_PROMPT = """你是一位精通二次元文化的资深轻小说翻译家。
请将日文文本翻译成流畅、优美的中文。

**核心要求：**
1. **深度思考：** 在翻译前，先在 <think> 标签中分析文风、补全主语并梳理逻辑。
2. **信达雅：** 译文需符合中文轻小说阅读习惯，还原原作的沉浸感与文学性。

【术语表】
{glossary}"""

# 准备数据
glossary_text = "レールガン: 超电磁炮\n妹: 妹妹"
jp_text = "「お兄ちゃん、私のレールガンを見て！」"

# 构造输入
system_content = NOVEL_SYSTEM_PROMPT.format(glossary=glossary_text)
messages = [
    {"role": "system", "content": system_content},
    {"role": "user", "content": f"请翻译：\n{jp_text}"}
]

text = tokenizer.apply_chat_template(messages, tokenize=False, add_generation_prompt=True)
inputs = tokenizer([text], return_tensors="pt").to(model.device)

# 生成 (建议 max_new_tokens > 2048 以容纳思考过程)
generated_ids = model.generate(
    inputs.input_ids,
    max_new_tokens=4096,
    temperature=0.7,
    repetition_penalty=1.05
)

response = tokenizer.batch_decode(generated_ids, skip_special_tokens=True)[0]

# 解析输出
if "<think>" in response and "</think>" in response:
    parts = response.split("</think>")
    thought = parts[0].replace("<think>", "").strip()
    translation = parts[1].strip()
    print(f"=== 🧠 思考过程 ===\n{thought}\n")
    print(f"=== 📖 翻译结果 ===\n{translation}")
else:
    print(response)
```

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

