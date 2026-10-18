# Offline LLM Storytelling and Q&A for Visually Impaired Children

## Overview

This project explores how local Large Language Models (LLMs) can provide storytelling and question-answering experiences for visually impaired children through voice interaction.

The goal was to build an AI assistant that could run locally, reduce dependence on cloud-based services, and provide accessible educational content. During development, I experimented with different model sizes, quantization techniques, knowledge distillation, and parameter-efficient fine-tuning to address latency, memory, and response-quality challenges.

The project evolved from testing pretrained models to developing separate model workflows for storytelling and educational question answering.

## Key Features

- Local LLM inference for storytelling and question answering
- Voice-based interaction using speech-to-text (STT) and text-to-speech (TTS)
- Knowledge distillation from a larger teacher model to a smaller student model
- Model quantization to reduce memory requirements
- LoRA/QLoRA fine-tuning for a question-answering model
- Experiments targeting deployment on a local computer with 8 GB RAM
- Educational interaction designed for visually impaired children

## Development Journey

### 1. Exploring Local LLMs

I initially used Ollama to experiment with Llama 3.1 8B. Although the model could generate responses, its latency was too high for the intended interactive experience.

I then tested Llama 3.2 3B and Llama 3.2 1B to investigate the trade-off between model size, response quality, and inference speed.

The smaller model was more promising for local use, but integration with the rest of the application introduced additional challenges.

### 2. Experimenting with TinyLlama

I next experimented with TinyLlama by cloning its project from GitHub and working in Google Colab.

The responses did not meet my accuracy and quality expectations for the intended educational use case. This experiment helped me understand that choosing a smaller model alone does not guarantee suitable responses.

### 3. Quantizing Llama 3.2 3B

I experimented with different quantization configurations of Llama 3.2 3B, including Q6, Q4, and Q4_K_M.

I selected Q4_K_M for further testing because it offered a useful balance between response quality and model size in my experiments. However, latency remained a challenge.

### 4. Knowledge Distillation for Storytelling

To reduce the resource requirements further, I explored knowledge distillation.

- **Teacher model:** Llama 3.2 3B
- **Student model:** Llama 3.2 1B

The objective was to transfer useful response behavior from the larger model to the smaller model.

After distillation, I quantized the student model for local inference on a computer with 8 GB RAM. This model was intended for the storytelling workflow.

### 5. Fine-Tuning for Question Answering

For the educational Q&A workflow, I explored parameter-efficient fine-tuning using LoRA/QLoRA.

I used a general question-and-answer dataset obtained from Hugging Face as the starting point for the fine-tuning workflow.

The objective was to improve the model's suitability for educational questions and answers while keeping the training and deployment workflow practical.

The storytelling and Q&A workflows were developed as separate approaches because they had different response requirements.

## System Workflow

### Storytelling

Voice input → Speech-to-text → Local distilled and quantized LLM → Generated story → Text-to-speech → Audio output

### Question Answering

Voice input → Speech-to-text → Fine-tuned LLM → Generated answer → Text-to-speech → Audio output

*These diagrams describe the intended workflows. The exact implementation and component interfaces should be documented alongside the released source code.*

## Technology Stack

- **Language:** Python
- **Local inference experiments:** Ollama
- **LLMs:** Llama 3.1 8B, Llama 3.2 3B, Llama 3.2 1B, TinyLlama
- **Model optimization:** Quantization and knowledge distillation
- **Fine-tuning:** LoRA / QLoRA
- **Training environment:** Google Colab
- **Dataset source:** Hugging Face
- **Speech interface:** STT and TTS components
- **Target environment:** Local computer with 8 GB RAM

Before releasing the implementation, the exact model checkpoints, quantization formats, speech libraries, and dependency versions will be documented.

## Engineering Challenges and Lessons Learned

- Larger models can generate useful responses but may introduce unacceptable latency on limited hardware.
- Smaller models can be easier to deploy but may not provide the desired response quality without further optimization.
- Quantization reduces model resource requirements, but its effect on response quality and speed must be measured.
- Knowledge distillation provides a way to transfer behavior from a larger teacher model to a smaller student model.
- LoRA/QLoRA offers a parameter-efficient approach to adapting a language model for a specific task.
- Integrating speech recognition, language generation, and speech synthesis introduces additional software and latency challenges.

## Evaluation

The development process included qualitative testing of response quality and practical experimentation with local inference.

Verified measurements for latency, memory usage, model size, and Q&A quality will be added when the corresponding test records are available. No unverified benchmark values are reported here.


## Project Status

Experimental development completed across local LLM testing, model optimization, storytelling, and Q&A fine-tuning. The publicly available implementation and reproducibility instructions will depend on which materials are authorized for release.

## Author

**Muhammad Ammar**

AI/ML Engineering | Generative AI | Large Language Models | Edge AI
