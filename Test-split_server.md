## Test-split Server on CIRR Dataset

We host an [evaluation server](http://cirr.cecs.anu.edu.au/) individually. It accepts a `.json` file containing the model's predictions and returns results.

>The `.json` files must be generated following our templates, otherwise, it cannot be properly processed.

>We do not save your information, nor your uploaded files to the server. 

>Nevertheless, please follow our instructions and DO NOT upload any file containing sensitive information. We are not responsible for any related incidents.

### Generating the Prediction Files for Upload

#### The Easiest Way
If you are developing based on the [CIRPLANT](https://github.com/Cuberick-Orion/CIRPLANT) codebase, please refer to [this section](https://github.com/Cuberick-Orion/CIRPLANT#test-split-evaluation) of the README file. The model supports exporting two `.json` files that can be readily uploaded for the evaluation of Recall and Recall_Subset.

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
 - The list of candidates is your model's prediction. 
 - To limit the file size, please select, for each entry, the top-50 (resp. 3) predictions to evaluate on Recall (resp. Recall_Subset).
 - **Important** Two special entries shall be added to the file, indicating the version of the CIRR dataset used, and the metric for evaluation.
   - Note that Recall and Recall_Subset require two individual JSON files.
   - e.g., `"version": "rc2", "metric": "recall",`

See example `.json` files on [Recall](demo_files/test1_pred_ranks_recall.json) and [Recall_Subset](demo_files/test1_pred_ranks_recall_subset.json). These files were generated on our trained baseline model. You can try to upload them to the server, they shall pass all our sanity checks.

### Contact
If you have any questions regarding our dataset, model, or publication, please create an issue in the [project repository](https://github.com/Cuberick-Orion/CIRR/issues), or email [zheyuan.liu@anu.edu.au](mailto:zheyuan.liu@anu.edu.au).