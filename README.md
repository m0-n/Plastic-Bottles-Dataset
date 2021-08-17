# 5,592 Plastic Bottles in Rivers Dataset

<img align="right" src="https://i.imgur.com/nSHYBkQ.png">

This dataset contains 5,592 labeled plastic bottles in rivers. It can be used to build a object detection model to detect and quantify plastic pollution in rivers.

## Quick Start (with Dataset)
To download the dataset, simply clone the repository (ca. 2.6 GB):

<kbd>[git clone https://github.com/m0-n/Plastic-Bottles-Dataset](#)</kbd>

Alternatively, <a href="https://github.com/m0-n/Plastic-Bottles-Dataset/archive/master.zip">click here</a> for a ZIP file. 

After download, delete this readme.

## Quick Start (with Model)

If you don't want to train your model or just want to get started quickly, you can download a model trained on the dataset here: https://github.com/m0-n/Plastic-Bottle-Detection-Models

The model graph is available as TensorFlow Protobuf and TensorFlow Lite. 

## Background
Rivers as vehicles for plastic transport remain understudied in the context of global plastic pollution emissions. This work presents a prototype of a model that can detect plastic objects in rivers which can be used on resource-constrained devices without internet connection.

Estimates on how much plastic is emitted by a river mainly rely on mathematical models that consider the size of cities near the river, their development level and more. This is not very granular, as only a monthly estimate for the output of a whole river or city is given. This makes the data often not very actionable insight, because the most polluting rivers tend to also be very long, which makes it hard to know where to start exactly. The data is also statistically infered, not measured in the real world and reflects what we think is realistic not what actually is. 

## Model performance
My own model trained on the dataset achieved an average precision of 0.541 with precision of 92% and recall of 42%  on a holdout-set of static images of the same dataset. Performance can generally be expected to decline with distance. Real-world performance may be lower than on the holdout-set as images can be expected to be more different than the training set. 

Tiling (e.g. 3x3) was shown to be highly effective in improving average precision. Thus, when device performance permits, split camera input in 3x3 tiles and run inference on all simultaneously. The model is suited for edge devices, such as the Raspberry Pi.

<div align="center">
  <b>Bias-Variance Tradeoff</b><br />
<img src="https://i.imgur.com/fhZ6CaE.jpg" width="600px">
</div>

<div align="center">
<img src="https://i.imgur.com/x1Sfuny.jpg" width="600px">
</div>
  
 <div align="center">
  <b>Model performance comparison with different preprocessing (all models Google Cloud AutoML):</b><br />
  
| Preprocessing used        | TT\*\* |Conf. tresh.  | Precision | Recall   | Avg Precision\*\*\* |
|:---------------------------|:-------|:-------------|:----------|:---------|:--------------------|
| None                       | 4h     | 0.07         | 55.2%\*   | 48.7%\*  | 0.38                |
| 3x3 Tiling                 | 4h     | 0.22         | 56.5%\*   | 59.1%\*  | 0.54                |
| Mosaic                     | 4h     | 0.27         | 55.9%\*   | 48.6%\*  | 0.43                |
| Random rotation            | 4h     | 0.20         | 49.6%\*   | 50.4%\*  | 0.36                |
| 5x5 Tiling                 | 4h     | 0.22         | 62.0%\*   | 57.7%\*  | 0.54                |
| 3x3 Tiling + auto-orient   | 4h     | 0.22         | 45.3%\*   | 55.24%\* | 0.48                |
| 3x3 Tiling + contrast      | 4h     | 0.22         | 66.0%\*   | 54.6%\*  | 0.52                |
| 3x3 Tiling (final model)   | 11h    | 0.22         | 56.5%\*   | 59.1%\*  | 0.54                |


\*at 0.01 IoU \*\*training time (node hours) \*\*\*area under curve at
0.5 IoU
</div>
  
The final model with 3x3 tiling preprocessing performed 42.1\% better than the baseline with no preprocessing with an area under curve of 0.54 instead of 0.38.

I believe the effectiveness of tiling on our data was due to the input images being quite large with a median image ratio of 3024x3096. Without tiling, input images were probably down-sampled before training and thus lost information on smaller bottles. This would also explain why 5x5 tiling did not perform better than 3x3 tiling. 

Using a mosaic preprocessing step gave the model a boost of 13.1\% compared to the raw data. Random image and label box rotation reduced performance by 5.3\%. 

Auto-orienting images (discarding the exif-meta data in the images) along with 3x3 tiling did perform 11.2\% worse than just using tiling. 

Increasing contrast with histogram equalization did not have a strong effect on model performance with a decrease of 3.8\% compared to using tiling alone. 
At the end, there were three models with identical precision scores and it would have also been possible to pick one of the other two as the final model. 

The package size was about 2.8MB for all models. The models were optimized for accuracy and the processing speed / frames-per-second at inference time was not taken into account. Pruning one of these models and using it with TensorFlow Lite may result in (presumably slightly) lower accuracy. 
During training, model loss fell quickly within the first 2-3 hours. Increasing training time was only attempted for the best-performing approach, but was stopped early after 11 hours (24 hours were scheduled), as no further reductions in loss could be realised at that point. That model did not do better than the same model trained just for 4 hours. 


## Data gathering

The instructions for the photographers were:
* Always point the camera in a 90-degree angle relative to the river
* Try to photograph a little bit from above
* Do not use the zoom of your camera
* Take a lot of pictures in different places (at least 50x pictures in each place, wait at least 5 seconds between two pictures).  
* In general, don’t wait for the perfectshot, but take many (hundreds).
* Try to make pictures at different times in the same location (e.g.:  after sunset,around noon, afternoon etc.)

During the data gathering, the photographers were give nexamples  of  good and  bad  images  from  the  pool  they  sent  in  and  edge  cases  were discussed.   The data gathering / picture taking process took roughly two months of work.  Pictures were mostly taken from the side of a river.  This means, for example, that the dataset maybe  less  suitable  for  e.g.   aerial  surveillance.   

No  images  were  taken  during  nighttime or during bad weather conditions.  While some variance of the time of day naturally occurred, all images were taken during daylight. Camera zoom was intentionally not used in order to cover a large variety of dis-tances.  This means, that are a significant number of images where the plastic bottle is very far away and may only be visible upon a close look and/or using zoom.  I hope to increase the odds that a machine learning system can detect these as well, enabling surveillance of larger rivers. I estimate the bottles farthest away in the dataset have a distance of about 50-60 meters to the camera.  At this point, even with zoom, a human has problems classifying the object in the picture – it is still clearly distinct from the water surface, but not easily separable e.g. from a bird. The variety of our dataset means there is also a lot of variance in the number of bottles represented in an image.  

There are images with bottles swimming freely as well as bottles that are relativelystationary. All bottles are photographed either on river water or on other pollutionobjects,  including  more  bottles.  No  bottles  have  been  photographed  on  land. The images  were  taken  with  different  devices,  both  mobile  phones  and  cameras.   Due  to this, the images generally have different resolutions.  No tripod has been used for any pictures and the height from which the pictures were taken may variate slightly as well as the angle of the camera.

## Dataset contents

 | Attribute  | Value  |
|:----------|:-----------|
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


<b>Contents by folder:</b>

|  Folder Id |  Country | Images |  Labels |
|:----------|:-----------|:-------|:-------|
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


A  total  of  c. 15.000  images  have  been  taken  during  the  data  gathering  process. Many of these images were near duplicates. This was due to the photographers taking many images directly after each other over the course of a few seconds.  I removed these near duplicates manually by going through every image. This  step  was  responsible  for  an  order-of-magnitude  reduction  in  the  number  of images.  However, a different angle on the same bottle did qualify as a distinct bottle and was not marked as a duplicate.  During deduplication, some images were rotated to  fit  the  perspective  of  a  human  standing  on  that  spot. Rotation  was  not  used  tocreate more data (so when a rotated image was used, the original was removed from the dataset).


## Labeling Process and Statistics
The images remaining after deduplication were  labeled using labelImg. Every plastic bottle in every picture was tagged  with a rectangular label and one round of checking by a different person was done.

The number of plastic bottles per picture varies significantly. There are 239 images with just one bottle, 190 with two, 125 with three, 84 with four, 60 with five, 51 withsix, 46 with seven and 40 images with eight bottles.  A group of 164 images has ninebottles or more.  This is shown in below figure which shows the distribution ofthe number of labels across all images.  The group with nine and more bottles in eachimage makes up a total of 53.9% (3,014) of all labels.

<div align="center">
<img src="https://i.imgur.com/gPljx1T.jpg" width="700px">
</div>

In below figure  let's look at the number of images and labels in each folder, with the y-axis being the log(count) of images and labels and the x-axis is the id of the session/folder.  This shows us the number of images as well as the number of labels for each subfolder of our dataset. This underlines that some folders have many more labels (both in absolute numbers and on a per-image basis) as others.

<div align="center">
<img src="https://i.imgur.com/2xtGY0G.jpg" width="700px">
</div>

This means there is significant variance between the sessions in terms of the number of images as well as in the number of labels. The distribution of images and labels on a per-country level is shown below:

<div align="center">
<img src="https://i.imgur.com/XG4i10P.jpg" width="700px">
</div>

The variance in the image to labels ratio is not a reflection on the individual countries’ pollution status, but due to the photographer’s performance and settings.

For example, many of the pictures in Bosnia were taken from a very large river and from great distance, showing a lot of bottles in a river section, mainly because the river section is very large. This also leads to the individual bottles being very small.  By contrast, pictures from Sudan generally showed a smaller section of a river, leading to pictures with generally less bottles in it.
The differences in the number of pictures for each country are due to different levels of productivity of the photographers, with the most productive ones delivering many times more useable pictures per workhour than the others. 


The average image size in the dataset is 11.25mp, with a minimum of 0.38mp and a maximum of 48mp. The median image ratio is 3024x3096 pixels.

The width and height distribution is sketched below.
<div align="center">
<img src="https://i.imgur.com/sYifgQl.png" width="500px">
</div>

A label heatmap on the dataset shows that bottles tend to be more present in the center of pictures, but with plentiful exceptions. 

This is expected as humans tend to place the objects they want to photograph more towards the center of the picture frame. 

<div align="center">
<img src="https://i.imgur.com/LYz610c.png" width="500px">
</div>

If there are any mistakes or bottles missing, I encourage readers to inform me about their changes (e.g. make a pull request) and I will update the dataset and give credit for any amends made.


## Preprocessing Suggestions

The dataset in this repository has _not_ been preprocessed, these are suggestions before training.

I used  2x2 and 3x3 tiling for preprocessing the data to create more training data and to increase the relative size of the bottles in the picture frame. 

<img src="https://i.imgur.com/QfoDSuw.jpg" width="500px">

I also tried mosaic preprocessing, which was not effective. 


<img src="https://i.imgur.com/J5Q6THk.jpg" width="500px">


I tried other forms of preprocessing, such as random image box rotation and random label box rotation. The idea was to make the model generalize better to different camera positions by rotating the image by a random value between -15 degrees and +15 degrees  However, this did not work well and these approaches was discarded as they did not improve accuracy.

<img src="https://i.imgur.com/2iRKjkN.jpg" width="500px">


I also tried to increase the contrast of the images by using histogram equalization after the tiling step. Histogram equalization is a technique to improve contrast in images, by spreading out more frequent intensity values (e.g. a certain color). This leads to a higher contrast overall in the picture and in particular in areas of previously low contrast.

<img src="https://i.imgur.com/qRv6Yr9.jpg" width="500px">

A few examples of contrast-enhanced images are provided below:


<img src="https://i.imgur.com/dAbMD3X.jpg" width="500px">

Adding contrast seemed like a good idea, because there should be contrast between the bottles and the water, but it may be low. Reinforcing the contrast, so I thought, may lead to the model recognising the unique shape of the plastic bottle better, as the lines / separation from the background would be more visible. However, that outcome did not materialize and the contrast enhancement was removed from the preprocessing. 

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


