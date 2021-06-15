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


## Data gathering

The instructions for the photographers were:
•Always point the camera in a 90-degree angle relative to the river
•Try to photograph a little bit from above
•Do not use the zoom of your camera
•Take a lot of pictures in different places (at least 50x pictures in each place, wait at least 5 seconds between two pictures).  
•In general, don’t wait for the perfectshot, but take many (hundreds).
•Try to make pictures at different times in the same location (e.g.:  after sunset,around noon, afternoon etc.)

During the data gathering, the photographers were constantly givenexamples  of  good  and  bad  images  from  the  pool  they  sent  in  and  edge  cases  were discussed.  All supervision was conducted remotely and over Slack, a chat software. The data gathering / picture taking process took roughly two months, starting inFebruary 2020 and about 200 reported work hours by the field workers.  Pictures were mostly taken from the side of a river.  This means, for example, that the dataset maybe  less  suitable  for  e.g.   aerial  surveillance.   

No  images  were  taken  during  nighttimeor during bad weather conditions.  While some variance of the time of day naturallyoccurred, all images were taken during daylight. Camera zoom was intentionally not used in order to cover a large variety of dis-tances.  This means, that are a significant number of images where the plastic bottle is very far away and may only be visible upon a close look and/or using zoom.  We hope to increase the odds that a machine learning system can detect these as well, enabling surveillance of larger rivers. We estimate the bottles farthest away in our dataset have a distance of about 50-60meters to the camera.  At this point, even with zoom, a human has problems classifying the object in the picture – it is still clearly distinct from the water surface, but not easily separable e.g. from a bird. The variety of our dataset means there is also a lot of variance in the number of bottles represented in an image.  

There are images with bottles swimming freely as well as bottles that are relativelystationary. All bottles are photographed either on river water or on other pollutionobjects,  including  more  bottles.  No  bottles  have  been  photographed  on  land. The images  were  taken  with  different  devices,  both  mobile  phones  and  cameras.   Due  to this, the images generally have different resolutions.  No tripod has been used for any pictures and the height from which the pictures were taken may variate slightly as well as the angle of the camera.

## Dataset contents

<div id="tab:my-table">
  
  |           |            |
|:----------|:-----------|
|           |            | 
| Total images: | 5,592    | 
| Avg. bottles per image:       | 5.6    |
| Image format       | JPG  |
| Total image file size:      | 2.6 GB  |
| Photographed in:       | 34 Sessions    |  
| Countries of rivers:       | Bangladesh, Bosnia, India, Indonesia, Nepal, Pakistan, Sudan    | 
| Camera perspective:       | Side of river (mostly)      |  
| Labeling format:       | Pascal     |  
| License:       | Public Domain    |  

  </div>


By folder:

<div id="tab:my-table">

|           |            |        |        |
|:----------|:-----------|:-------|:-------|
|           |            |        |        |
| Folder Id | Country    | Images | Labels |
| 001       | Indonesia  | 14     | 62     |
| 002       | Indonesia  | 6      | 80     |
| 003       | India      | 16     | 29     |
| 004       | Nepal      | 20     | 49     |
| 005       | Nepal      | 13     | 54     |
| 006       | Pakistan   | 5      | 15     |
| 007       | Pakistan   | 56     | 341    |
| 008       | Nepal      | 5      | 17     |
| 009       | Sudan      | 5      | 9      |
| 010       | Pakistan   | 49     | 75     |
| 011       | Bosnia     | 11     | 1003   |
| 012       | Bosnia     | 15     | 27     |
| 013       | Pakistan   | 23     | 211    |
| 014       | Pakistan   | 50     | 72     |
| 015       | Pakistan   | 15     | 22     |
| 016       | India      | 42     | 60     |
| 017       | Nepal      | 9      | 72     |
| 018       | Bangladesh | 21     | 91     |
| 019       | Bosnia     | 136    | 660    |
| 020       | Bosnia     | 159    | 1464   |
| 021       | Pakistan   | 25     | 39     |
| 022       | Pakistan   | 36     | 48     |
| 023       | India      | 75     | 159    |
| 024       | Nepal      | 2      | 12     |
| 025       | Nepal      | 7      | 37     |
| 026       | Nepal      | 13     | 68     |
| 027       | Nepal      | 11     | 35     |
| 028       | Nepal      | 7      | 34     |
| 029       | Nepal      | 51     | 167    |
| 030       | Bosnia     | 55     | 396    |
| 031       | Bangladesh | 10     | 17     |
| 032       | Bangladesh | 7      | 12     |
| 033       | Bangladesh | 3      | 7      |
| 034       | Pakistan   | 27     | 148    |


</div>

A  total  of  c. 15.000  images  have  been  taken  during  the  data  gathering  process.Many of these images were near duplicates.  This was due to the photographers taking1 many images directly after each other over the course of a few seconds.  I removed these near duplicates manually by going through every image.This  step  was  responsible  for  an  order-of-magnitude  reduction  in  the  number  ofimages.  However, a different angle on the same bottle did qualify as a distinct bottleand was not marked as a duplicate.  During deduplication, some images were rotatedto  fit  the  perspective  of  a  human  standing  on  that  spot.   Rotation  was  not  used  tocreate more data (so when a rotated image was used, the original was removed from the dataset).

## Labeling Process and Statistics
The images remaining after deduplication were  labeled using labelImg. Every plastic bottle in every picture was tagged  with a rectangular label and one round of checking by a different person was done.





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


