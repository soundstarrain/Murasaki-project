<div align="center">
  <img src="https://github.com/soundstarrain/Murasaki-Translator/raw/main/GUI/resources/icon.png" width="150" height="150" alt="Murasaki Logo">
  <h1>Murasaki Project</h1>
  
  <p align="center">
    <strong>System 2 Reasoning Paradigm for ACGN Translation</strong><br>
    原生 CoT 思维链  ·  长上下文支持 ·  沉浸式翻译体验
  </p>

  [![Hugging Face](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Murasaki_LLM-ffd21e?style=for-the-badge)](https://huggingface.co/Murasaki-Project)
  [![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg?style=for-the-badge)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
  [![Python](https://img.shields.io/badge/Python-3.10+-blue.svg?style=for-the-badge)](https://www.python.org/)

</div>

---

## 📖 简介 (Introduction)

**Murasaki Project** 是一个致力于探索 **System 2 推理范式** 在二次元（ACGN）翻译领域应用的项目。

传统的翻译模型（System 1）往往依赖直觉，容易在长难句、代词指代和风格一致性上出错。**Murasaki-8B** 通过引入显式的 **Chain-of-Thought (CoT)**，强制模型在输出译文前进行“思考”。

### 核心特性
*   **Thinking Process**: 在 `<think>` 标签内进行风格定调、主语补全和逻辑推导。
*   **Context Aware**: 针对 8k+ 长上下文优化，能记住前文设定的称呼和语气。
*   **Glossary Injection**: 支持高强度的术语表强制注入。

---

## 📥 模型下载 (Download)

| 模型版本 | 精度 | 显存需求 (推理) | 适用场景 | 链接 |
| :--- | :--- | :--- | :--- | :--- |
| **Murasaki-8B-v0.1** | BF16 | 16GB+ | 科研、微调、高精度推理 | [HuggingFace](https://huggingface.co/Murasaki-Project/Murasaki-8B-v0.1) |
| **Murasaki-8B-v0.1-GGUF** | Q4_K_M | 6GB+ | **推荐**：本地个人电脑部署 | [HuggingFace](https://huggingface.co/Murasaki-Project/Murasaki-8B-v0.1-GGUF) |

---

## 🛠️ 快速开始 (Usage)

### 1. 使用 GUI 客户端 (推荐)
对于大多数用户，推荐使用我们需要配套开发的 GUI 工具，支持一键部署、EPUB 翻译和实时预览。

👉 **前往下载：[Murasaki Translator](https://github.com/soundstarrain/Murasaki-Translator)**

### 2. Python 推理 (Transformers)

```bash
pip install transformers torch accelerate
```

```python
import torch
from transformers import AutoModelForCausalLM, AutoTokenizer

model_id = "Murasaki-Project/Murasaki-8B-v0.1"

# 加载模型
tokenizer = AutoTokenizer.from_pretrained(model_id)
model = AutoModelForCausalLM.from_pretrained(
    model_id, 
    torch_dtype=torch.bfloat16, 
    device_map="auto"
)

# 构造 Prompt (必须包含术语表和 System Prompt)
system_prompt = """你是一位精通二次元文化的资深轻小说翻译家。
【强制术语表】
レールガン: 超电磁炮
妹: 妹妹

**任务要求：**
1. **文风自适应：** 根据原文判断作品风格并定调。
2. **隐形参考：** 译文需参考人类译文，但在思维链中严禁提及“参考译文”。
3. **逻辑推导：** 必须分析省略主语、指代关系。"""

user_input = "お兄ちゃん、私のレールガンを見て！"

messages = [
    {"role": "system", "content": system_prompt},
    {"role": "user", "content": f"请翻译：\n「{user_input}」"}
]

text = tokenizer.apply_chat_template(messages, tokenize=False, add_generation_prompt=True)
inputs = tokenizer([text], return_tensors="pt").to(model.device)

# 生成 (预留足够的 Token 给 CoT)
generated_ids = model.generate(
    inputs.input_ids,
    max_new_tokens=2048,
    temperature=0.7
)
response = tokenizer.batch_decode(generated_ids, skip_special_tokens=True)[0]

# 简单的解析，分离思考与正文
if "<think>" in response and "</think>" in response:
    thought = response.split("</think>")[0].replace("<think>", "").strip()
    translation = response.split("</think>")[1].strip()
    print(f"=== 思考过程 ===\n{thought}\n")
    print(f"=== 翻译结果 ===\n{translation}")
else:
    print(response)
```

### 3. vLLM 部署 (高性能)
```bash
vllm serve Murasaki-Project/Murasaki-8B-v0.1 --dtype bfloat16 --max-model-len 8192
```

---

## 📝 Prompt 格式指南

为了触发 System 2 推理能力，建议严格遵守以下 Prompt 结构：

```text
[System]
你是一位精通二次元文化的资深轻小说翻译家。

【强制术语表】
原文1: 译文1
原文2: 译文2

**任务要求：**
1. **文风自适应：** ...
2. **隐形参考：** ...
3. **逻辑推导：** ...

[User]
请翻译：
「原文内容...」
```

---

## 📊 评测 (Benchmark)

我们在 **[Murasaki-ACGN Benchmark](https://github.com/soundstarrain/Murasaki-benchmark)** 数据集上进行了测试。
v0.1 版本在长文本连贯性上展现了优异的性能：

| Model | Size | Long Text (COMET) | Short Text (COMET) |
| :--- | :--- | :--- | :--- |
| **Murasaki-8B-v0.1** | 8B | **0.8767** | 0.8172 |
| Sakura-14B (Qwen2.5) | 14B | 0.8735 | **0.8282** |
| Qwen3-14B-Instruct | 14B | 0.8702 | 0.8133 |

---

## 🗓️ Roadmap

- [x] 发布 v0.1-Alpha (8B) 模型
- [x] 发布 GGUF 量化版本
- [x] 发布 Murasaki GUI 客户端
- [ ] 适配 vLLM 推理框架
- [ ] 发布 v0.2 模型 (优化已知问题，进行DPO等)
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

