# Dataset
## The Code Was Written On colab But the Notebook Is Not Avaiable for Preview For Preview See The PDF
Uses LLMA to synthesize input data (OpenWeb) 

OpenWebText --> Refined Batches with LLaMA

This repository contains a dataset pipeline that takes the raw OpenWebText corpus and transforms it into refined, structured batches using a locally running LLaMA model. The goal is to generate cleaner, rephrased synthetic text that can later be used for tokenizer training or as high-quality training data for small LLMs.

📌 Overview

Input: OpenWebText dataset (.jsonl.gz)

Process:

The dataset is streamed in manageable chunks (50–500 lines per batch).

Each batch is passed into an LLaMA-based model.

The model outputs rewritten text in a clean Q/A format.

Output:

Refined batches as batch_data00001.jsonl, batch_data00002.jsonl, …

Each entry follows the format:

{"q": "<original text>", "a": "<rewritten text>"}

⚡ Motivation

Inspired by the BeyondWeb paper (DatalogyAI, 2025), which showed that synthetic datasets can make models up to 6× more efficient, this project goes one step earlier:

Instead of training only on synthetic datasets, we generate synthetic text during preprocessing, making both the tokenizer and the model training more efficient.

With these refined batches, even a 150–200M parameter MoE model can perform like a 600M–1B model, saving massive amounts of compute.

📂 Dataset Structure

raw/ → original OpenWebText files

refined/ → LLaMA outputs in batches

Example refined file:

batch_data00001.txt
batch_data00002.txt
batch_data00003.txt
...


Each .jsonl file contains 50–500 entries, depending on batch size.

🛠️ Requirements

Python 3.9+

llama.cpp
 or Hugging Face transformers

GPU with 15GB+ VRAM (Colab T4/A100 recommended)

🚀 Usage

Download OpenWebText.

Mount Google Drive (for Colab) or prepare local storage.

Run preprocessing script to create refined batches.

Refined data is saved automatically to your chosen output directory.

📊 Applications

Training a 32k synthetic tokenizer

Building lightweight 150M–200M parameter MoE models

Pretraining experiments with high-efficiency synthetic corpora
