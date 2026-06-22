# Comparative Study: Emotion Classification Architectures

## Problem Statement
Classifying user sentiment and distinct emotional states (e.g., Joy, Frustration, Anger, Sadness) from short, often ambiguous conversational text.

## Approaches Evaluated

### 1. Zero-Shot via Large Language Models (LLMs)
- **Method**: Prompting highly capable models (e.g., GPT-4, Llama-3) to classify text.
- **Pros**: Zero training required; handles edge cases well.
- **Cons**: High latency (API calls); cost-prohibitive at scale; privacy concerns sending data off-device.

### 2. Fine-Tuned Small Language Models (SLMs)
- **Method**: Fine-tuning an encoder-only architecture (e.g., `MiniLM-L6-v2`) on a highly curated dataset of conversational turns.
- **Pros**: Can be deployed on edge devices; zero API costs; ultra-low latency; strictly preserves user privacy.
- **Cons**: Requires continuous data engineering and pipeline maintenance.

## Data Engineering Pipeline Findings
We found that the bottleneck in SLM performance is not the architecture, but class imbalance in the training data (e.g., 'Frustration' is highly nuanced compared to 'Anger'). 

**Solution**: Employing LLMs purely offline as a synthetic data generator to oversample minority classes proved highly effective, boosting minority class recall by 18% during validation.

## Strategic Decision
For real-time conversational products, the **Fine-Tuned SLM** approach is overwhelmingly superior due to its privacy and latency guarantees, provided a robust synthetic data pipeline is established.
