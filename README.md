# Unsupervised Droplet Counting and Classification, and Neubauer Chamber Automation
**TeamSnorlax:**
* Ruben Burdin
* Medya Tekes
* Nicholas Sperry

## Overview
This EPFL ML project (ML for science) aims at assisting with cutting edge machine learning techniques lab researches with 2 different tools. 
- Project 1: A droplet counting and classification utility for microscope images
- Project 2: A cell counting for neubauer chamber microscope images

These can be considered as 2 different projects and required our team to double down on effort and resource investment for each of them. This is an outstanding achievement to have acheived two full machine learning projects when only one was required.

These 2 projects are impact work. They aim at improving the quality, consistence and speed of analysis for lab researchers.
Out tools have both been wrapped into Docker images and made public (open sourced) so that it could (1) be used in any lab of the planet with a single command line and 
(2) the approaches fine-tuned by further machine learning research. 
Our novel and outstanding performance models are completely reproducible are not yet been published in any paper so far. We are thus into pioneering research.

Please see the attached research paper in PDF for futher explanation on the methods and results.

Have fun experimenting or futher researching!

## Installation and Requirements

### Requirements

#### Data
This project involved using two separate datasets - one for the Unsupervised Droplet Counting and Classification and another for the Neubauer Chamber Automation. Due to the data augmentation methods we used, these datasets have become quite large so we instead host them in a Google Drive. For the Unsupervised Droplet Counting and Classification:

* Download the data from **LINK**, and place inside the `Project 1 - Unsupervised Droplet classification/` folder.

For the Neubauer Chamber Automation:

* Download the data from **LINK**, and place inside the `Project 2 - Cell counting in Neubauer Chambers/`folder. This data set is quite large, around 4 Gigabytes.

#### Installation
This project is based entirely on Jupyter Notebooks. To run these, make sure you have Anaconda installed on your machine. All the requirements should be already met, but if not there are some `!pip install ` commands in the notebooks for any extra requirements. This entire project was done using Google Colab, so there should be no issues when run from there.

We also provide some Docker images: **LINK AND LINK**


## Project Layout
Since this project contains two sub-projects, we have split the GitHub to make this cleaner. 

### Project 1 - Unsupervised Droplet Counting and Classification
The first part of the project can be found in the `Project 1 - Unsupervised Droplet classification/` folder, and contains the following notebooks:

* `unsupervised_droplet_classifier_demo.ipynb` - **Explain**
* `unsupervised_droplet_classification_analysis.ipynb` - **Explain**

### Project 2 - Neubauer Chamber Automation
The second part of the project can be found in the `Project 2 - Cell counting in Neubauer Chambers/`folder, and contains the following notebooks:

* `Data Augmentation.ipynb` - The notebook used to create the Augmented Data set from the original Instagram dataset
* `DataSets.ipynb` - Contains the Pytorch Dataset class to load the data to train the UNet model. It is a static notebook, and is only used when imported into the other notebooks
* `UNetModel.ipynb` - Contains the UNet model used to segment the Neubauer Chamber cells, taken from [here](https://github.com/milesial/Pytorch-UNet). This notebook is only imported into other notebooks
* `Model Training.ipynb` - Notebook used to train the UNet model. Implements two difference loss functions, one using only Dice Loss (taken from [here](https://github.com/marshuang80/cell-segmentation/blob/master/loss.py)) and another using a modified Dice Loss function (taken from [here]( https://kornia.readthedocs.io/en/v0.1.2/_modules/torchgeometry/losses/dice.html)) combined with Cross Entropy Loss.
* `Neubauer Cell Counting.ipynb` - The notebook used to evaluate the UNet and Cell Counting on the unlabelled test set. 
* `Square detection-func.ipynb` - This notebook combines the automatic (unsupervised) square detection of a Nuebauer Chamber image, and the trained UNet to segment and count each cell in an image. This then returns the cell concentration per cell.
* `Square detection-manual square.ipynb` - Does the same as the notebook above, but this notebook requires a reference square to be drawn in the image (covering one of the Neubauer chamber squares). It then returns the cell concentration per cell.
