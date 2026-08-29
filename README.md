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
│   │   ├── Experiment_1_Unprompted_Embeddings.ipynb
│   │   ├── Experiment_2_Prompted_Embeddings.ipynb
│   │   ├── Experiment_3_Prompted_vs_Unprompted.ipynb
│   │   └── Experiment_4_Second_Moment.ipynb
│   └── gpt_oss_20b/
│       ├── Experiment_1_Unprompted_Embeddings.ipynb
│       ├── Experiment_2_Prompted_Embeddings.ipynb
│       ├── Experiment_3_Prompted_vs_Unprompted.ipynb
│       └── Experiment_4_Second_Moment.ipynb
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

Each model folder has four notebooks:

1. **Unprompted embeddings:** last-layer mean-pooled sentence vectors with no task prompt, plus first-moment analyses (PCA, distances, per-neuron KL).
2. **Prompted embeddings:** the same pipeline with a concept-identifying prompt prepended to each sentence.
3. **Prompted vs. unprompted:** comparison of saved embeddings (no re-encoding).
4. **Second moment:** covariance analyses using the normalised Frobenius norm, eigenvalue spectra, Gaussian KL, and permutation tests.

Run 1 then 2 before 3 and 4.

## Setup

Python 3.10+ is recommended. Install dependencies **once** with the commands below. After that, notebooks skip `pip` if the packages are already importable, so later runs do not repeat the install. The first cell still installs from `requirements.txt` automatically if anything is missing (that first install can take several minutes because of PyTorch).

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
| BERT unprompted embeddings and first-moment analysis | `llms/bert_large/Experiment_1_Unprompted_Embeddings.ipynb` |
| BERT prompted embeddings | `llms/bert_large/Experiment_2_Prompted_Embeddings.ipynb` |
| BERT prompted/unprompted comparison | `llms/bert_large/Experiment_3_Prompted_vs_Unprompted.ipynb` |
| BERT covariance analysis | `llms/bert_large/Experiment_4_Second_Moment.ipynb` |
| GPT-OSS-20B unprompted embeddings and first-moment analysis | `llms/gpt_oss_20b/Experiment_1_Unprompted_Embeddings.ipynb` |
| GPT-OSS-20B prompted embeddings | `llms/gpt_oss_20b/Experiment_2_Prompted_Embeddings.ipynb` |
| GPT prompted/unprompted comparison | `llms/gpt_oss_20b/Experiment_3_Prompted_vs_Unprompted.ipynb` |
| GPT covariance analysis | `llms/gpt_oss_20b/Experiment_4_Second_Moment.ipynb` |

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

[NA]

## Citation

If you use this code, please cite the accompanying paper. A formal citation can be added here once the workshop proceedings entry is available.
