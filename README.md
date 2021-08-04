## Composed Image Retrieval on Real-life Images
This repository contains the **C**omposed **I**mage **R**etrieval on **R**eal-life images (**CIRR**) dataset.

For details please see our [ICCV 2021 paper](#) - **Image Retrieval on Real-life Images with Pre-trained Vision-and-Language Models**.

If you find this repository useful, we would appreciate it if you give us a star.

-----
>You are currently viewing the [dataset repository](https://github.com/Cuberick-Orion/CIRR). For more information, see our [project homepage](https://cuberick-orion.github.io/CIRR/).

## Download CIRR Dataset

### Annotations

Directly download by zip, or clone this repository to local by:

```bash
git clone git@github.com:Cuberick-Orion/CIRR.git
```

The `data` folder structure is described [below](#dataset-file-structure), you can find all relevant annotations in the `.json` files.

### Pre-extracted Image Features

### Raw Images

Training and testing on CIRR does not require the raw images. However, should you prefer to acces them, please refer to our image source [NLVR2](https://lil.nlp.cornell.edu/nlvr/).

**Note**: we do not recommend downloading the images by URLs ([provided here](https://github.com/lil-lab/nlvr/tree/master/nlvr2#downloading-the-images)), as it contains too many broken links. Instead, we suggest to follow the [instructions here](https://github.com/lil-lab/nlvr/tree/master/nlvr2#direct-image-download) to directly access the images. To quote the authors:

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
     ├─── img_feat_frcnn  <-[RCNN regional features]
     │        <IMG0_ID>.pkl
     │        <IMG1_ID>.pkl
     │            ...
     ├─── img_feat_res152 <-[ResNet 152 features]
     │        <IMG0_ID>.pkl
     │        <IMG1_ID>.pkl
     │            ...
     ├─── img_raw         <-[Optional, raw images]
     │        <IMG0_ID>.pkl
     │        <IMG1_ID>.pkl
     │            ...     
     └─── img_feat_<...>  <-[Some other types of features]
              <IMG0_ID>.pkl
              <IMG1_ID>.pkl
                  ...     
```

where, `VER` is the dataset version, `img_feat` folders contain different types of feature.

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
    - Details on each entry can be found in the supp. mat. Sec.G of our paper.

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
    - Details on the auxiliary annotations can be found in the supp. mat. Sec.C of our paper.

 - `image_splits/split.VER.SPLIT.json`
    - A list of elements, where each element maps an image filename to the relative path of the img file, example:
      ```json
      {"test1-147-1-img1": "./test1/test1-147-1-img1.png",
       "test1-83-0-img1": "./test1/test1-83-0-img1.png",
       "test1-11-2-img0": "./test1/test1-11-2-img0.png",
       ...
      }
      ```
    - image filenames are preserved from the NLVR2 dataset.
 - `img_feat_<...>/`
    - A folder containing a certain type of pre-extracted image features, each file saves the feature of one image.
    - Filename is generated as such:
      ```python
      <IMG0_ID> = "test1-147-1-img1.png".replace('.png','.pkl')
      ```
      i.e., `test1-147-1-img1.pkl`, so that each file can be directly indexed by its name.

## Test-split Evaluation Server
We do not publish the ground-truth for the test-split of CIRR. Instead, an evaluation server is hosted at: [https://cirr.cecs.anu.edu.au/](https://cirr.cecs.anu.edu.au/), should you prefer to publish results on the test-split.

## License
 - We have licensed the annotations of CIRR under the MIT License. Please refer to the [LICENSE file](LICENSE) for details.

 - Following [NLVR2 Licensing](https://github.com/lil-lab/nlvr#licensing), we do not license the images used in CIRR, as we do not hold the copyright to them.

 - The images used in CIRR are sourced from the [NLVR2 dataset](https://lil.nlp.cornell.edu/nlvr/). Users shall be bounded by its Terms of Service.
 
## Citation

Please cite our paper if it helps your research:
```
# TODO
```