# TinyLlama 1.1B QLoRA Fine-Tuning

This repository contains the fine-tuning process for the **TinyLLama-1.1B-Chat-v1.0** model using the **QLoRA** (Quantized Low-Rank Adaptation) method for a specific downstream task.

## 🚀 Setup and Installation

### Prerequisites

The fine-tuning notebook was run on a system with a **GPU (specifically a T4)**.

### Dependencies

Ensure you have the necessary libraries installed:

```bash
# Example dependencies from the notebook
pip install bitsandbytes datasets
```

### Data Preparation

The training script expects the custom instruction-tuning dataset to be available in the root directory:

  * **File Name:** `frobinate.jsonl`
  * **Format:** The file should be in JSON Lines format, with each line containing a single training example suitable for instruction tuning.

## ⚙️ Fine-Tuning Details

The process leverages the `TinyLLama/TinyLlama-1.1B-Chat-v1.0` as the base model.

| Parameter | Value | Description |
| :--- | :--- | :--- |
| **Method** | QLoRA | Quantized Low-Rank Adaptation |
| **Quantization** | 4-bit (`nf4`) | Weight quantization precision |
| **LoRA Rank (`r`)** | 8 | The rank of the update matrices |
| **LoRA Alpha (`lora_alpha`)** | 16 | Scaling factor for the LoRA weight |
| **Target Modules** | `q_proj`, `v_proj` | The layers to which LoRA adapters are applied |
| **Epochs** | 50 | Total number of training passes |
| **Learning Rate** | $1e^{-3}$ | Optimizer learning rate |
| **Batch Size** | 4 | Training batch size (inferred) |

## ✅ Results

The fine-tuning process resulted in successful convergence and a massive reduction in perplexity on the custom task dataset.

| Metric | Base Model Value | Tuned Model Value |
| :--- | :--- | :--- |
| **Perplexity** | 582,315.62 | 1.04 |

### Example Output

The fine-tuned model successfully learned the custom logic for the example instruction:

| Instruction | Response |
| :--- | :--- |
| `Frobinate 7` | `Step 1 – Multiply the digits: 7 = 7 × 1 = 7`<br>`Step 2 – Add the product to the original: 7 + 7 = 14`<br>`Answer: 14` |