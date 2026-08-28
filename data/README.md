# Data setup

The repository contains the small text spreadsheets used for the LLM experiments, but does **not** redistribute the image datasets. Download image data from the original sources below and organise it as shown here.

## LLM data included in this repository

```text
data/llm_data/
├── Sentences.xlsx
├── comp_sci_sentences.xlsx
└── Hate vs Not-Hate.xlsx
```

## CNN image sources

- **Cats and dogs:** Melvin Paul Jacob, *Cat Dog Dataset* — https://www.kaggle.com/datasets/melvinpauljacob/cat-dog-dataset
- **Cars:** Patrick Rondeau, *The Car Connection Picture Dataset* — https://www.kaggle.com/datasets/prondeau/the-car-connection-picture-dataset
- **Rangoli:** Siddharth Magesh, *Rangoli Detection Dataset* — https://www.kaggle.com/datasets/siddharthmagesh/rangoli-detection-dataset
- **Microscopy:** Batuhan Yildirim, *Electron Microscopy Particle Segmentation* — https://www.kaggle.com/datasets/batuhanyil/electron-microscopy-particle-segmentationd
- **Indian roads:** Mitanshu Chakrawarty, *New IDD Dataset* — https://www.kaggle.com/datasets/mitanshuchakrawarty/new-idd-dataset
- **Turkish roads:** Yusuf Berk Sardoğan, *Traffic Detection Project* — https://www.kaggle.com/datasets/yusufberksardoan/traffic-detection-project/data

Please consult the original dataset pages for licensing and citation requirements.

## Expected directory layout

The default folder layout expected by the cleaned notebooks is:

```text
data/cnn_images/
├── Cats/
├── Dogs/
├── Cars/
├── Rangoli/
├── Microscopy/
├── Pose/
│   ├── Sleeping/
│   └── Standing/
└── Roads/
    ├── India/
    └── Turkey/
```

If you keep the datasets elsewhere, set environment variables before launching Jupyter:

```bash
export CNN_DATA_ROOT=/path/to/cnn_images
export POSE_DATA_ROOT=/path/to/pose_root
export ROAD_DATA_ROOT=/path/to/roads_root
```

The experiments use fixed-size subsets (typically 100 reference/test examples as described in the paper). The notebooks sort filenames before slicing so that repeated runs over the same folder contents use the same subset.
