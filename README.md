# Multi-Level Integrity Verification for Deep Neural Network Models

Reproducible research code implementing the manuscript's parameter-, representation-, and explainability-level integrity verification pipeline.

## Important research note
The manuscript specifies the framework and reported aggregate results, but does not provide exact fusion weights, decision thresholds, all attack strengths, training hyperparameters, or raw experiment records. Therefore:

- `data/reported/` contains values transcribed from the manuscript and is clearly labelled **reported, not reproduced**.
- Default values in `config/default.yaml` are explicit implementation assumptions.
- `scripts/run_demo.py` runs a deterministic end-to-end synthetic demonstration.
- `scripts/train.py` and `scripts/download_data.py` support public torchvision datasets for real experiments.

## Quick start

```bash
python -m venv .venv
# Windows: .venv\\Scripts\\activate
# Linux/macOS: source .venv/bin/activate
pip install -r requirements.txt
python scripts/run_demo.py
pytest -q
```

Outputs are written to `outputs/metrics`, `outputs/tables`, and `outputs/figures`.

## Full workflow

```bash
python scripts/download_data.py --dataset mnist
python scripts/train.py --dataset mnist --model lenet5 --epochs 2
python scripts/run_demo.py --attack weight_modification
python scripts/reproduce_reported_results.py
```

## Implemented components

- Layer-wise SHA-256 parameter fingerprints
- Activation-statistics representation fingerprints
- Linear CKA, cosine similarity, normalized Euclidean similarity
- Integrated-gradients-style input attribution fingerprints
- Correlation, SSIM-like, and IoU explanation similarities
- Weighted layer integrity fusion
- Tampered-layer localization
- Model integrity and risk scoring
- Risk-aware mitigation and re-validation
- Six deterministic tampering scenarios
- Baselines and ablation configurations
- Reported-result tables and plots

## Dataset/model mapping

- MNIST / Fashion-MNIST → LeNet-5
- CIFAR-10 → ResNet-18
- CIFAR-100 → ResNet-50
- Tiny ImageNet → DenseNet-121 or MobileNetV2

## Citation
See `CITATION.cff`.
