# ByteMe-OpenAImer-SRIJAN

The given Repository consists of the outputs and the link to the notebooks of Track-1 and Track-2 prelims round of OpenAImer SRIJAN

Track-1: Supervised Contrastive Learning · Track-2: ResNet18 Model Compression

Repository README distilled from the team’s presentation. 

Team & Affiliation

Team ByteMe — BCSE UG’27, Jadavpur University
Members: Arjeesh Palai · Arko Dasgupta · Sombrata Biswas · Abhirup Pal. 

TL;DR

Track-1: Two-stage pipeline using DenseNet201 with Supervised Contrastive (SupCon) pre-training + linear evaluation. Achieved F1 0.9948, Acc 0.9936, Precision 0.9944, Recall 0.9952. Visualizations (t-SNE) show well-separated clusters post contrastive training. Other backbones tried: ResNet50, InceptionV3, InceptionResNetV2, DenseNet169. 

Track-2: Post-training L1 unstructured, weighted pruning (“lottery-ticket style”) + architecture slimming on ResNet18. Result: ~0.38 MB disk, 8.63 ms latency, 52.8% validation accuracy. Motivated layer-sensitive ~50% pruning; future work: FishLeg/second-order pruning variants. 

Why Supervised Contrastive Learning?

Without contrastive objectives, class boundaries blur; linear classifiers struggle.

SupCon pulls positives (same class) together and pushes all others away via a log-softmax over pairwise similarities; temperature τ ∈ (0,1] scales sharpness. Outcome: compact class clusters → higher accuracy with fewer epochs. 

Method (Track-1)
Architecture

Base encoder: DenseNet201 (used in both stages).

Projection head: MLP atop encoder during SupCon pre-training.

Linear head: Softmax classifier trained with cross-entropy in evaluation stage (encoder frozen).

Backprop: Full (encoder + head) during pre-training; classifier-only during evaluation. 

Pipeline

SupCon Pre-training: Image → Encoder → Projection head → SupCon loss.

Linear Evaluation: Freeze encoder → Train linear classifier on encoder features. 

Results

DenseNet201: F1 0.9948, Accuracy 0.9936, Precision 0.9944, Recall 0.9952.

t-SNE: Clear class-wise clustering after SupCon.

Other models evaluated: ResNet50, InceptionV3, InceptionResNetV2, DenseNet169. 

Method (Track-2) — ResNet18 Compression
What we pruned/compressed

Pruning: L1 unstructured, weighted (post-training; lottery-ticket-style).

Slimming: Removal of Residual Layers 2–4 and the second block of Residual Layer 1 (as per slide schematic). 

Metrics

Disk size: ~0.38 MB

Latency: 8.63 ms

Validation accuracy: 52.8% 

Why ~50% pruning?

Preserves critical features in sensitive layers.

Good sparsity/utility trade-off; reduces overfitting risk.

Efficient compression with minimal drop when done layer-sensitively. 

Scope for Improvement

Layer-Sensitive Pruning: Adapt pruning ratios per-layer by impact.

FishLeg / FLS: Learn a compact approximation to the inverse Fisher to get second-order-aware saliency; supports unstructured and 2:4 semi-structured pruning with tensor factorization + preconditioning. 

Reproducing (High-Level Guide)

The slides describe the approach and results; wire up your codebase accordingly.

Environment

Deep learning stack (e.g., PyTorch + torchvision), metric tooling, t-SNE plotting.

SupCon Pre-training

Use DenseNet201 encoder + MLP projection head.

Train with Supervised Contrastive Loss (temperature τ).

Save encoder weights.

Linear Evaluation

Freeze encoder, attach a linear classifier, train with cross-entropy.

Report F1/Acc/Prec/Rec + t-SNE embeddings.

Compression (Track-2)

Apply L1 unstructured weighted pruning to ResNet18.

Optionally slim residual layers/blocks per slide schematic.

Measure model size, latency, validation accuracy.

Tip: For next iterations, prototype layer-sensitive ratios and evaluate FishLeg-style second-order pruning for better accuracy-at-sparsity
