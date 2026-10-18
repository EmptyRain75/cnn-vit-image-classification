# CNN and Vision Transformer Image Classification

A personal learning project continuing [MNIST Image Classification](https://github.com/EmptyRain75/mnist-ai-classifier), with modular implementations and controlled studies of deeper CNNs, ConvNeXt, ViT, and Swin.

The goal is to understand what motivates each architectural change, which modules are reused or replaced, and how architecture and training choices affect learning. Higher accuracy is one outcome; explaining the model and its experimental behavior is the main purpose.

## Learning progression

- CNN baseline → training studies → ResNet → supporting DenseNet/MobileNet block studies → ConvNeXt.
- ViT baseline → local window attention → shifted windows and hierarchy → Swin.
- Pretrained models → frozen-backbone classification → fine-tuning → final comparison.

These are learning paths, not a guarantee that every later model performs better.

## Scope

CIFAR-10 is the initial dataset for learning implementations and controlled experiments. A second natural-image dataset is planned for practical application and transfer learning; its identity and split protocol are not yet selected.

Small custom learning implementations will be distinguished from canonical library models. Reduced ConvNeXt-style and Swin-style models are not reproductions of their published ImageNet results. Pretrained runs will be reported separately from training from scratch.

Historical models provide context. Full training studies focus on selected models rather than every architecture in the reference slides. RNN, LSTM, and GRU are outside the core vision scope.

## Repository areas

| Path | Purpose |
|---|---|
| [docs/00_roadmap.md](docs/00_roadmap.md) | Stages, learning goals, and completion checklist |
| [docs/01_experiment_protocol.md](docs/01_experiment_protocol.md) | Initial data, selection, comparison, and recording rules |
| [notebooks/](notebooks/) | Module-by-module explanations, code, outputs, and observations |
| [src/](src/) | Reusable executable code extracted after notebook validation |
| [configs/](configs/) | Reproducible settings for implemented runs |
| [experiments/](experiments/) | Focused experiment plans and analysis |
| [results/](results/) | Small metric files, figures, and conclusions |

## Development workflow

Study the ideas → complete a modular learning notebook → validate shapes and behavior → extract clean source code → document mathematics and architecture → conduct focused experiments → write conclusions.

Each notebook starts with its objective and pipeline, then explains each module immediately before its code. Once shared helpers are stable, later notebooks import them from source to avoid divergent training loops.

## Current progress

- [x] Create repository and initialize project documentation
- [x] Define learning scope and initial experiment protocol
- [ ] Build and execute the first CIFAR-10 CNN baseline notebook
- [ ] Extract and validate the shared training/evaluation pipeline
- [ ] Complete CNN training studies
- [ ] Implement and study ResNet
- [ ] Complete supporting DenseNet/MobileNet block studies
- [ ] Implement and study a small ConvNeXt-style model
- [ ] Adapt and study the ViT baseline
- [ ] Implement and study a small Swin-style model
- [ ] Select a second dataset and complete transfer-learning studies
- [ ] Repeat shortlisted runs and write the final comparison

## Running the project

Implementation has not started. There are no runnable model notebooks, training commands, or recorded results yet. Google Colab is the initial execution environment. Dependencies and exact runtime versions will be recorded when the first notebook is validated.

The next deliverable is `notebooks/01_cifar10_cnn_baseline.ipynb`: data inspection, a saved split, preprocessing, a basic CNN, training/validation, checkpoint selection, and evaluation.

## References

The learning plan draws on AI VIET NAM AIO2025 materials on BatchNorm and skip connections, classic-to-modern CNN architectures, and ResNet/DenseNet exercises. Course materials are reference inputs and are not redistributed here.

Primary architecture references:
- [ResNet](https://arxiv.org/abs/1512.03385)
- [DenseNet](https://arxiv.org/abs/1608.06993)
- [MobileNet](https://arxiv.org/abs/1704.04861)
- [MobileNetV2](https://arxiv.org/abs/1801.04381)
- [ViT](https://arxiv.org/abs/2010.11929)
- [Swin Transformer](https://arxiv.org/abs/2103.14030)
- [ConvNeXt](https://arxiv.org/abs/2201.03545)
