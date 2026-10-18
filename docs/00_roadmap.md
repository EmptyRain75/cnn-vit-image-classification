# Project Roadmap

Status: planning and repository initialization complete; implementations and training pending.

This continues the [MNIST project](https://github.com/EmptyRain75/mnist-ai-classifier). Its basic CNN and ViT provide conceptual starting points. See the [README](../README.md) for scope and the [experiment protocol](01_experiment_protocol.md) for evaluation rules.

## Guiding questions

For every change: what problem motivates it, which module changes, what remains reusable, and what evidence supports the conclusion?

The conceptual modules are data, preprocessing, input representation, feature processing, classifier, loss, optimization, and evaluation. A conceptual module need not occupy a separate file.

## Stage 0 — Setup and protocol

- [x] Create repository
- [x] Record learning scope, workflow, and milestones
- [x] Draft the initial experiment protocol
- [ ] Inspect CIFAR-10 and implement the saved split
- [ ] Run a timing/memory pilot and set the first study budget
- [ ] Record the validated environment and dependencies

CIFAR-10 is the starting dataset. The second dataset, exact model sizes, training durations, and total compute budget remain open until pilots provide evidence.

## Stage 1 — CNN baseline

- [ ] Build a modular CIFAR-10 notebook with RGB examples and class counts
- [ ] Create separate training and evaluation transforms
- [ ] Trace tensor shapes and count parameters
- [ ] Train a basic CNN and plot training/validation curves
- [ ] Select a checkpoint using validation loss
- [ ] Record held-out evaluation, confusion matrix, and example errors
- [ ] Extract clean data, training, checkpoint, and evaluation helpers
- [ ] Document architecture and observations

Deliverable: an executed baseline notebook and a reproducible reference configuration.

## Stage 2 — CNN training studies

Study BatchNorm2d axes, learned scale/shift, running statistics, and train/eval behavior; inverted dropout; augmentation; weight decay; optimizer and learning-rate scheduling.

- [ ] Baseline versus BatchNorm
- [ ] Dropout comparison with a declared insertion point and rate
- [ ] Basic augmentation comparison
- [ ] Focused weight-decay and optimizer/scheduler studies
- [ ] Inspect convergence, overfitting, and selected checkpoints
- [ ] Combine promising settings and describe interactions

Start with one main change per study. Do not imply dropout or BatchNorm must improve every configuration. Distinguish input normalization from internal normalization.

## Stage 3 — Deeper CNNs and ResNet

- [ ] Compare shallow and deeper plain CNNs
- [ ] Explain degradation using training behavior, separately from overfitting
- [ ] Implement identity and projection shortcuts
- [ ] Implement basic residual blocks and explain bottleneck blocks
- [ ] Assemble a small ResNet and inspect stage shapes
- [ ] Compare a plain/residual pair with aligned depth and widths where feasible
- [ ] Inspect layerwise gradients alongside training curves
- [ ] Document additions, limitations, and results

Gradient diagnostics are evidence about the measured model and batches, not proof of the only cause of a performance difference.

## Stage 4 — Supporting CNN architecture studies

Historical context: LeNet/AlexNet/ZFNet; VGG's stacked small filters; Inception's parallel branches and channel reduction.

Hands-on block studies:
- [ ] DenseNet: concatenation, growth rate, bottlenecks, transition layers
- [ ] Implement a small dense block/network
- [ ] Grouped, depthwise, and pointwise convolution
- [ ] Compare standard and depthwise-separable parameter/operation counts
- [ ] MobileNetV2-style expansion, projection, and inverted residual blocks
- [ ] Explain parameter count versus activation memory and measured speed

These are supporting studies; exhaustive training of every historical architecture is not required.

## Stage 5 — ConvNeXt

- [ ] Separate training-recipe modernization from architecture changes
- [ ] Study patchifying stems and hierarchical stage design
- [ ] Study depthwise convolution, inverted bottlenecks, and larger kernels
- [ ] Study GELU, channel-wise LayerNorm, and separate downsampling
- [ ] Explain layer scale and stochastic depth in the canonical design
- [ ] Implement a small ConvNeXt-style model with an explicit deviation list
- [ ] Select a few ablations within the pilot-based budget
- [ ] Evaluate the combined configuration and document conclusions

Candidate ablations: kernel size, activation, normalization, and convolution type. Define tensor layout and normalization axes explicitly. Do not claim to reproduce the full paper through a few small-dataset runs.

## Stage 6 — ViT baseline

- [ ] Adapt the prior ViT to RGB images
- [ ] Review patch embedding, positional information, CLS token, pre-norm, attention, and FFN
- [ ] Trace patch size → token count → attention-memory implications
- [ ] Train a small baseline using the shared evaluation protocol
- [ ] Select focused patch-size/width/depth studies
- [ ] Document optimization, errors, and compute limitations

Do not infer a general architecture ranking from one training recipe or seed.

## Stage 7 — Swin

- [ ] Study local window attention and window partition/reversal
- [ ] Implement relative position bias
- [ ] Implement shifted windows and attention masking
- [ ] Explain padding and boundary handling
- [ ] Implement patch merging and hierarchical stages
- [ ] Assemble a small Swin-style classifier
- [ ] Compare regular-window-only and alternating regular/shifted-window models
- [ ] Trace shapes and document deviations from canonical Swin

Use an input resolution and window size that allow meaningful multiple-window stages. Do not mechanically transplant a standard high-resolution configuration onto 32×32 inputs.

## Stage 8 — Application dataset and transfer learning

- [ ] Select and verify a second natural-image dataset, access terms, labels, and splits
- [ ] Check duplicates/group leakage and class balance
- [ ] Select library CNN and Transformer checkpoints with recorded pretraining sources
- [ ] Use checkpoint-appropriate preprocessing
- [ ] Train classifier heads over frozen backbones
- [ ] Compare partial and full fine-tuning where feasible
- [ ] Report pretraining and resolution separately from scratch-trained studies

Course weather/scene tasks are candidate applications, not a finalized dataset choice. Confirm dataset provenance and availability before adopting either.

## Stage 9 — Final comparison

- [ ] Repeat shortlisted configurations across seeds where budget permits
- [ ] Summarize accuracy, loss, parameters, runtime, and measured inference behavior
- [ ] Compare classwise errors and examples
- [ ] Separate scratch-trained and pretrained results
- [ ] Distinguish controlled ablations from best-configuration comparisons
- [ ] State tuning, data, compute, and measurement limitations
- [ ] Write the final architectural and experimental synthesis
- [ ] Verify links, outputs, dependencies, and reproduction instructions

## Completion standard and workflow

For a major model, completion means an explained notebook with preserved outputs, validated runnable source, mathematics/architecture notes, a recorded configuration, results, and conclusions.

Notebook first → clean source → documentation → focused experiments. Later notebooks reuse stable source helpers. Supporting block studies can finish with shape checks, analytical counts, and a small demonstration rather than a full training campaign.

RNN, LSTM, and GRU remain outside the core scope. Detection, segmentation, training ImageNet-scale models from scratch, and exhaustive hyperparameter searches are optional future projects.
