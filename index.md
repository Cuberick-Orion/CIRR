## Composed Image Retrieval on Real-life Images

**Composed Image Retrieval** (or, **Image Retreival conditioned on Language Feedback**) is a relatively new retrieval task, where an input query consists of an image and short textual description of how to modify the image. 

For humans the advantage of a bi-modal query is clear: some concepts and attributes are more succinctly described visually, others through language. By cross-referencing the two modalities, a reference image can capture the general gist of a scene, while the text can specify finer details.

We identify a major challenge of this task as the inherent ambiguity in knowing what information is important (typically one object of interest in the scene) and what can be ignored (e.g., the background and other irrelevant objects).

Here, we extend the task of composed image retrieval by introducing the **C**omposed **I**mage **R**etrieval on **R**eal-life images (**CIRR**) dataset - the first dataset of open-domain, real-life images with human-generated modification sentences.

![Demo image from CIRR data](demo_imgs/project_page_demo_img_0.png)

Concurrently, we release the code and pre-trained models for our method **C**omposed **I**mage **R**etrieval using **P**retrained **LAN**guage **T**ransformers (**CIRPLANT**). Together with the dataset, we believe this work will inspire further research on this task on a finer-grain level.

Read more in our [published paper](https://arxiv.org/abs/2108.04024).

----
<sub>You are currently viewing the [Project homepage](https://cuberick-orion.github.io/CIRR/).</sub>


## CIRR Dataset

<!-- ### Download -->

[Click to download our dataset](https://github.com/Cuberick-Orion/CIRR).

<!-- ### Test-split Evaluation Server -->

We do not publish the ground truth for the test split of CIRR. Instead, we host an [evaluation server](http://cirr.cecs.anu.edu.au/), should you prefer to publish results on the test-split.

Note, the ground truth for the validation split is available as usual and can be used for development.

## CIRPLANT Model

[Click to access our codebase](https://github.com/Cuberick-Orion/CIRPLANT).

Our code is in [PyTorch](https://pytorch.org/), and is based on [PyTorch Lightning](https://www.pytorchlightning.ai/). 

----
<sub>To encourage continuing research in this task, we will additionally provide an implementation of [TIRG](https://github.com/google/tirg) that is compatible with our codebase (coming soon).</sub>

## News
 - **Aug. 2021**: We have opened our test-split evaluation server.
 - **Aug. 2021**: We are releasing our dataset and code for the project.

## Licensing

 - We have licensed the code and annotations of CIRR under the MIT License. Please refer to the LICENSE file for details.

 - Following [NLVR2 Licensing](https://github.com/lil-lab/nlvr#licensing), we do not license the images used in CIRR, as we do not hold the copyright to them.

 - The images used in CIRR are sourced from the [NLVR2 dataset](https://lil.nlp.cornell.edu/nlvr/). Users shall be bounded by its Terms of Service.
 
## Citation

Please cite our paper if it helps your research:
```
@article{liu2021cirr,
      title={Image Retrieval on Real-life Images with Pre-trained Vision-and-Language Models}, 
      author={Zheyuan Liu and Cristian Rodriguez-Opazo and Damien Teney and Stephen Gould},
      journal={arXiv preprint arXiv:2108.04024},
      year={2021},
}
```

## Contact

If you have any questions regarding our dataset, model, or publication, please create an issue in the [project repository](https://github.com/Cuberick-Orion/CIRR/issues), or email [zheyuan.liu@anu.edu.au](mailto:zheyuan.liu@anu.edu.au).