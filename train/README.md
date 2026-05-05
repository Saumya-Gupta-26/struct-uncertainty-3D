# Structure-wise Uncertainty for 3D Segmentation

This repository contains training code for 3D structure-wise uncertainty of tiff volumes. The inference/testing code is separate and has been provided earlier.

## 1. Environment Setup
Please follow environment setup instructions from inference code (both environment setup as well as DIPHA)

## 2. Training data
For this pipeline, I used Figure3 data to train the segmentation model. I then used the segmentation model to perform inference on Figure2 data to predict 'likelihood'. Then, Figure2 input/likelihood/gt are used to train the uncertainty model. 
- Need to populate directories `data/Figure3/image` and `data/Figure3/gt` with Figure3 input (.tiff) and gt (.tiff) files respectively
- Need to populate directories `data/Figure2/image` and `data/Figure2/gt` with Figure2 input (.tif) and gt (.tiff) files respectively.
- Need to populate `data/Figure2/seg_pred` with .npy files. These are predictions made by the segmentation_unet3d model. Use the inference code shared earlier to generate these .npy likelihood/predictions.

## 3. Running the pipeline
First need to train the segmentation model (on Figure3 data). Then we use the outputs/predictions of the segmentation model to train the uncertainty model (on Figure2 data).

### 3.1) Training the Segmentation model
Sample run command:
```bash
cd segmentation_unet3d/
CUDA_VISIBLE_DEVICES="1,2,3,4" python3 train_unet_3D.py --params config.json
```
### 3.2) Training the Uncertainty model 
Sample run command:
```bash
cd uncertainty/
CUDA_VISIBLE_DEVICES=6 python3 train.py --params config.json
```

## 4. Contact
For any issues, please email saumgupta@cs.stonybrook.edu
