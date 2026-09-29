## 1. Quick Start 

### 1.1 Requirements

- Python 3.9 and a CUDA-capable GPU are recommended for evaluation.
- PyTorch with a CUDA version compatible with your system.
- Python packages used by the project include NumPy, SciPy, PyYAML, SimpleITK, scikit-image, Pillow, tqdm, and Matplotlib.
- [TIGRE](https://github.com/CERN/TIGRE) is needed for the CT projection/preprocessing scripts.

### 1.2 Data

 The current experiments use preprocessed CBCT volumes and projections. Set `dataset.root_dir` in `configs/finetune_s2.yaml` to the location of your own preprocessed data before evaluation. 

```text
dataset/
│
├── 1/
│   ├── 1.nii.gz
│   ├── projections.pickle
│   ├── projections_vis.png
│   └── blocks/
│       ├── blocks_coords.npy
│       ├── block-0.npy
│       ├── block-1.npy
│       ├── ...
│       └── block-7.npy
│
├── 2/
│   ├── 2.nii.gz
│   ├── projections.pickle
│   ├── projections_vis.png
│   └── blocks/
│       ├── blocks_coords.npy
│       ├── block-0.npy
│       ├── block-1.npy
│       ├── ...
│       └── block-7.npy
│
├── 3/
│   ├── 3.nii.gz
│   ├── projections.pickle
│   ├── projections_vis.png
│   └── blocks/
│       ├── blocks_coords.npy
│       ├── block-0.npy
│       ├── block-1.npy
│       ├── ...
│       └── block-7.npy
│
└── ...
```

The division of the training set, validation set and test set follows:

```text
train.txt
├── 1
├── 5
├── 11
└── ...
val.txt
├── 12
├── 23
└── ...
test.txt
├── ...
```

### 1.3 Trained Weights

Download the PUF-Net pre-trained and view-specific model weights from the [Releases](https://github.com/lanyadong66-star/SUF-Net/releases/tag/v1.0.0.0) page and place the downloaded `.pth` files in the `./checkpoints` directory.

### 1.4 Evaluation

With the full local project, the prepared data, and the corresponding checkpoint available, run from the project root. For the 6-view model:

```bash
python code/Infer_6v_s2.py\
  --name "6v+s2" \
  --split test \
  --cfg_path configs/finetune_s2.yaml \
  --ckpt_path "logs/6v+s2/PUF_6v_s2.pth" \
  --save_results \
  --results_dir inference_results/6-views
```

For the 8-view or 10-view model, change `--name`,  `--ckpt_path`, and `--results_dir` to the matching values. The evaluator reports PSNR and SSIM and saves predictions when `--save_results` is set.



## 2. Release

The complete source code will be released soon.
