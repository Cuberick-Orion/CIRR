## Composed Image Retrieval on Real-life Images
This repository contains the **C**omposed **I**mage **R**etrieval on **R**eal-life images (**CIRR**) dataset.

For details please see our [ICCV 2021 paper](#) - **Image Retrieval on Real-life Images with Pre-trained Vision-and-Language Models**.

If you find this repository useful, we would appreciate it if you give us a star.

-----
>You are currently viewing the [Dataset repository](https://github.com/Cuberick-Orion/CIRR). For more information, see our [Project homepage](https://cuberick-orion.github.io/CIRR/).

## Download CIRR Dataset

> Our dataset is structured in a similar way as [Fashion-IQ](https://github.com/XiaoxiaoGuo/fashion-iq), an existing dataset on this task.

### Annotations

First create a `data` folder to your desired location, then clone the `data` branch to local with:

```bash
mkdir data
cd data

git clone -b data git@github.com:Cuberick-Orion/CIRR.git
```

The `data/cirr` folder contains all relevant annotations. File structure is described [below](#dataset-file-structure).

### Pre-extracted Image Features

The available types of image features are:
 - ImageNet pre-trained ResNet152 features
   - can be extracted from raw images
   - we recommend [downloading our extracted in `zip`](https://drive.google.com/file/d/1JIEM46AwtdwfsEsSMsRoZhml0Xlf5060/view?usp=sharing)
 - F-RCNN image regional features
   - provided by OSCAR as we source our images from NLVR2
   - [download directly from OSCAR](https://github.com/microsoft/Oscar/blob/master/DOWNLOAD.md)
   - we recommend [downloading the subset of features used in CIRR](https://drive.google.com/file/d/1lzd3bljiF9evVkHJ-95FLCfu7dGJg-Iz/view?usp=sharing) (filtered out unused images and re-zipped by us)

Each `zip` file we provide contains a folder of individual image feature files `.pkl`.

Once downloaded, unzip it into `data/cirr/`, following the file structure [below](#dataset-file-structure).

### Raw Images

Training and testing on CIRR do not require raw images. However, should you want to access them, please refer to our image source [NLVR2](https://lil.nlp.cornell.edu/nlvr/).

**Note**: We do not recommend downloading the images by URLs ([provided here](https://github.com/lil-lab/nlvr/tree/master/nlvr2#downloading-the-images)), as it contains too many broken links. Instead, we suggest following the [instructions here](https://github.com/lil-lab/nlvr/tree/master/nlvr2#direct-image-download) to directly access the images. To quote the authors:

>To obtain access, please fill out the linked [Google Form](https://goo.gl/forms/yS29stWnFWzrDBFH3). This form asks for your basic information and asks you to agree to our Terms of Service. We will get back to you within a week. If you have any questions, please email `nlvr@googlegroups.com`.

## Dataset File Structure

The downloaded dataset should look like this:

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
     ├─── img_feat_frcnn  
     │    ├── train      
     │    │      <IMG0_ID>.pkl
     │    │      <IMG1_ID>.pkl
     │    │           ...
     │    ├── dev         
     │    │      <IMG0_ID>.pkl
     │    │      <IMG1_ID>.pkl
     │    │           ...
     │    └── test1       
     │           <IMG0_ID>.pkl
     │           <IMG1_ID>.pkl
     │                ...
     ├─── img_feat_res152 
     │        <Same subfolders as above>
     └─── img_raw         
              <Same subfolders as above>
```

where `VER` is the dataset version.

## Dataset File Description

 - `captions/cap.VER.SPLIT.json`
    - A list of elements, where each element contains core information on a query-target pair, example:
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
    - Details on each entry can be found in the **supp. mat. Sec. G** of our paper.

 - `captions_ext/cap.ext.VER.SPLIT.json`
    - A list of elements, where each element contains auxiliary annotations on a query-target pair, example:
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
    - Details on the auxiliary annotations can be found in the **supp. mat. Sec. C** of our paper.

 - `image_splits/split.VER.SPLIT.json`
    - A dictionary, where each key:value pair maps an image filename to the relative path of the img file, example:
      ```json
      "test1-147-1-img1": "./test1/test1-147-1-img1.png",
      ```
    - image filenames are preserved from the NLVR2 dataset.
 - `img_feat_<...>/`
    - A folder containing a certain type of pre-extracted image features, each file saves the feature of one image.
    - Filename is generated as such:
      ```python
      <IMG0_ID> = "test1-147-1-img1.png".replace('.png','.pkl')
      ```
      in this case, `test1-147-1-img1.pkl`, so that each file can be directly indexed by its name.

## Test-split Evaluation Server
We do not publish the ground truth for the test split of CIRR. Instead, an evaluation server is hosted [here](https://cirr.cecs.anu.edu.au/), should you prefer to publish results on the test-split.

## License
 - We have licensed the annotations of CIRR under the MIT License. Please refer to the [LICENSE file](LICENSE) for details.

 - Following [NLVR2 Licensing](https://github.com/lil-lab/nlvr#licensing), we do not license the images used in CIRR, as we do not hold the copyright to them.

 - The images used in CIRR are sourced from the [NLVR2 dataset](https://lil.nlp.cornell.edu/nlvr/). Users shall be bounded by its Terms of Service.
 
## Citation

Please cite our paper if it helps your research:
```
# TODO
```