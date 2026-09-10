---
layout: project
title: "CIRR Dataset — Composed Image Retrieval on Real-life Images"
description: "The CIRR dataset and CIRPLANT model for composed image retrieval on real-life images. Explore the dataset, paper, code, and test-split evaluation server."
last_modified_at: 2026-09-10
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
  <a class="btn btn-primary" href="https://github.com/Cuberick-Orion/CIRR" target="_blank" rel="noopener noreferrer">Dataset repository</a>
  <a class="btn btn-dark" href="https://openaccess.thecvf.com/content/ICCV2021/html/Liu_Image_Retrieval_on_Real-Life_Images_With_Pre-Trained_Vision-and-Language_Models_ICCV_2021_paper.html" target="_blank" rel="noopener noreferrer">Published paper · ICCV 2021</a>
  <a class="btn btn-outline" href="https://youtu.be/9IA-bCuhlac" target="_blank" rel="noopener noreferrer">5-minute video</a>
</div>

<nav class="page-outline" aria-label="On this page">
  <a href="#cirr-dataset">Dataset</a>
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

## CIRR Dataset
{: #dataset-heading .panel-heading}

<div class="panel-body" markdown="1">

The CIRR test-split ground truth is kept private. Use the [primary evaluation server](https://cirr.zheyuanliu.me/evaluate.html) to submit your model's predictions and obtain test-split scores. A [backup server](https://cirr.junjie.au/) is also available.

On the primary server, sign in with GitHub, upload a prediction JSON file, and complete hCaptcha verification to evaluate it. The [How-To guide](https://cirr.zheyuanliu.me/how-to) covers file formats, submission limits, and results. Prediction-file examples are also available in the [repository instructions](https://github.com/Cuberick-Orion/CIRR/blob/main/Test-split_server.md).

Validation-split ground truth remains publicly available for local development and evaluation.

<div class="action-row">
  <a class="btn btn-primary" href="https://github.com/Cuberick-Orion/CIRR" target="_blank" rel="noopener noreferrer">Dataset repository</a>
  <a class="btn btn-outline" href="https://cirr.zheyuanliu.me/raw-image-download">Raw image download</a>
  <a class="btn btn-outline" href="https://cirr.zheyuanliu.me/evaluate.html">Test-split evaluation</a>
</div>

</div>
</section>

<section id="cirplant-model" class="panel" aria-labelledby="model-heading" markdown="1">

## CIRPLANT Model
{: #model-heading .panel-heading}

<div class="panel-body" markdown="1">

Concurrently, we release the code and pre-trained models for our method **C**omposed **I**mage **R**etrieval using **P**retrained **LAN**guage **T**ransformers (**CIRPLANT**). Together with the dataset, we believe this work will inspire further research on this task on a finer-grain level.

Our code is in [PyTorch](https://pytorch.org/), and is based on [PyTorch Lightning](https://www.pytorchlightning.ai/).

<div class="action-row">
  <a class="btn btn-outline" href="https://github.com/Cuberick-Orion/CIRPLANT" target="_blank" rel="noopener noreferrer">Code repository</a>
</div>

</div>
</section>

<section id="news" class="panel" aria-labelledby="news-heading" markdown="1">

## News
{: #news-heading .panel-heading}

<div class="panel-body" markdown="1">

- **Sept. 2026**: The primary test-split evaluation server is back online after migrating to Cloudflare. Use [cirr.zheyuanliu.me](https://cirr.zheyuanliu.me/) for evaluation; [cirr.junjie.au](https://cirr.junjie.au/) remains available as a backup.
- **Aug. 2021**: We opened the test-split evaluation server.
- **Aug. 2021**: We released the dataset and code for the project.
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
