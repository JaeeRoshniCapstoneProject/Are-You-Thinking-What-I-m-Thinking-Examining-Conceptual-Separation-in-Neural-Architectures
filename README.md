# Are You Thinking What I'm Thinking? — Conceptual Separation in Neural Architectures

Code and data accompanying our work on **conceptual separation** in convolutional neural networks (CNNs) and large language models (LLMs). We study whether examples of the same concept form coherent internal representations, whether related concepts are represented more similarly than unrelated concepts, and how this structure changes for unfamiliar, shifted, or ambiguous concepts.

## Repository structure

```text
.
├── cnns/
│   ├── Experiment_1_Cats_Dogs_Cars.ipynb
│   ├── Experiment_2_Rangoli_Microscopy.ipynb
│   └── Experiment_3_Pose_Roads.ipynb
├── llms/
│   ├── bert_large/
│   │   ├── bert_wo_prompt.ipynb
│   │   ├── bert_w_prompt.ipynb
│   │   ├── bert_compare_prompted.ipynb
│   │   └── bert_second_moment_analysis.ipynb
│   └── gpt_oss_20b/
│       ├── sentences_without_prompt.ipynb
│       ├── sentences_with_prompt.ipynb
│       ├── compare_prompted.ipynb
│       └── second_moment_analysis.ipynb
├── data/
│   ├── README.md
│   └── llm_data/
├── results/                  # generated locally; ignored by git
├── requirements.txt
└── README.md
```

## Experiments

### CNNs

We extract activations from the layer immediately before the classifier in ImageNet-pretrained **ResNet-50** (2048 dimensions) and **MobileNetV2** (1280 dimensions). The notebooks cover:

1. **In-distribution concept separation:** cats, dogs, and cars.
2. **Unfamiliar visual concepts:** Rangoli and electron-microscopy images.
3. **Within-class variation:** sleeping vs. standing cats and Indian vs. Turkish road scenes.

The analysis includes PCA, Euclidean distance, cosine distance, Mahalanobis distance, and KL-divergence-based activation-blueprint comparisons.

### LLMs

We analyse final-layer, mean-pooled sentence representations from **BERT-large-uncased** and **GPT-OSS-20B** for three concept pairs:

- Computer Science vs. Shakespeare
- Information Security vs. Theory of Computation
- Hate Speech vs. No-Hate Speech

The notebooks contain first-moment geometric analyses, per-neuron KL divergence, prompted vs. unprompted comparisons, and second-moment covariance analyses using the normalised Frobenius norm and permutation tests.

## Setup

Python 3.10+ is recommended.

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\\Scripts\\activate
pip install -r requirements.txt
```

The BERT notebooks can run on a standard CUDA-capable GPU. **GPT-OSS-20B is substantially more demanding** and is best run on a high-memory GPU (for example, an A100-class environment). Model downloads are handled through Hugging Face. If authentication is required in your environment, run:

```bash
huggingface-cli login
```

No access token is stored in this repository.

## Data

The three LLM spreadsheets used by the notebooks are included under `data/llm_data/`. Image datasets are **not redistributed** here; download them from their original sources and arrange them according to `data/README.md`.

By default, the CNN notebooks look for images under:

```text
data/cnn_images/
```

You can instead point the notebooks to an external location without editing code:

```bash
export CNN_DATA_ROOT=/path/to/cnn_images
export POSE_DATA_ROOT=/path/to/pose_images
export ROAD_DATA_ROOT=/path/to/road_images
```

## Reproducing the paper analyses

Run notebooks top-to-bottom in the following order when dependencies exist between outputs:

| Paper analysis | Notebook |
|---|---|
| CNN: cats, dogs, cars; PCA/distances/KL | `cnns/Experiment_1_Cats_Dogs_Cars.ipynb` |
| CNN: Rangoli and microscopy coherence | `cnns/Experiment_2_Rangoli_Microscopy.ipynb` |
| CNN: cat pose and road domain shift | `cnns/Experiment_3_Pose_Roads.ipynb` |
| BERT unprompted embeddings and first-moment analysis | `llms/bert_large/bert_wo_prompt.ipynb` |
| BERT prompted embeddings | `llms/bert_large/bert_w_prompt.ipynb` |
| BERT prompted/unprompted comparison | `llms/bert_large/bert_compare_prompted.ipynb` |
| BERT covariance analysis | `llms/bert_large/bert_second_moment_analysis.ipynb` |
| GPT-OSS-20B unprompted embeddings and first-moment analysis | `llms/gpt_oss_20b/sentences_without_prompt.ipynb` |
| GPT-OSS-20B prompted embeddings | `llms/gpt_oss_20b/sentences_with_prompt.ipynb` |
| GPT prompted/unprompted comparison | `llms/gpt_oss_20b/compare_prompted.ipynb` |
| GPT covariance analysis | `llms/gpt_oss_20b/second_moment_analysis.ipynb` |

Generated embeddings, plots, reports, and intermediate results are written under `results/` and are intentionally excluded from version control.

## Reproducibility notes

- Repository notebooks use relative paths rather than machine-specific paths.
- Random seeds are set to `42` in the notebook setup cells where applicable.
- Notebook outputs are cleared in the committed versions to keep the repository lightweight and avoid stale outputs being mistaken for freshly reproduced results.
- Pretrained model weights may change only if upstream model repositories change; for archival reproducibility, record the exact package and model revisions used for the final camera-ready run.
- The image datasets are third-party resources and remain subject to their original licenses and terms.

## Dataset sources

See `data/README.md` for dataset links, expected folder structure, and attribution details.

## Authors

Jaee Ponde and Roshni Agarwal  
Supervisor: Prof. Subhashis Banerjee

## Citation

If you use this code, please cite the accompanying paper. A formal citation can be added here once the workshop proceedings entry is available.
