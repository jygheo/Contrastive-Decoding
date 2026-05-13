Below are the instructions to obtain the exact datasets used in our experiments.

## 1. Text Generation Datasets

We evaluated our text models across three distinct domains: news, Wikipedia, and stories.

* **Wikinews:** * Source: Hugging Face (`izumi-lab/wikinews-en-20230728`)
  * Retrieval: `load_dataset("izumi-lab/wikinews-en-20230728", split="train")`
* **WikiText-103:** * Source: Hugging Face (`Salesforce/wikitext`)
  * Retrieval: `load_dataset("Salesforce/wikitext", "wikitext-103-raw-v1", split="train")`
* **Project Gutenberg:** * Source: [Project Gutenberg Dataset Archive](https://shibamoulilahiri.github.io/gutenberg_dataset.html)
  * Note: For local reproduction, download the `.txt` files from the archive and place them inside a `data/Gutenberg/` subdirectory. Our text generation scripts are configured to read `.txt` files directly from this folder path.

## 2. Music Generation Dataset

We extended Contrastive Decoding to the audio domain using the GTZAN dataset for genre-conditioned music generation.

* **GTZAN:**
  * Source: Hugging Face (`sanchit-gandhi/gtzan`)
  * Retrieval: `load_dataset("sanchit-gandhi/gtzan", split="train")`

## Reproduction Quick-Start

If you are running the Jupyter Notebooks provided in the `code/` directory (e.g., `music_generation.ipynb` or `text_generation.ipynb`), you do not need to manually download the Hugging Face datasets. The scripts are already configured to stream and parse the data directly via the `datasets` library:

```python
from datasets import load_dataset

# Example: Loading GTZAN audio samples
gtzan_samples = load_dataset("sanchit-gandhi/gtzan", split="train", streaming=True)
