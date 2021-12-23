# Unsupervised Droplet Counting and Classification, and Neubauer Chamber Automation
**TeamSnorlax:**
* Medya Tekes
* Ruben Burdin
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

## 🚀(spoiler) Use the tools in seconds with our public Docker images.
Lightning fast. No libraries required. All models are pre-trained.
Using the docker images is recommended to use the tool or to have a clean and short version of the whole project. All other elements made available in the github repositopry and Google Drive data storage are for independent model training and reproducibility. The models in the Docker images are pretrained and corresond exactly to the ones mentionned and developped by the author of the research paper.

User guide:
1. Install docker in your local device (to do only once).
Go to [Docker official website](https://www.docker.com/products/docker-desktop).

2. Run the container with a single command on the command line.

### For the Droplet Segmentation and Classification:


    docker run -it -v $PWD/leonie_input_data:/usr/src/app/input_data rubenburdin/epfl-droplet-classification

    #where “$PWD/leonie_input_data” is the folder address where the images to be annotated are located.

The annotated images will be located into a new “annotated_images” folder into the original image folder, with a summary excel sheet! 🚀
References: https://hub.docker.com/r/rubenburdin/epfl-droplet-classification 

That's it! 🥳

<br />

## Installation and Requirements

### Requirements

#### Data
This project involved using two separate datasets - one for the Unsupervised Droplet Counting and Classification and another for the Neubauer Chamber Automation. Due to the data augmentation methods we used, these datasets have become quite large so we instead host them in a Google Drive. The full data and models are available at https://drive.google.com/drive/folders/179HAtF0pKPRG7f6U2cTufaUGVEhyzO2Q.
For the Unsupervised Droplet Counting and Classification:

* Download the data from https://drive.google.com/drive/folders/1Yo-KIokmTKfmPn24HVe8RVNiXe54eG08, and place inside the `Project 1 - Unsupervised Droplet classification/` folder.

For the Neubauer Chamber Automation:

* Download the 2 folders in https://drive.google.com/drive/folders/1YSCyHa7qYJeBbobsf_tAgTVp4repoytO, and place them both inside the `Project 2 - Cell counting in Neubauer Chambers/`folder. This data set is quite large, around 4 Gigabytes.

##### Description of the folders in the [Public Google Drive](https://drive.google.com/drive/folders/179HAtF0pKPRG7f6U2cTufaUGVEhyzO2Q)

    Snorlax Public Data
    ├── Droplet Detection
    │   ├── data_droplets
    │   │   ├── droplets_original_annotated #contains annotated images after the processing
    │   │   └── droplets_original_not_annotated #contains original images as handed in by the laboratory
    │   │   ├── extracted_droplets_test_labelled #segmented droplets labelled (1000 images)
    │   │   └── extracted_droplets_train_unlabelled #training set of images, unlabelled for unsupervised learning
    │   └── models #contains the pre-trained models necessary for further research development
    ├── Cell Counting Neubauer
    │   ├── models #contains pre-trained UNet models
    │   ├── Data Set 
    │        ├── Originals
    |            ├── Images #contains original images taken from Instagram
    |            ├── Masks #contains the masks for the original images taken from Instagram
    │        ├── Square detection
    |            ├── Cropped-augmented-norotation #contains augmented image set used to test square detection algorithm
    |            ├── Results #contains the results of square detection algorithm on augmented set
    |            ├── Manual squares #contains examples for the alternative approach with manually drawn square detection algorithm
    │        ├── train_augmented
    |            ├── images # contains the augmented set used in model training for cell detection/counting
    |            ├── masks # contains the masks for the augmented set used in model training for cell detection/counting
    │        └── 
 

#### Installation
This project is based entirely on Jupyter Notebooks. To run these, make sure you have Anaconda installed on your machine. All the requirements should be already met, but if not there are some `!pip install ` commands in the notebooks for any extra requirements. This entire project was done using Google Colab, so there should be no issues when run from there.

We also provide some **Public Docker images** hosted on [DockerHub](https://hub.docker.com/u/rubenburdin)


## Project Layout
Since this project contains two sub-projects, we have split the GitHub to make this easy to follow. 

### Project 1 - Unsupervised Droplet Counting and Classification
The first part of the project can be found in the `Project 1 - Unsupervised Droplet classification/` folder, and contains the following notebooks:

* `unsupervised_droplet_classifier_demo.ipynb` - The notebook contains the whole pipeline including the ingestion of original data, image preprocessing, droplet segmentation and droplet classification.
* `unsupervised_droplet_classification_analysis.ipynb` - The notebook contains all the image preprocessing code, and code snippets that have been used to create different models and evaluate them.

### Project 2 - Neubauer Chamber Automation
The second part of the project can be found in the `Project 2 - Cell counting in Neubauer Chambers/`folder, and contains the following notebooks:

* `Data Augmentation.ipynb` - The notebook used to create the Augmented Data set from the original Instagram dataset
* `DataSets.ipynb` - Contains the Pytorch Dataset class to load the data to train the UNet model. It is a static notebook, and is only used when imported into the other notebooks
* `UNetModel.ipynb` - Contains the UNet model used to segment the Neubauer Chamber cells, taken from [here](https://github.com/milesial/Pytorch-UNet). This notebook is only imported into other notebooks
* `Model Training.ipynb` - Notebook used to train the UNet model. Implements two difference loss functions, one using only Dice Loss (taken from [here](https://github.com/marshuang80/cell-segmentation/blob/master/loss.py)) and another using a modified Dice Loss function (taken from [here]( https://kornia.readthedocs.io/en/v0.1.2/_modules/torchgeometry/losses/dice.html)) combined with Cross Entropy Loss.
* `Neubauer Cell Counting.ipynb` - The notebook used to evaluate the UNet and Cell Counting on the unlabelled test set. 
* `Square detection-func.ipynb` - This notebook combines the automatic (unsupervised) square detection of a Nuebauer Chamber image, and the trained UNet to segment and count each cell in an image. This then returns the cell concentration per cell.
* `Square detection-manual square.ipynb` - Does the same as the notebook above, but this notebook requires a reference square to be drawn in the image (covering one of the Neubauer chamber squares). It then returns the cell concentration per cell.
