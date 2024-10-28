# Mask R-CNN for Bubble mask extraction

This is a project of [Multiphase flow & Flow visualization Lab](https://mffv.snu.ac.kr/) for bubble detection and mask extraction. The purpose of the project is to automatically extract bubble mask of experimental images from various experimental conditions using deep learning model. More information can be found in the paper ([Kim & Park, 2021](https://www.nature.com/articles/s41598-021-88334-0)). 

The codes are based on [Matterport Mask R-CNN implementation](https://github.com/matterport/Mask_RCNN), using ResNet-101 as the backbone and applied transfer learning from pre-trained COCO weights. 

The output of the model is as follows:

- color mask for input image/video 
- PNG logical mask for each bubble detected
- bubble property txt (centroid, area, axes, orientation)

The repository includes:

- Source code of Mask R-CNN built on FPN and ResNet101.
- Source code to visualize the color mask of the input image/video.
- source code to detect and save logical mask and bubble properties.

![Mask Extraction Example](assets/sample.gif)


## [👣 2024 updated] Environment package (conda-pack)
Because the model was released long ago, some packages are incompatible.

Thanks to [conda-pack](https://conda.github.io/conda-pack/), we released our packages which are compatible with the model.

The package is available in here [link](https://drive.google.com/file/d/15rp_MNpDyCmpegIoHUrZq6170-qqWraP/view?usp=drive_link).

1. Download and unzip the package.
2. Download this repo under the unzipped folder. ex) `my_env/bubble/bubble.py`
3. Activate the environment. `source my_env/bin/activate`
4. To deactivate `source my_env/bin/deactivate`

** The package was tested under Linux OS.


## Tested environment
This code was tested on the below environment.

- NVIDIA RTX 2080 ti
- Driver 440.95.01
- CUDA 10.2
- cuDNN 7.6.5
- Python 3.7
- TensorFlow 1.14.0
- Keras 2.2.5 and other common packages listed in `requirements.txt`.


## Preparing the input
Prepare images (JPG or PNG or TIF) under a series of folders ending in `_###` 

- For example, `folder_001, folder_002 ...` 
- Your `path/to/image` become `.../folder`


## How to test your own bubble image/video
1. Clone this repository
1. Install dependencies
   ```bash
   pip3 install -r requirements.txt
   ```
1. Run setup from the repository root directory
    ```bash
    python3 setup.py install
    ``` 
1. Download trained weights (mask_rcnn_bubble.h5) from the [link](https://drive.google.com/file/d/1BSi4djQtR0QKYEp-nFGsGi0e6UVEx5ug/view?usp=sharing).

1. Run bubble detection script **in `bubble/` directory** to visualize color mask
   (supports only 3-channel jpg image or video)
    ```bash
    bubble$ python3 bubble.py splash --weights=path/to/mask_rcnn_bubble.h5 --image=path/to/image
    ```
    for the video:
    ```bash
    bubble$ python3 bubble.py splash --weights=path/to/mask_rcnn_bubble.h5 --video=path/to/video
    ```
    
1. Run bubble detection script **in `bubble/` directory** to extract logical mask and bubble properties
   (JPG or PNG or TIF images)
    ```bash
    bubble$ python3 bubble.py detect --weights=path/to/mask_rcnn_bubble.h5 --image=path/to/image --results=/path/to/results --folder_num_start=0 --folder_num=1 --confidence=0.5 to 0.99
    ```

