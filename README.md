## Composed Image Retrieval on Real-life Images
This repository contains the **C**omposed **I**mage **R**etrieval on **R**eal-life images (**CIRR**) dataset.

For details please see our [ICCV 2021 paper](https://arxiv.org/abs/2108.04024) - **Image Retrieval on Real-life Images with Pre-trained Vision-and-Language Models**.

If you find this repository useful, we would appreciate it if you could give us a star.


>You are currently viewing the [Dataset repository](https://github.com/Cuberick-Orion/CIRR). For more information, see our [Project homepage](https://cuberick-orion.github.io/CIRR/).

>If you wish to develop on this task using our codebase, we recommend first checking out our [Code repository](https://github.com/Cuberick-Orion/CIRPLANT), setting up the code locally, then downloading the dataset.

## News and Upcoming Updates

<details>
  <summary>Click to see news</summary>
  
  - **Aug. 2021**: We have updated our test-split server to include the Recall_Subset evaluation.
  - **Aug. 2021**: We have opened our test-split evaluation server.
  - **Aug. 2021**: We are releasing our dataset and code for the project.
  
</details>

<details>
  <summary>Click to see our planned updates</summary>
  
  - None.
  
</details>

## Download CIRR Dataset

> Our dataset is structured in a similar way as [Fashion-IQ](https://github.com/XiaoxiaoGuo/fashion-iq), an existing dataset on this task.

### Annotations

Obtain the annotations by:
```bash
# create a `data` folder at your desired location
mkdir data
cd data

# clone the cirr_dataset branch to the local data/cirr folder
git clone -b cirr_dataset git@github.com:Cuberick-Orion/CIRR.git cirr
```

The `data/cirr` folder contains all relevant annotations. File structure is described [below](#dataset-file-structure).

### Pre-extracted Image Features

The available types of image features are:
 - ImageNet pre-trained ResNet152 features
   - can be extracted from raw images
   - we recommend [downloading our extracted in `zip`](https://drive.google.com/file/d/1JIEM46AwtdwfsEsSMsRoZhml0Xlf5060/view?usp=sharing)
 - F-RCNN image regional features
   - provided by OSCAR as we source our images from NLVR2
   - we recommend [downloading the subset of features used in CIRR](https://drive.google.com/file/d/1lzd3bljiF9evVkHJ-95FLCfu7dGJg-Iz/view?usp=sharing) (filtered out unused images and re-zipped by us)
   - alternatively, [download directly from OSCAR](https://github.com/microsoft/Oscar/blob/master/DOWNLOAD.md)

Each `zip` file we provide contains a folder of individual image feature files `.pkl`.

Once downloaded, unzip it into `data/cirr/`, following the file structure [below](#dataset-file-structure).

### Raw Images

Training and testing on CIRR do not require raw images. However, should you want to access them, please refer to our image source [NLVR2](https://lil.nlp.cornell.edu/nlvr/).

**Note**: We do not recommend [downloading the images by URLs](https://github.com/lil-lab/nlvr/tree/master/nlvr2#downloading-the-images), as it contains too many broken links. Instead, we suggest [following the instructions here](https://github.com/lil-lab/nlvr/tree/master/nlvr2#direct-image-download) to directly access the images. To quote the authors:

>To obtain access, please fill out the linked [Google Form](https://goo.gl/forms/yS29stWnFWzrDBFH3). This form asks for your basic information and asks you to agree to our Terms of Service. We will get back to you within a week. If you have any questions, please email `nlvr@googlegroups.com`.

## Dataset File Structure

<details>
  <summary>The downloaded dataset should look like this (Click to expand!)</summary>
  
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
We do not publish the ground truth for the test split of CIRR. Instead, an evaluation server is hosted [here](http://cirr.cecs.anu.edu.au/), should you prefer to publish results on the test-split. The functions of the test-split server will be incrementally updated.

[See test-split server instructions](Test-split_server.md).

## License
 - We have licensed the annotations of CIRR under the MIT License. Please refer to the [LICENSE file](LICENSE) for details.

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