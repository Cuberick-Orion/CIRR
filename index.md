---
layout: project
title: "CIRR Dataset — Composed Image Retrieval on Real-life Images"
description: "The CIRR dataset and CIRPLANT model for composed image retrieval on real-life images. Download annotations, images, and features; explore file formats, the paper, code, and test-split evaluation."
last_modified_at: 2026-09-17
---

<header class="project-intro" aria-labelledby="page-heading" markdown="1">

# CIRR Dataset
{: #page-heading}

## Composed Image Retrieval on Real-life Images
{: #composed-image-retrieval-on-real-life-images .project-subtitle}

<div class="project-copy" markdown="1">

**Composed Image Retrieval** (or **Image Retrieval conditioned on Language Feedback**) is a retrieval task where an input query consists of an image and a short textual description of how to modify the image.

We introduce the **C**omposed **I**mage **R**etrieval on **R**eal-life images (**CIRR**) dataset — the first dataset of open-domain, real-life images with human-generated modification sentences.

</div>

<div class="action-row">
  <a class="btn btn-primary" href="#cirr-dataset">Download dataset</a>
  <a class="btn btn-dark" href="https://openaccess.thecvf.com/content/ICCV2021/html/Liu_Image_Retrieval_on_Real-Life_Images_With_Pre-Trained_Vision-and-Language_Models_ICCV_2021_paper.html" target="_blank" rel="noopener noreferrer">Published paper · ICCV 2021</a>
  <a class="btn btn-outline" href="https://youtu.be/9IA-bCuhlac" target="_blank" rel="noopener noreferrer">5-minute video</a>
</div>

<nav class="page-outline" aria-label="On this page">
  <a href="#cirr-dataset">Downloads</a>
  <a href="#dataset-file-description">File reference</a>
  <a href="#test-split-evaluation-server">Evaluation</a>
  <a href="#cirplant-model">Model</a>
  <a href="#news">News</a>
  <a href="#licensing">Licensing</a>
  <a href="#citation">Citation</a>
  <a href="#contact">Contact</a>
</nav>

</header>

<section class="panel" aria-labelledby="overview-heading" markdown="1">

## Composed image retrieval
{: #overview-heading .panel-heading}

<div class="panel-body" markdown="1">

For humans the advantage of a bi-modal query is clear: some concepts and attributes are more succinctly described visually, others through language. By cross-referencing the two modalities, a reference image can capture the general gist of a scene, while the text can specify finer details.

We identify a major challenge of this task as the inherent ambiguity in knowing what information is important (typically one object of interest in the scene) and what can be ignored (e.g., the background and other irrelevant objects).

<figure class="example-figure">
  <a class="example-image-link" href="{{ '/demo_imgs/project_page_demo_img_0.png' | relative_url }}" target="_blank" rel="noopener noreferrer" aria-label="Open the CIRR example image at full size">
    <img src="{{ '/demo_imgs/project_page_demo_img_0.png' | relative_url }}" alt="CIRR example: a reference photo of a dog is paired with modification text to retrieve either a same-breed dog running with its puppy or two same-breed dogs on the floor." width="1280" height="640">
  </a>
  <figcaption>One reference image, two modification sentences, and two different target images. Select the image to view the example at full size.</figcaption>
</figure>

</div>
</section>

<section id="cirr-dataset" class="panel" aria-labelledby="dataset-heading" markdown="1">

## Download CIRR dataset
{: #dataset-heading .panel-heading}

<div class="panel-body" markdown="1">

CIRR contains **annotations**, **raw images**, and optional **pre-extracted image features**. Its organization follows [Fashion-IQ](https://github.com/XiaoxiaoGuo/fashion-iq). Start with the annotations, then add the images or features you need under `data/cirr/`.

### Annotations
{: #annotations}

Clone the `cirr_dataset` branch into a local `data/cirr/` folder:

<div class="reference-code" tabindex="0" role="region" aria-label="Clone the CIRR annotations" markdown="1">

```bash
# create a `data` folder at your desired location
mkdir data
cd data

# clone the cirr_dataset branch to the local data/cirr folder
git clone -b cirr_dataset git@github.com:Cuberick-Orion/CIRR.git cirr
```

</div>

The [dataset repository](https://github.com/Cuberick-Orion/CIRR/tree/cirr_dataset) contains the annotations. See the [directory structure](#dataset-file-structure) and [file reference](#dataset-file-description) below for their organization and fields.

<p class="reference-note"><strong>Paper correction:</strong> Table 2 should report <strong>4,181 validation pairs</strong>, rather than 4,184.</p>

### Raw images
{: #raw-images}

CIRR uses images from NLVR2. To obtain them:

1. Follow the [NLVR2 direct-image-download instructions](https://github.com/lil-lab/nlvr/tree/master/nlvr2#direct-image-download) and submit the form agreeing to its Terms of Service.
2. If the NLVR2 team does not respond, [email us](mailto:zheyuan.david.liu@outlook.com).
3. In your email, explicitly confirm that you submitted the NLVR2 form and agreed to its terms.
{: .instruction-list}

<p class="reference-note"><strong>Use the direct image archive.</strong> Downloading individual images by URL is not recommended: many links are broken, and those downloads lack the required subfolder structure in <code>train/</code>. Preserve the original filenames and folders when extracting the images.</p>

[Raw image download guidance](https://cirr.zheyuanliu.me/raw-image-download)

### Pre-extracted image features
{: #pre-extracted-image-features}

Features are optional. Each supplied ZIP contains individual `.pkl` files; extract it into `data/cirr/`, retaining the [directory structure](#dataset-file-structure).

<div class="resource-row" markdown="1">

#### ResNet152 features

ImageNet-pretrained ResNet152 features can be extracted from the raw images or downloaded ready to use.

<a class="btn btn-outline" href="https://1drv.ms/u/s!AgLqyV5O53gxuPtPHH1LWQplm7WKag?e=V66dRc" target="_blank" rel="noopener noreferrer">Download ResNet152 features</a>

</div>

<div class="resource-row" markdown="1">

#### F-RCNN regional features

These features are provided by OSCAR for NLVR2 images. We offer the subset used in CIRR, with unused images filtered out and the files re-zipped. Alternatively, follow [OSCAR's download instructions](https://github.com/microsoft/Oscar/blob/master/DOWNLOAD.md).

<a class="btn btn-outline" href="https://1drv.ms/u/s!AgLqyV5O53gxuPtS48r36TmzZChXJw?e=BDgmyr" target="_blank" rel="noopener noreferrer">Download F-RCNN features</a>

</div>

</div>
</section>

<section id="dataset-file-description" class="panel" aria-labelledby="file-reference-heading" markdown="1">

## Dataset file reference
{: #file-reference-heading .panel-heading}

<div class="panel-body" markdown="1">

### Directory structure
{: #dataset-file-structure}

In filenames, `VER` is the dataset version and `SPLIT` is `train`, `val`, or `test1`.

Keep the NLVR2 image filenames and numeric training subfolders. These folder numbers carry no special meaning in CIRR. Both feature directories follow the same subfolder structure as `img_raw/`.

The raw-image validation folder is named **`dev/`**, while its annotation files use **`val`**.

<details class="reference-details" markdown="1">
<summary>View the complete directory structure</summary>

<div class="reference-code" tabindex="0" role="region" aria-label="CIRR dataset directory structure" markdown="1">

```text
data/cirr/
├── captions/
│   ├── cap.VER.test1.json
│   ├── cap.VER.train.json
│   └── cap.VER.val.json
├── captions_ext/
│   ├── cap.ext.VER.test1.json
│   ├── cap.ext.VER.train.json
│   └── cap.ext.VER.val.json
├── image_splits/
│   ├── split.VER.test1.json
│   ├── split.VER.train.json
│   └── split.VER.val.json
├── img_raw/
│   ├── train/
│   │   ├── 0/<image_id>.png
│   │   ├── 1/<image_id>.png
│   │   ├── 2/<image_id>.png
│   │   └── ...
│   ├── dev/<image_id>.png
│   └── test1/<image_id>.png
├── img_feat_res152/
└── img_feat_frcnn/
```

</div>

</details>

<div class="file-entry" markdown="1">

### Core annotations
{: #core-annotations}

`captions/cap.VER.SPLIT.json`
{: .file-path}

A list of records containing the core information for each query–target pair. The example includes the pair ID, reference and target images, modification sentence, and image-set membership. See **Section G of the paper's supplementary material** for field details.

<details class="reference-details" markdown="1">
<summary>View a core annotation example</summary>

<div class="reference-code" tabindex="0" role="region" aria-label="Core annotation JSON example" markdown="1">

```json
{
  "pairid": 12063,
  "reference": "test1-147-1-img1",
  "target_hard": "test1-83-0-img1",
  "target_soft": {
    "test1-83-0-img1": 1.0
  },
  "caption": "remove all but one dog and add a woman hugging   it",
  "img_set": {
    "id": 1,
    "members": [
      "test1-147-1-img1",
      "test1-1001-2-img0",
      "test1-83-1-img1",
      "test1-359-0-img1",
      "test1-906-0-img1",
      "test1-83-0-img1"
    ],
    "reference_rank": 3,
    "target_rank": 4
  }
}
```

</div>

</details>

</div>

<div class="file-entry" markdown="1">

### Auxiliary annotations
{: #auxiliary-annotations}

`captions_ext/cap.ext.VER.SPLIT.json`
{: .file-path}

A list of auxiliary annotations for each query–target pair. See **Section C of the supplementary material** for details.

<details class="reference-details" markdown="1">
<summary>View an auxiliary annotation example</summary>

<div class="reference-code" tabindex="0" role="region" aria-label="Auxiliary annotation JSON example" markdown="1">

```json
{
  "pairid": 12063,
  "reference": "test1-147-1-img1",
  "target_hard": "test1-83-0-img1",
  "caption_extend": {
    "0": "being a photo of dogs",
    "1": "add a big dog",
    "2": "more focused on the hugging",
    "3": "background should contain grass"
  }
}
```

</div>

</details>

</div>

<div class="file-entry" markdown="1">

### Image splits
{: #image-splits}

`image_splits/split.VER.SPLIT.json`
{: .file-path}

A dictionary mapping each image ID to its relative image path. Original filenames and training subfolders are preserved from NLVR2.

<details class="reference-details" markdown="1">
<summary>View an image split example</summary>

Test-split excerpt (`split.VER.test1.json`):
{: .example-label}

<div class="reference-code" tabindex="0" role="region" aria-label="Test image split JSON example" markdown="1">

```json
{
  "test1-147-1-img1": "./test1/test1-147-1-img1.png"
}
```

</div>

Training-split excerpt (`split.VER.train.json`):
{: .example-label}

<div class="reference-code" tabindex="0" role="region" aria-label="Training image split JSON example" markdown="1">

```json
{
  "train-11041-2-img0": "./train/34/train-11041-2-img0.png"
}
```

</div>

</details>

</div>

<div class="file-entry" markdown="1">

### Image feature files
{: #image-feature-files}

`img_feat_res152/` and `img_feat_frcnn/`
{: .file-path}

Each `.pkl` file stores one image's features. Replace the image filename's `.png` extension with `.pkl` to index the corresponding feature file:

<div class="reference-code" tabindex="0" role="region" aria-label="Image feature filename example" markdown="1">

```python
image_id = "test1-147-1-img1.png"
feature_filename = image_id.replace(".png", ".pkl")
# test1-147-1-img1.pkl
```

</div>

</div>

</div>
</section>

<section id="test-split-evaluation-server" class="panel" aria-labelledby="evaluation-heading" markdown="1">

## Test-split evaluation
{: #evaluation-heading .panel-heading}

<div class="panel-body" markdown="1">

<a class="service-status" href="https://cirr.zheyuanliu.me"><img src="https://img.shields.io/website?url=https%3A%2F%2Fcirr.zheyuanliu.me%2Fapi%2Fhealth&amp;label=server&amp;up_message=online&amp;up_color=brightgreen&amp;down_message=offline&amp;down_color=red" alt="Evaluation server status" height="20" loading="lazy"></a>

The test-split ground truth is kept private. Submit your model's prediction JSON files to the [evaluation server](https://cirr.zheyuanliu.me/evaluate.html) to obtain test-split scores. Validation-split ground truth remains publicly available for local development and evaluation.

Sign in with GitHub, choose a prediction file, and complete hCaptcha verification. The [How-To guide](https://cirr.zheyuanliu.me/how-to) covers file formats, submission limits, example files, and results.

<div class="action-row">
  <a class="btn btn-primary" href="https://cirr.zheyuanliu.me/evaluate.html">Test-split evaluation</a>
  <a class="btn btn-outline" href="https://cirr.zheyuanliu.me/how-to">How-To</a>
</div>

If the site is unavailable, please [contact us](#contact).
{: .section-footnote}

</div>
</section>

<section id="cirplant-model" class="panel" aria-labelledby="model-heading" markdown="1">

## CIRPLANT Model
{: #model-heading .panel-heading}

<div class="panel-body" markdown="1">

Concurrently, we release the code and pre-trained models for our method **C**omposed **I**mage **R**etrieval using **P**retrained **LAN**guage **T**ransformers (**CIRPLANT**). Together with the dataset, we believe this work will inspire further research on this task on a finer-grain level.

Our code is in [PyTorch](https://pytorch.org/), and is based on [PyTorch Lightning](https://www.pytorchlightning.ai/).

The paper, *Image Retrieval on Real-life Images with Pre-trained Vision-and-Language Models*, is available as a [PDF](https://openaccess.thecvf.com/content/ICCV2021/papers/Liu_Image_Retrieval_on_Real-Life_Images_With_Pre-Trained_Vision-and-Language_Models_ICCV_2021_paper.pdf) and on [arXiv](https://arxiv.org/abs/2108.04024).

<div class="action-row">
  <a class="btn btn-outline" href="https://github.com/Cuberick-Orion/CIRPLANT" target="_blank" rel="noopener noreferrer">Code repository</a>
</div>

</div>
</section>

<section id="news" class="panel" aria-labelledby="news-heading" markdown="1">

## News
{: #news-heading .panel-heading}

<div class="panel-body" markdown="1">

- **Sept. 2026**: The test-split evaluation server returned online after a three-day outage and migration to Cloudflare.
- **Oct. 2024**: Added guidance for researchers having trouble obtaining raw images from NLVR2.
- **Jun. 2024**: Updated the download links.
- **Aug. 2021**: Released the dataset and code, and opened the test-split evaluation server.
{: .news-list}

</div>
</section>

<section id="licensing" class="panel" aria-labelledby="licensing-heading" markdown="1">

## Licensing
{: #licensing-heading .panel-heading}

<div class="panel-body" markdown="1">

- We have licensed the code and annotations of CIRR under the MIT License. Please refer to the [LICENSE file](https://github.com/Cuberick-Orion/CIRR/blob/main/LICENSE) for details.
- Following [NLVR2 Licensing](https://github.com/lil-lab/nlvr#licensing), we do not license the images used in CIRR, as we do not hold the copyright to them.
- The images used in CIRR are sourced from the [NLVR2 dataset](https://lil.nlp.cornell.edu/nlvr/). Users are bound by its Terms of Service.
{: .licensing-list}

</div>
</section>

<section id="citation" class="panel" aria-labelledby="citation-heading" markdown="1">

## Citation
{: #citation-heading .panel-heading}

<div class="panel-body" markdown="1">

Please cite our paper if it helps your research:

<div class="citation-code" tabindex="0" role="region" aria-label="BibTeX citation" markdown="1">

```bibtex
@InProceedings{Liu_2021_ICCV,
    author    = {Liu, Zheyuan and Rodriguez-Opazo, Cristian and Teney, Damien and Gould, Stephen},
    title     = {Image Retrieval on Real-Life Images With Pre-Trained Vision-and-Language Models},
    booktitle = {Proceedings of the IEEE/CVF International Conference on Computer Vision (ICCV)},
    month     = {October},
    year      = {2021},
    pages     = {2125-2134}
}
```

</div>

</div>
</section>

<section id="contact" class="panel" aria-labelledby="contact-heading" markdown="1">

## Contact
{: #contact-heading .panel-heading}

<div class="panel-body" markdown="1">

If you have any questions regarding our dataset, model, or publication, please create an issue in the [project repository](https://github.com/Cuberick-Orion/CIRR/issues), or [email us](mailto:zheyuan.david.liu@outlook.com).

</div>
</section>
