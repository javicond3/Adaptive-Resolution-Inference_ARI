# Adaptive Resolution Inference (ARI): Energy Efficient Machine Learning for the Internet of Things

## Overview

The implementation of Machine Learning (ML) in Internet of Things (IoT) devices poses significant operational challenges due to limited energy and computation resources. While techniques like quantization and pruning reduce energy consumption, they often come at the cost of model accuracy.

**Adaptive Resolution Inference (ARI)** is a novel approach that optimizes the tradeoff between energy dissipation and model performance. The core principle of ARI is to:
1. **Run initial inference with reduced precision** (quantization or Stochastic Computing).
2. **Evaluate the margin** of the output scores over the decision threshold.
3. **Conditionally recompute**: If the margin is sufficient, the result is deemed reliable. If the margin is too small (indicating uncertainty due to quantization noise), the inference is re-run using the full-precision model.

This approach ensures that the vast majority of inferences are executed using the low-energy, reduced-precision model, while only a small fraction of "uncertain" inputs require the full model. As a result, ARI achieves significant energy savings (between 40% and 85%) without degrading the overall model performance.

## Repository Structure

The repository is organized into three main directories containing the visual results of our experiments across different models (CNN, MLP), datasets (MNIST, Fashion-MNIST, SVHN, CIFAR-10), and precision configurations (FP16, Stochastic Computing with varying bit-widths).

### 1. `Margin analysis/`
This folder contains plots analyzing the margin over the decision threshold for different configurations. 
- **Contents**: Files named like `[model]_[dataset]_FP16_SCbits[X].png` (e.g., `cnn_cifar10_FP16_SCbits10.png`).
- **Description**: These plots illustrate how the quantization process affects the inference scores and demonstrate the distribution of margins. They help visualize why a specific margin threshold is effective at distinguishing between reliable low-precision predictions and those that require full-precision recomputation.

### 2. `Recomputation/`
This folder contains plots detailing the recomputation rates.
- **Contents**: Files named like `[model]_[dataset]_FP16_recomputation.png` (e.g., `mlp_mnist_FP16_recomputation.png`).
- **Description**: These graphs show the fraction of inferences that fall below the confidence margin and thus require recomputation with the full-precision model. Lower recomputation rates directly correlate with higher energy savings.

### 3. `Threshold/`
This folder contains comparative analyses across different threshold values and bit-widths.
- **Contents**: Files named like `[model]_[dataset]_FP16_compare_bits.png` (e.g., `cnn_svhn_FP16_compare_bits.png`).
- **Description**: These plots compare the performance and energy tradeoffs when varying the decision threshold and the number of bits used in the reduced-precision model. They are crucial for determining the optimal configuration that maximizes energy efficiency while maintaining accuracy.

## Experimental Setup

The ARI methodology was evaluated using the following configurations:
- **Models**: Multi-Layer Perceptrons (MLP) and Convolutional Neural Networks (CNN).
- **Datasets**: MNIST, Fashion-MNIST, SVHN, and CIFAR-10.
- **Implementations**: 
  - Floating-point (FP16 as the full-precision baseline).
  - Stochastic Computing (SC) with varying bit-widths (e.g., 6 to 12 bits) for the reduced-precision inferences.

## Citation

If you use this work or find it helpful, please cite the original paper:

```bibtex
@article{wang2023adaptive,
  title={Adaptive Resolution Inference (ARI): Energy Efficient Machine Learning for the Internet of Things},
  author={Wang, Ziheng and Reviriego, Pedro and Niknia, Farzad and Conde, Javier and Liu, Shanshan and Lombardi, Fabrizio},
  journal={IEEE Internet of Things Journal},
  year={2023},
  doi={10.1109/JIOT.2023.3339623},
  publisher={IEEE}
}
```
