# DEEP-LEARNING-APPROACHES-FOR-MUSHROOM-TOXICITY-CLASSIFICATION
An image-based research project that classifies mushroom sporocarp
(fruiting-body) images into **Edible** and **Poisonous** categories. The
project compares ConvNeXt models, a deep-feature/SVM weighted ensemble,
and a ConvNeXt--Swin hybrid architecture.

> **Safety notice:** This project is for academic and research purposes
> only. Its predictions are experimental and must never be used to
> decide whether a wild mushroom is safe to eat. Do not consume a
> mushroom based on this model's output. Correct identification requires
> qualified expertise and may require evidence beyond an image.

## Project Overview

Mushrooms can have visually similar appearances despite differing
toxicity. This project investigates deep-learning methods that learn
visual representations from mushroom images and perform binary
classification.

### Models

  -----------------------------------------------------------------------
  Model                               Approach
  ----------------------------------- -----------------------------------
  ConvNeXt-Tiny                       ImageNet-pretrained ConvNeXt
                                      fine-tuned for two classes

  ConvNeXt-Small                      ImageNet-pretrained ConvNeXt
                                      fine-tuned for two classes

  Weighted Ensemble                   EfficientNet-B3, ResNeSt50d and
                                      Swin-Tiny feature extractors;
                                      individual SVM classifiers;
                                      weighted probability aggregation

  Conv--Swin Hybrid                   ConvNeXt local features and Swin
                                      Transformer global-context features
                                      fused by concatenation, followed by
                                      fully connected layers and a
                                      Softmax classifier
  -----------------------------------------------------------------------

## Dataset

The research dataset contains **3,401 mushroom images**:

-   **Edible:** 1,181 images
-   **Poisonous:** 2,220 images

Images were collected using the iNaturalist API and organized into two
classes. The paper reports a split of **70% training, 15% validation and
15% testing**.

Training-time augmentation described in the paper includes random
flipping, random rotation, RandAugment and MixUp. Images are resized and
normalized before being passed to the models.

## Reported Results

The following are the best final accuracies reported in the project
paper:

  Model                   Accuracy
  ------------------- ------------
  ConvNeXt-Tiny             89.32%
  ConvNeXt-Small            90.70%
  Weighted Ensemble         88.64%
  Conv--Swin Hybrid     **93.54%**

The Conv--Swin Hybrid achieved the highest reported accuracy. The paper
also reports precision, recall, F1-score and confusion-matrix results
for each approach. Evaluation support counts differ between the reported
model results; consult the paper's result tables when comparing detailed
class-wise metrics.

## Methodology

1.  Collect and label mushroom sporocarp images.
2.  Preprocess and augment the training images.
3.  Fine-tune ConvNeXt-Tiny and ConvNeXt-Small using ImageNet-pretrained
    weights.
4.  Extract deep features using EfficientNet-B3, ResNeSt50d and
    Swin-Tiny, train SVM classifiers and aggregate their probability
    outputs using validation-performance-based weights.
5.  Fuse ConvNeXt and Swin Transformer features in the Conv--Swin hybrid
    model.
6.  Evaluate using accuracy, precision, recall, F1-score and confusion
    matrices.

The paper describes PyTorch and GPU-based model training. It also
presents a Tkinter desktop interface for uploading an image and viewing
a model prediction.

## Repository Contents

The exact folder and file names may vary depending on the version
published. A suggested organization is:

``` text
Mushroom-Toxicity-Classification/
├── README.md
├── requirements.txt
├── dataset/                
├── models/
│   ├── convnext_tiny/
│   ├── convnext_small/
│   ├── weighted_ensemble/
│   └── conv_swin_hybrid/
├── desktop_application/
├── results/
└── research_paper/
```

## Getting Started

Clone the repository:

``` bash
git clone https://github.com/<your-username>/<repository-name>.git
cd <repository-name>
```

Create and activate a virtual environment, then install the dependencies
listed in `requirements.txt`:

``` bash
python -m venv .venv
```

Windows:

``` bash
.venv\Scripts\activate
```

Install dependencies:

``` bash
pip install -r requirements.txt
```

**Note:** A ready-to-run training or prediction command is not specified
here because the published repository's script names, checkpoint paths
and exact dependency versions should be documented from the code you
upload. Add those commands once the repository structure is finalized.
Model checkpoints and the full image dataset may be large; consider Git
LFS or GitHub Releases, and follow iNaturalist licensing/attribution
requirements for dataset images.

## Future Work

-   Expand the image dataset using additional biodiversity sources.
-   Extend binary classification to mushroom species-level
    classification.
-   Optimize models for mobile and edge-device deployment.
-   Explore explainable AI methods to help interpret model predictions.
-   Investigate habitat, geographic and environmental context as
    additional information.

## Citation

If you use or refer to this work, cite the associated research paper:

**"Deep Learning Approaches for Mushroom Toxicity Classification."**

Add the final publication or conference details here when available.

## Disclaimer

This software is an experimental academic classifier, not a food-safety
system or a substitute for expert mushroom identification. A high
confidence score does not establish that a mushroom is edible or safe.
