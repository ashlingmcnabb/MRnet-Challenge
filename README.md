<div align="center">

![Logo](content/logo.jpg)

# Stanford MRnet Challenge

**This repo contains code for the MRNet Challenge**

</div>
For more details refer to https://stanfordmlgroup.github.io/competitions/mrnet/

# Install dependencies
1. `pip install git+https://github.com/ncullen93/torchsample`
2. `pip install nibabel`
3. `pip install sklearn`
4. `pip install pandas`

# Instructions to run the training
1. Clone the repository.

2. Download the dataset (~5.7 GB), and put `train` and `valid` folders along with all the the `.csv` files inside `images` folder at root directory. 
```Shell
  images/
      train/
          axial/
          sagittal/
          coronal/
      val/
          axial/
          sagittal/
          coronal/
      train-abnormal.csv
      train-acl.csv
      train-meniscus.csv
      valid-abnormal.csv
      valid-acl.csv
      valid-meniscus.csv
```      

3. Make a new folder called `weights` at root directory, and inside the `weights` folder create three more folders namely `acl`, `abnormal` and `meniscus`.

4. All the hyperparameters are defined in `config.py` file. Feel free to play around those.

5. Now finally run the training using `python train.py`. All the logs for tensorboard will be stored in the `runs` directory at the root of the project.

# Understanding the Dataset

![Logo](content/mri_scan.png)

The dataset contains MRIs of different people. Each MRI consists of multiple images.
Each MRI has data in 3 perpendicular planes. And each plane as variable number of slices.

Each slice is an `256x256` image

For example:

For `MRI 1` we will have 3 planes:

Plane 1- with 35 slices

Plane 2- with 34 slices

Place 3 with 35 slices

Each MRI has to be classisifed against 3 diseases

Major challenge with while selecting the model structure was the inconsistency in the data. Although the image size remains constant , the number of slices per plane are variable within a single MRI and varies across all MRIs.

So we are proposing a model for each plane. For each model the `batch size` will be variable and equal to `number of slices in the plane of the MRI`. So training each model, we will get features for each plane.

We also plan to have 3 separate models for each disease. 

# Model Specifications

![Logo](content/model.png)

We will be using Alexnet pretrained as a feature extractor. When we would have trained the 3 models on the 3 planes, we will use its feature extractor layer as an input to a `global` model for the final classification

# Contributors
<p > 
  Neelabh Madan   
 <a href = https://github.com/neelabh17 target='blank'> <img src=https://github.com/edent/SuperTinyIcons/blob/master/images/svg/github.svg height='30' weight='30'/></a>
<br>

Jatin Prakash <a href = https://github.com/bicycleman15 target='blank'> <img src=https://github.com/edent/SuperTinyIcons/blob/master/images/svg/github.svg height='30' weight='30'/></a>


