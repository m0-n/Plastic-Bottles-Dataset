# 999 Images of Plastic Bottles in Rivers Dataset
<img align="right" src="https://i.imgur.com/nSHYBkQ.png">

This data repository contains 999 images of plastic bottles in rivers, with 5,592 labeled bottles, taken in seven countries (Bangladesh, Bosnia, India, Indonesia, Nepal, Pakistan, Sudan). It contains the image data and labels in 34 subfolders. 

The purpose of the dataset is to enable novel applications and research at the intersection of machine learning and ecology. For example, it can be used to build a custom object detection model to detect and quantify pollution in rivers.

## Quick Start (with Dataset)
To download the dataset, simply clone the repository (ca. 2.6 GB):

<kbd>[git clone https://github.com/m0-n/Plastic-Bottles-Dataset](#)</kbd>

Alternatively, <a href="https://github.com/m0-n/Plastic-Bottles-Dataset/archive/master.zip">click here</a> for a ZIP file. 

After download, delete this readme. 

## Quick Start (with Model)

If you don't want to train your model or just want to get started quickly, you can download a model trained on the dataset here: https://github.com/m0-n/Plastic-Bottle-Detection-Models

The model graph is available as TensorFlow Protobuf and TensorFlow Lite. 

## Background
Rivers as vehicles for plastic transport remain understudied in the context of global plastic pollution emissions. This work presents a first prototype of a model that can de- tect plastic objects in rivers which can be used on resource-constrained devices without internet connection.

Estimates on how much plastic is emitted by a river mainly rely on mathematical models that consider the size of cities near the river, their development level and more. This is not very granular, as only a monthly estimate for the output of a whole river or city is given. This makes the data often not very y actionable insight, because the most polluting rivers tend to also be very long, which makes it hard to know where to start.

## Model performance
A preliminary model trained on the dataset achieved an average precision of 0.541 with precision of 92% and recall of 42%  on a holdout-set of static images of the same dataset. Performance can generally be expected to decline with distance. Real-world performance may be lower than on the holdout-set as images can be expected to be more different than the training set. 

Tiling (e.g. 3x3) was shown to be highly effective in improving average precision. Thus, when device performance permits, split camera input in 3x3 tiles and run inference on all simultaneously. The model is suited for edge devices, such as the Raspberry Pi.

<img src="https://i.imgur.com/fhZ6CaE.jpg" width="500px">
<img src="https://i.imgur.com/x1Sfuny.jpg" width="500px">



## Example Hardware

Model has been tested on Raspberry Pi4B (1,5 GHz 64-Bit-Quad-Core 4GB LPDDR4-3200 SDRAM 64 GB SSD, 3-4 Watt) 

The goal was to test the model on an device similar to what could be used in a real-world scenario, with limited computing power and energy supply.


<img src="https://i.imgur.com/I52XvmX.png" width="500px">



## Support
To receive support when using this dataset, please open a new issue thread and use the label <kbd>[question](https://github.com/m0-n/Plastic-Bottles-Dataset/labels/question)</kbd>. This project is actively supported and you can expect a reply in a day or two.


## Showcase
To showcase your research (any academic / non-academic projects), please open a new issue thread and use the label <kbd>[showcase](https://github.com/m0-n/Plastic-Bottles-Dataset/labels/showcase)</kbd>. Please feel free to also post early-stage projects and even ideas and link any relevant papers.


## Feedback
Comments and feedback is always appreciated. Pull requests, for example with corrections or additional data, are very welcome and will be reviewed in a timely manner. Please use the label <kbd>[feedback](https://github.com/m0-n/Plastic-Bottles-Dataset/labels/feedback)</kbd> for feedback and general comments.

## License
The data is available under a <a href="https://wiki.creativecommons.org/wiki/public_domain">public domain license</a> and free to use by anyone without any restrictions.

## Example Detections
<img src="https://i.imgur.com/aZz7Gjo.jpeg">


