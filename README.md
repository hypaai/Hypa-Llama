<div align="center">

# Hypa Llama

**Hypa Intelligence's open research repository for fine-tuning Llama into a multilingual, tool-aware assistant for low-resource and underrepresented languages.**

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)
[![Hugging Face](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-hypaai-yellow)](https://huggingface.co/hypaai)
[![Model](https://img.shields.io/badge/Model-Hypa--Llama3.1%208B-blue)](https://huggingface.co/hypaai/Hypa-Llama3.1-8b-SFT)
[![Blog post](https://img.shields.io/badge/Read-Blog%20Post-purple)](https://hypa-intelligence.hashnode.dev/tuning-llama-3-1-for-multilingual-dictionary-translation-and-tool-aware-language-understanding)

</div>

---

## About

Hypa Llama is the home for **Hypa Intelligence** research on adapting Meta's Llama family into a genuinely useful multilingual assistant for **low-resource and underrepresented languages**, not only one region or language family. The first release in this repository is **Hypa-Llama3.1 8B**, a supervised fine-tune of a prior Hypa Llama checkpoint aimed at **multilingual dictionary lookup, translation, and tool-aware language understanding** across seventeen languages, including twelve languages of Nigeria alongside English, French, and Spanish.

We believe multilingualism is the most underrated alignment problem in AI. A model that cannot communicate with a Yoruba farmer, a Hausa journalist, an Igbo student, an Annang grandmother, or an Idoma trader is not actually **general-purpose** for **underrepresented languages** more broadly. It is an Anglophone assistant with party tricks. Every time the field pushes the frontier without bringing **low-resource and underrepresented** languages along, we widen that gap. We think that is a problem worth working on directly, in the open.

This repository will host the full body of work as it grows. The first project (Hypa-Llama3.1 8B) is here today. Future projects will land as peer subfolders so the trajectory of the work stays visible and reproducible.

## Repository structure (current)

```
Hypa-Llama/
├── Hypa-Llama3.1-8b/
│   └── notebooks/
│       └── Hypa_Llama3_1_(8B)_Unsloth.ipynb
├── .gitignore
└── README.md
```

## Hypa-Llama3.1 8B at a glance

A supervised fine-tune of a prior Hypa Llama 3 checkpoint for multilingual translation, dictionary tasks, language detection, and related instruction-following, consistent with the **tool-aware, multilingual** focus described in our public write-up.

| Item | Value |
|---|---|
| **Base model** | [hypaai/Hypa_Llama3.2-8b-SFT-2025-12-20_II-16bit](https://huggingface.co/hypaai/Hypa_Llama3.2-8b-SFT-2025-12-20_II-16bit) |
| **Method** | LoRA SFT (r=256, alpha=256) via Unsloth + TRL |
| **Context length** | 2,048 tokens (RoPE scaling to 131,072) |
| **Optimizer** | AdamW 8-bit, lr 1e-4, cosine schedule |
| **Batch / accum** | 16 × 2 (effective batch 32) |
| **Epochs** | 1 |
| **Dataset** | [hypaai/Hypa-Text-10k](https://huggingface.co/datasets/hypaai/Hypa-Text-10k) |
| **Languages (this release)** | 17 (14 in Nigeria + English, French, Spanish) |
| **License** | Apache 2.0 |

### Languages covered

English, Annang (ann), Efik (efi), Ebira (ebi), Eggon (ego), Spanish (es), French (fr), Hausa (ha), Ibibio (ibb), Idoma (idm), Igala (igl), Igbo (ig), Nupe (nup), Pidgin (pg), Tiv (tiv), Urhobo (urh), Yoruba (yo).

Several of these languages, including Annang, Ebira, Eggon, Idoma, Igala, Nupe, and Urhobo, have either never been formally represented in a large-scale fine-tuning corpus before, or had no settled ISO-style code at the time we needed one.

### Released artifacts

- 🤗 **Merged model (16-bit)**: [hypaai/Hypa-Llama3.1-8b-SFT](https://huggingface.co/hypaai/Hypa-Llama3.1-8b-SFT)
- 🤗 **LoRA adapter checkpoints**: [hypaai/Hypa-Llama3.1-8b-SFT-LoRAs](https://huggingface.co/hypaai/Hypa-Llama3.1-8b-SFT-LoRAs)
- 📊 **TensorBoard metrics**: [TensorBoard on HF](https://huggingface.co/hypaai/Hypa-Llama3.1-8b-SFT-LoRAs/tensorboard)
- 📦 **Training data (public subset)**: [hypaai/Hypa-Text-10k](https://huggingface.co/datasets/hypaai/Hypa-Text-10k) - see also [all Hypa datasets & models](https://huggingface.co/hypaai)

## Blog post

The full write-up (model design, training setup, multilingual evaluation, and lessons learned) is published at:

- **[Tuning Llama 3.1 for multilingual dictionary, translation, and tool-aware language understanding](https://hypa-intelligence.hashnode.dev/tuning-llama-3-1-for-multilingual-dictionary-translation-and-tool-aware-language-understanding)** - Hashnode (canonical)

We publish results and lessons openly because that transparency is the price of admission to leading on multilingual AI. Other labs bury this. We do not.

## Roadmap

This repository is intended to grow. Each future project will land as a peer subfolder so the full arc of the research stays visible and reproducible:

- **Future Llama iterations.** v2 of Hypa-Llama3.1 8B with hyperparameter improvements, then larger Llama variants as Meta releases them.
- **From-scratch training.** Pretraining experiments with multilingual-first data mixes, including tokenizer ablations tuned for **orthographies and language families underrepresented** in large-scale corpora.
- **Audio modalities.** ASR and audio-to-text translation fine-tunes.
- **Vision modalities.** Image-text fine-tunes for OCR and document understanding in low-resource scripts.
- **Reinforcement learning.** RLHF and DPO post-training for instruction-following quality and safety in target languages.
- **Voice output.** TTS head adaptation for a fully multilingual end-to-end voice assistant.

## Contributing

We welcome contributions from researchers, engineers, native speakers, and anyone who shares the goal of broadening AI's linguistic reach:

- **Native-speaker review.** If you speak any of our target languages, especially the smaller ones in this release (Annang, Ebira, Eggon, Idoma, Igala, Nupe, Tiv, Urhobo), or **other underrepresented languages** you want to see supported, we would love help validating model outputs and flagging errors.
- **Data contributions.** If you have access to clean parallel data, dictionaries, or transcribed speech in **underrepresented languages** (including beyond those in this release), please reach out.
- **Code and research.** Open issues, pull requests, and proposals for new experiments are all welcome.
- **Reproducing the work.** If you run our notebooks and find bugs, version-skew issues, or reproducibility gaps, please file an issue.

## Citation

If you use Hypa-Llama3.1 8B or any of the work in this repository, please cite:

```bibtex
@misc{hypaai2026hypallama318b,
  title        = {Hypa-Llama3.1 8B: A Multilingual Fine-Tune of Llama 3.1 for Underrepresented Languages},
  author       = {{Hypa Intelligence}},
  year         = {2026},
  publisher    = {Hugging Face},
  howpublished = {\url{https://huggingface.co/hypaai/Hypa-Llama3.1-8b-SFT}},
  note         = {Apache 2.0 License. Blog: \url{https://hypa-intelligence.hashnode.dev/tuning-llama-3-1-for-multilingual-dictionary-translation-and-tool-aware-language-understanding}}
}
```

## License

This repository is released under the **Apache License 2.0**.

The released model checkpoints are built on Meta's Llama 3 family and are subject to Meta's Llama 3 Community License in addition to Apache 2.0. Datasets released under the `hypaai` Hugging Face organization are subject to their individual dataset licenses, documented on each dataset page.

## Acknowledgments

- **Meta AI** for releasing Llama 3.1 openly and enabling this line of research.
- **Unsloth** for making LoRA fine-tuning dramatically faster and more memory-efficient.
- **Runpod** for reliable GPU infrastructure.
- The **language communities, speakers, and reviewers** whose texts, voices, and feedback grounded this work and keep it honest.

---

<div align="center">

**Hypa Intelligence** • [Website](https://hypaintelligence.com) • [Hugging Face](https://huggingface.co/hypaai) • [Blog / updates](https://hypaintelligence.com/updates)

*Multilingualism is not a feature. It is a prerequisite for AI that represents all of us.*

</div>
