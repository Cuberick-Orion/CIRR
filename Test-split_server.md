## Test-split Server on CIRR Dataset

Our test-split server is hosted individually [here](cirr.cecs.anu.edu.au). It accepts a `.json` file containing the model's predictions and returns results.

>The `.json` file must be generated following our templates, otherwise, it cannot be properly processed.

>We do not save your information, nor your uploaded files to the server. 

>Nevertheless, please follow our instructions and DO NOT upload any file containing sensitive information. We are not responsible for any related incidents.

### Generating the Prediction Files for Upload

#### The Easiest Way
If you are developing based on the [CIRPLANT](https://github.com/Cuberick-Orion/CIRPLANT) codebase, please refer to [this section](https://github.com/Cuberick-Orion/CIRPLANT#test-split-evaluation) of the README file. The model supports exporting a `.json` file that can be readily uploaded.

#### The Manual Way
Please follow the following template to generate the `.json` file.

 - The content should be a dictionary, where each entry looks like:
   ```json
    "12063": ["test1-233-3-img1", 
              "test1-969-1-img0", 
              "test1-455-2-img1", 
              "test1-835-3-img0", 
              "test1-238-1-img1",
              ...
    ],
   ```
   - Here, `12063` is the unique `pair_id`, you shall find it in our dataset annotation entries (check out either one of the    `captions/cap.VER.SPLIT.json` files).
   - The list of candidates is your model's prediction. To limit the file size, please select the top-50 predictions for each entry.
 - **Important** A special entry shall be added to the file, indicating the version of the CIRR dataset used - in case of future changes made to the testing procedures.
   - e.g., `"version": "rc2"`

An example `.json` file is available [here](demo_files/test.rand.v0.json). You can try to upload it to the server - it shall pass all our sanity checks.

### Contact
If you have any questions regarding our dataset, model, or publication, please create an issue in the [project repository](https://github.com/Cuberick-Orion/CIRR/issues), or email [zheyuan.liu@anu.edu.au](mailto:zheyuan.liu@anu.edu.au).