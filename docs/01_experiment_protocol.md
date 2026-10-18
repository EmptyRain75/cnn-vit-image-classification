# Initial Experiment Protocol

Status: specification only; no split or experiment has been executed.

## Initial dataset and splits

Use CIFAR-10's official 50,000 training and 10,000 test examples. Proposed development split: a stratified, seeded 45,000/5,000 split of the official training examples. Initial split seed: 42. Save actual indices and a dataset/version identifier so every model uses the same examples.

The official test set is held out. Use validation for configuration and checkpoint decisions. Do not repeatedly inspect test results to steer development. If the baseline receives an early test evaluation for a learning demonstration, keep subsequent tuning validation-only and disclose that test access.

Choose the second dataset and its split protocol separately. Preserve official splits when suitable; account for duplicates or related examples that could leak across splits.

## Preprocessing

The first scratch-trained CNN uses native 32×32 RGB images. Compute any normalization statistics from training examples only, without random augmentation. Reuse those statistics for validation and test.

Keep training and evaluation transforms separate. Start with deterministic preprocessing for the baseline; introduce augmentation in a declared study. Do not augment validation/test images randomly.

Later custom architectures may require adapted stems, window sizes, or resolution. Record these changes. Resizing changes compute and does not create new source-image detail. Pretrained checkpoints use their documented preprocessing, which may differ from the scratch baseline.

## Shared training contract

- Models return raw class logits for CrossEntropyLoss.
- Use model.train() for parameter updates and model.eval() with disabled gradient recording for evaluation.
- Aggregate mean loss by example count, including a smaller final batch.
- Save the best validation-loss checkpoint, including model buffers such as BatchNorm statistics.
- Record the selected epoch and associated validation accuracy; do not silently select by a different metric.
- Keep a resumable checkpoint separately when needed, including optimizer/scheduler state and random-generator state.
- Check shapes, finite outputs/losses, and whether a tiny training subset can be fitted before expensive runs.
- Record actual package versions, device, precision, and relevant deterministic settings. Seeding does not guarantee identical results on every platform.

## First pilot

Build the simplest CNN and run a short timing/memory pilot before choosing the full epoch count or study budget. Record setup/download time separately from training plus validation. Include checkpointing in timing if it is part of the measured loop, and state that boundary.

The initial pilot configuration and final baseline configuration will be committed when implemented. No accuracy target or fixed total runtime is promised yet.

## Study types

### Controlled ablation
Change one main factor and hold declared settings fixed. Align architecture, splits, initialization/seed policy, training duration, and selection procedure where applicable. Record unavoidable changes and possible interactions.

Changing batch size at fixed epochs changes the number of optimizer updates. Matching parameter counts alone does not match training cost.

### Tuned configuration comparison
Give each model a declared tuning budget and reasonable training choices. Report the search and selected configurations. This compares implemented training systems, not architecture alone.

### Transfer learning
Report pretrained runs separately from scratch runs. Record the checkpoint identifier, pretraining dataset, input transforms, frozen/trainable layers, and trainable versus total parameters. Consider overlap between pretraining data and the evaluation dataset.

## Run records

For each run retain:
- Run ID, source commit, configuration, split identifier, and random seeds.
- Dataset, resolution, preprocessing, augmentation, model variant, and architecture deviations.
- Optimizer, learning rate, batch size, duration, regularization, schedule, and precision.
- Training/validation curves, selected checkpoint epoch, validation loss/accuracy.
- Parameter counts, runtime boundaries, device, and any measured peak accelerator memory.
- Final test metrics only when the configuration is ready for held-out evaluation.
- A short observation, interpretation, limitations, and next decision.

Record inference measurements using a stated batch size, warmup, device synchronization, number of repeats, and summary statistic. Do not infer speed from parameter or FLOP counts alone.

Use one declared seed for exploration if necessary, then repeat shortlisted configurations with several seeds where feasible. Report mean and variation with the number of runs and individual results.

## Storage

Commit small configurations, split indices, CSV/JSON metrics, selected figures, and written conclusions. Do not commit raw datasets, model weights, credentials, or bulky generated outputs. Store large checkpoints externally and record their location and identity when required for reproduction.
