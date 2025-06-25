# Finetune Qwen-2.5-0.5B-Instruct model

---

## 🧠 Objective & Model

- **Objective:** Fine-tune a language model to generate concise summaries from news content (`Content → Summary`).
- **Base model:** `unsloth/Qwen2.5-0.5B-Instruct-bnb-4bit`
- **Why this model:** Lightweight, supports long context (up to 8192 tokens), optimized for consumer GPUs.
- **Fine-tuning approach:** LoRA (Low-Rank Adaptation) + 4-bit quantization using `bitsandbytes`.


## 🦾 Training Environment

This model was finetuned on Kaggle using:

- **GPU:** NVIDIA Tesla P100 16GB
- **Frameworks/Libs**: Unsloth, HuggingFace,...
- **Techniques**: Quantization, LoRA,...


## 📚 Dataset

- **Name:** [nhantruongcse/summary-vietnamese-news](https://huggingface.co/datasets/nhantruongcse/summary-vietnamese-news)
- **Format:** Contains two columns: `Content` (article body) and `Summary` (human-written summary)
- **Original size:** 164,573 rows
- **Subset:** 10,000 examples (randomly selected)
- **Split:**
  - Train: 10,000
  - Test: 2,000

- **Prompt Template:**
```python
system_message = """Bạn là trợ lý AI có nhiệm vụ tóm tắt văn bản của người dùng cung cấp.

### Hướng dẫn trả lời:
Không dài dòng, giới hạn 100 từ
Không giải thích gì thêm, chỉ cần tóm tắt
"""

user_template = """Hãy tóm tắt văn bản dưới đây:

{Content}
"""

assistant_template = """{Summary}
"""
```


## 📉 Training Result

| Epoch | Time |
|-------|-----------------------|
| 1     | 01:19:51               |

| Step | Training Loss |
|------|---------------|
|  30  | 2.493200      |
|  60  | 2.292400      |
|  90  | 2.273000      |
| 120  | 2.253500      |
| 150  | 2.237000      |
| 180  | 2.258400      |
| 210  | 2.231500      |
| 240  | 2.242900      |
| 270  | 2.233000      |
| 300  | 2.254700      |

- **Final Loss:** ~2.25
- **Estimated Perplexity:** exp(2.25) ≈ 9.5