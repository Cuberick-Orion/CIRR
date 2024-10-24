<div align="center">
 
## Composed Image Retrieval on Real-life Images

This repository contains the **C**omposed **I**mage **R**etrieval on **R**eal-life images (**CIRR**) dataset.

For details please see our [ICCV 2021 paper](https://openaccess.thecvf.com/content/ICCV2021/papers/Liu_Image_Retrieval_on_Real-Life_Images_With_Pre-Trained_Vision-and-Language_Models_ICCV_2021_paper.pdf) - **Image Retrieval on Real-life Images with Pre-trained Vision-and-Language Models**.

##

<sup> You are currently viewing the **Dataset repository**.
Site navigation > [**Project homepage**](https://cuberick-orion.github.io/CIRR/) &nbsp;|&nbsp; [**Code repository**](https://github.com/Cuberick-Orion/CIRPLANT) </sup>

[![arXiv](https://img.shields.io/badge/paper-iccv2021-383b78)](https://openaccess.thecvf.com/content/ICCV2021/html/Liu_Image_Retrieval_on_Real-Life_Images_With_Pre-Trained_Vision-and-Language_Models_ICCV_2021_paper.html) 
[![arXiv](https://img.shields.io/badge/arXiv-2108.04024-00ff00)](https://arxiv.org/abs/2108.04024)



</div>

##

**News and Upcoming Updates**

* **Oct 2024** **Please contact us if you are having trouble gaining access to the raw images from NLVR2.**
* **Jun 2024** Download links have been updated.
* Please note there is a typo in our paper (Table 2) -- the number of pairs in val is ~~4,184~~ 4,181.


## Download CIRR Dataset

Our dataset is structured in a similar way as [Fashion-IQ](https://github.com/XiaoxiaoGuo/fashion-iq), an existing dataset on this task. The files include annotations, raw images, and the optional pre-extracted image features.

### Annotations

Obtain the annotations by:
```bash
# create a `data` folder at your desired location
mkdir data
cd data

# clone the cirr_dataset branch to the local data/cirr folder
git clone -b cirr_dataset git@github.com:Cuberick-Orion/CIRR.git cirr
```

The `data/cirr` folder contains all relevant annotations. The file structure is described [below](#dataset-file-structure).

### Raw Images

**Updated October 2024 -- Please contact us if you are having trouble gaining access to the raw images from NLVR2.** 

Starting from late 2023, we have been made aware by multiple research groups that the NLVR2 team is not responding to their requests. To this end, please see the following steps in obtaining the raw images:

1. Please first contact the NLVR team and fill out a Google form agreeing to their terms of service. Instructions are [here](https://github.com/lil-lab/nlvr/tree/master/nlvr2#direct-image-download).
2. If you receive no response from the NLVR team, [email us](mailto:zheyuan.david.liu@outlook.com).
3. When contacting us, please explicitly state that you have filled out the NLVR team's Google form agreeing to their terms of service.

> [!IMPORTANT]
> The NLVR2 repository provides another way to obtain the images, which is to download the images by URLs. But we **do not** recommend it, as many of the links are broken, and the downloaded files lack the sub-folder structure in the `/train` folder.
> 
> Instead, please follow the above instruction to directly download the raw images.

### Pre-extracted Image Features

The available types of image features are:
 - ImageNet pre-trained ResNet152 features
   - can be extracted from raw images
   - or download our pre-extracted features [![Download](https://img.shields.io/badge/OneDrive-Download-red?style=flat-square&logo=microsoftonedrive)](https://1drv.ms/u/s!AgLqyV5O53gxuPtPHH1LWQplm7WKag?e=V66dRc)
 - F-RCNN image regional features
   - provided by OSCAR as we source our images from NLVR2
   - download the subset of features used in CIRR (filtered out unused images and re-zipped by us) [![Download](https://img.shields.io/badge/OneDrive-Download-red?style=flat-square&logo=microsoftonedrive)](https://1drv.ms/u/s!AgLqyV5O53gxuPtS48r36TmzZChXJw?e=BDgmyr)
   - alternatively, [download directly from OSCAR](https://github.com/microsoft/Oscar/blob/master/DOWNLOAD.md)

Each `zip` file we provide contains a folder of individual image feature files `.pkl`.

Once downloaded, unzip it into `data/cirr/`, following the file structure [below](#dataset-file-structure).

## Dataset File Structure

<details>
  <summary>The downloaded dataset should look like this (click to expand)</summary>
  
  ```
  data
  └─── cirr
      ├─── captions
      │        cap.VER.test1.json
      │        cap.VER.train.json
      │        cap.VER.val.json
      ├─── captions_ext
      │        cap.ext.VER.test1.json
      │        cap.ext.VER.train.json
      │        cap.ext.VER.val.json
      ├─── image_splits
      │        split.VER.test1.json
      │        split.VER.train.json
      │        split.VER.val.json
      ├─── img_raw  
      │    ├── train
      │    │    ├── 0 # sub-level folder structure inherited from NLVR2 (carries no special meaning in CIRR)
      │    │    │    <IMG0_ID>.png
      │    │    │    <IMG0_ID>.png
      │    │    │         ...
      │    │    ├── 1
      │    │    │    <IMG0_ID>.png
      │    │    │    <IMG0_ID>.png
      │    │    │         ...
      │    │    ├── 2
      │    │    │    <IMG0_ID>.png
      │    │    │    <IMG0_ID>.png
      │    │    └──       ...
      │    ├── dev         
      │    │      <IMG0_ID>.png
      │    │      <IMG1_ID>.png
      │    │           ...
      │    └── test1       
      │           <IMG0_ID>.png
      │           <IMG1_ID>.png
      │                ...
      ├─── img_feat_res152 
      │        <Same subfolder structure as above>
      └─── img_feat_frcnn         
               <Same subfolder structure as above>
  ```
</details>


## Dataset File Description

 - `captions/cap.VER.SPLIT.json`
    - A list of elements, where each element contains core information on a query-target pair.
    - Details on each entry can be found in the **supp. mat. Sec. G** of our paper.
    - <details>
      <summary>Click to see an example</summary>
      
      ```json
          {"pairid": 12063, 
          "reference":   "test1-147-1-img1", 
          "target_hard": "test1-83-0-img1", 
          "target_soft": {"test1-83-0-img1": 1.0}, 
          "caption": "remove all but one dog and add a woman hugging   it", 
          "img_set": {"id": 1, 
                      "members": ["test1-147-1-img1", 
                                  "test1-1001-2-img0",  
                                  "test1-83-1-img1",           
                                  "test1-359-0-img1",  
                                  "test1-906-0-img1", 
                                  "test1-83-0-img1"],
                      "reference_rank": 3, 
                      "target_rank": 4}
          }
      ```
      </details>


 - `captions_ext/cap.ext.VER.SPLIT.json`
    - A list of elements, where each element contains auxiliary annotations on a query-target pair.
    - Details on the auxiliary annotations can be found in the **supp. mat. Sec. C** of our paper.
    - <details>
      <summary>Click to see an example</summary>
      
      ```json
          {"pairid": 12063, 
          "reference":   "test1-147-1-img1", 
          "target_hard": "test1-83-0-img1", 
          "caption_extend": {"0": "being a photo of dogs", 
                            "1": "add a big dog", 
                            "2": "more focused on the hugging", 
                            "3": "background should contain grass"}
          }
      ```
      </details>

  

 - `image_splits/split.VER.SPLIT.json`
    - A dictionary, where each key:value pair maps an image filename to the relative path of the img file, example:
      ```json
      "test1-147-1-img1": "./test1/test1-147-1-img1.png",
      # or
      "train-11041-2-img0": "./train/34/train-11041-2-img0.png"
      ```
    - image filenames and (train-split) sub-level folder structures are preserved from the NLVR2 dataset.
 - `img_feat_<...>/`
    - A folder containing a certain type of pre-extracted image features, each file saves the feature of one image.
    - Filename is generated as such:
      ```python
      <IMG0_ID> = "test1-147-1-img1.png".replace('.png','.pkl')
      ```
      in this case, `test1-147-1-img1.pkl`, so that each file can be directly indexed by its name.

## Test-split Evaluation Server
We do not publish the ground truth for the test split of CIRR. Instead, an evaluation server is hosted [here](http://cirr.cecs.anu.edu.au/), should you prefer to publish results on the test-split. The functions of the test-split server will be incrementally updated.

[See test-split server instructions](Test-split_server.md).

The server is hosted independently at CECS ANU, so please [email us](mailto:zheyuan.david.liu@outlook.com) if the site is down.

## License
 - We have licensed the annotations of CIRR under the MIT License. Please refer to the [LICENSE file](LICENSE) for details.

 - Following [NLVR2 Licensing](https://github.com/lil-lab/nlvr#licensing), we do not license the images used in CIRR, as we do not hold the copyright to them.

 - The images used in CIRR are sourced from the [NLVR2 dataset](https://lil.nlp.cornell.edu/nlvr/). Users shall be bounded by its Terms of Service.
 
## Citation

Please cite our paper if it helps your research:
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

## Contact
If you have any questions regarding our dataset, model, or publication, please create an issue in the [project repository](https://github.com/Cuberick-Orion/CIRR/issues), or [email us](mailto:zheyuan.david.liu@outlook.com).
