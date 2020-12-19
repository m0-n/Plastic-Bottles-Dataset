# 999 Images of Plastic Bottles in Rivers Dataset
<img align="right" src="https://i.imgur.com/nSHYBkQ.png">

This data repository contains 999 images of plastic bottles in rivers, with 5,592 labeled bottles, taken in seven countries (Bangladesh, Bosnia, India, Indonesia, Nepal, Pakistan, Sudan). It contains the image data and labels in 34 subfolders. 

The purpose of the dataset is to enable novel applications and research at the intersection of machine learning and ecology. For example, it can be used to build a custom object detection model to detect and quantify pollution in rivers.

## Usage
To download the dataset, simply clone the repository (ca. 2.6 GB):

<kbd>[git clone https://github.com/m0-n/Plastic-Bottles-Dataset](#)</kbd>

Alternatively, <a href="https://github.com/m0-n/Plastic-Bottles-Dataset/archive/master.zip">click here</a> for a ZIP file. 

After download, delete this readme. 

## Support
To receive support when using this dataset, please open a new issue thread and use the label <kbd>[question](https://github.com/m0-n/Plastic-Bottles-Dataset/labels/question)</kbd>. This project is actively supported and you can expect a reply in a day or two.

## Model performance
A preliminary model trained on the dataset achieved an average precision of 0.541 with precision of 92% and recall of 42%  on a holdout-set of static images of the same dataset. Performance can generally be expected to decline with distance. Real-world performance may be lower than on the holdout-set as images can be expected to be more different than the training set. 

Tiling (e.g. 3x3) was shown to be highly effective in improving average precision. Thus, when device performance permits, split camera input in 3x3 tiles and run inference on all simultaneously. The model is suited for edge devices, such as the Raspberry Pi.

<img src="https://i.imgur.com/fhZ6CaE.jpg" width="500px">
<img src="https://i.imgur.com/x1Sfuny.jpg" width="500px">


## Showcase
To showcase your research (any academic / non-academic projects), please open a new issue thread and use the label <kbd>[showcase](https://github.com/m0-n/Plastic-Bottles-Dataset/labels/showcase)</kbd>. Please feel free to also post early-stage projects and even ideas and link any relevant papers.


## Feedback
Comments and feedback is always appreciated. Pull requests, for example with corrections or additional data, are very welcome and will be reviewed in a timely manner. Please use the label <kbd>[feedback](https://github.com/m0-n/Plastic-Bottles-Dataset/labels/feedback)</kbd> for feedback and general comments.

## License
The data is available under a <a href="https://wiki.creativecommons.org/wiki/public_domain">public domain license</a> and free to use by anyone without any restrictions.

## Example Detections
<img src="https://i.imgur.com/aZz7Gjo.jpeg">


