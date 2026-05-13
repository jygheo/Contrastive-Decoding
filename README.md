# Reproducing and Extending Contrastive Decoding: From Text to Music Generation

**Authors:** Yoongyu Heo, Winnie Liu, Bradley Lasker, Timothy Nguyen

## 1. Introduction
This repository contains our reproduction and novel extension on the paper *Contrastive Decoding: Open-ended Text Generation as Optimization* (Li et al., 2022). Contrastive Decoding (CD) is an inference-time method that improves generation quality by selecting tokens an "expert" model favors while penalizing tokens a smaller "amateur" model predicts.

## 2. Chosen Result
We aimed to reproduce the original baseline evaluations (Table 1) and model scaling behaviors (Figure 1) to validate CD's effectiveness and test the mechanistic hypothesis that a larger expert-amateur size gap produces a stronger contrastive signal. 

## 3. GitHub Contents
* `code/`: Jupyter notebooks for text and music generation/evaluation.
* `data/`: Instructions for obtaining the WikiText, Wikinews, Gutenberg, and GTZAN datasets.
* `results/`: Generation logs (`.jsonl`), evaluation tables, and generated figures.
* `report/`: Our final 2-page project summary report.
* `poster/`: Our academic poster from the in-class presentation.

## 4. Re-implementation Details
We evaluated CD on text (GPT-2, OPT-6.7B, Qwen1.5-7B) and extended it to audio using MusicGen. Due to architectural incompatibilities with MusicGen's EnCodec structure, we modified the decoding approach by replacing beam search with top-k sampling over the CD scores.

## 5. Reproduction Steps
To re-implement our findings in a local environment:
1. Clone this repository and navigate to the `code/` directory.
2. Install dependencies: `pip install torch transformers datasets torchaudio nltk mauve-text`.
3. Run `text_generation.ipynb` and `music_generation.ipynb` to generate the `.jsonl` data logs, followed by their respective `_eval.ipynb` scripts to calculate metrics.
* **Resources Needed:** A GPU (T4, A100, or equivalent) is required to run inference on the expert models.

## 6. Results/Insights
CD dominated text baselines across Coherence and Diversity, though we found metrics are highly sensitive to the amateur temperature hyperparameter. Furthermore, CD successfully transferred to audio generation; performance peaked when providing the amateur model with an "opposing-genre" prompt and applying CD exclusively to finer-detail codebooks (1-3).

### Audio Generation Highlights
Notice how the CD samples utilizing "opposing-genre" amateur prompts suppress generic features and sharpen the target genre compared to the baselines.

**Target Genre "Reggae"**
* **Baseline (Top-k):** https://github.com/user-attachments/assets/17058084-73e0-48f1-b365-2c2423a93d90
* **Contrastive Decoding (Amateur Prompt: "Classical"):** https://github.com/user-attachments/assets/bf79a0ba-1067-4df8-a858-3f858cb10ba5

**Target Genre "Disco"**
* **Baseline (Top-k):** https://github.com/user-attachments/assets/748b8e71-83ad-468a-a8dd-c967fe5527b1
* **Contrastive Decoding (Amateur Prompt: "Funeral March"):** https://github.com/user-attachments/assets/4faee3cd-e35f-4f3a-bb9a-8f2442228d57

**Target Genre "Metal"**
* **Baseline (Top-k):** https://github.com/user-attachments/assets/0f0fa5ec-527b-4787-88e5-4d660cf35f28
* **Contrastive Decoding (Amateur Prompt: "Smooth Jazz"):** https://github.com/user-attachments/assets/06eebf3e-68b2-4f87-a402-d5103e3ed054

**Codebook Optimization**
* **CD applied to Codebooks 1-3 only:** https://github.com/user-attachments/assets/76c596f3-0f4a-4f59-857a-5b530f500aa9
  * *Note: Skipping Codebook 0 reduces the structural artifacts heard in standard generation.*

*(Note: See the `results/` folder for full metric tables and scaling heatmaps).*

## 7. Conclusion
A single underspecified hyperparameter can drastically shift the behavioral space of an NLP method, highlighting a core reproducibility challenge. However, deliberately adversarial amateur prompting provides a strong, directional contrastive signal that successfully generalizes CD from text to audio generation.

## 8. References
* Copet, J., Kreuk, F., Gat, I., Remez, T., Kant, D., Synnaeve, G., Adi, Y., & Défossez, A. (2023). Simple and controllable music generation. *arXiv preprint arXiv:2306.05284*.
* Li, X. L., Holtzman, A., Fried, D., Liang, P., Weston, J., Zettlemoyer, L., Lewis, M., & Hajishirzi, H. (2022). Contrastive decoding: Open-ended text generation as optimization. *arXiv preprint arXiv:2210.15097*.

## 9. Acknowledgements
This project was completed as part of the coursework for CS 4782 at Cornell University.
