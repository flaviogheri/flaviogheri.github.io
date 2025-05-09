---
layout: single
title: "Lunar Zebro: The First Student Led Moon Rover"
permalink: /projects/lunar_zebro/
---

Meet the Lunar Zebro, the smallest, (cutest) and cheapest Lunar rover ever!

<!-- INSERT RENDER OF THE LUNAR ZEBRO HERE -->

In this project I worked both as a Software Engineer as well as an AI engineer in the team. More specifically we created the **sprint team** (TRAICI) focused on spearheading the development of the rover towards the IAC Milan conference.

In this project we had to develop a rock segmentation stack for the rover, as well as a general software restructuring of the code base to make it work reliably for an extended duration of the conference.

The project ended as a great success, winning the **Best Innovative Booth Award at IAC**. Although my contribution for the team has finished since the conference, the Lunar Zebro is progressing towards creating this lunar rover.

When the Lunar Zebro is launches, it provides an oppertunity to swarm the moon, gathering data at a significantly faster rate than the way it is currently done. This gives us an opportunity to expand our understanding of the universe and potentially discover resources for future space missions.

Small space rovers have the potential to explore vast amounts of area in swarms and can be deployed for search and rescue missions, mapping, radio astronomy and so on.

Obstacle avoidance is an essential part of traversing the lunar surface and since the Lunar Zebro is equipped with cameras to perceive its surroundings, it should come with a computer vision algorithm that can perform object detection. It is important that this algorithm is robust since hitting a rock could mean the end of a rover's life.

However, the energy supply on the moon is limited to solar energy. Many current Lunar perception applications use active sensors which in turn are eneergy expensive. Some classical computer vision techniques with passive sensors do exist (such as image processing with cameras), however as Lunar Zebro has a unique point of view, rock detection techniques more robust to dataset variance need to be found.

In this project, we evaluate several Deep Learning models whilst taking the energy consumption of the model into account in the evaluation. Of course we still require sufficient detection results.

## 2. Related Work

-----------------------

### Traditional Rover Obstacle Avoidance

Originally most algorithms used laser-based obstacle detection for most obstacle detection systems, with some rovers additionally equipping cameras for additional sensor redundancy. Nonetheless, as the lunar zebro is deploying a very small lunar rover with a very small energy supply, it will only operate with passive sensors (that is with two cameras). The team plans to use the KissCAM V1.0, although a SpaceGrade Camera, it holds a very poor camera resolution (480x360) [1]. In addition to this, the Lunar Zebro team has not yet developed any such rock detection algorithm.

### Existing Computer Vision algorithms for rock detection

Existing literature for lunar rock detection through computer vision exists in four main categories: 3D Point Clouds, Edge-Based Methods, Pixel-level Segmentation and Traditional Machine Learning Techniques [2].

**Disparity Image Detection:** This method uses disparity images in order to quickly retrieve objects that are distinct from the background, and combines the technique with traditional image processing in order to locate the rocks.

**Edge-based Methods:** This method uses traditional image processing techniques, such as Canny edge detection to identify more 'circular' or 'oval' shapes that are assumed to be rocks. This approach, however, is found to struggle with irregular rock shapes, and occluded rocks. Which cannot be discounted for in such a critical mission.

**Pixel-level Segmentation:** This method can detect rocks with high accuracy but is computationally expensive, making it less suitable for energy-constrained environments unless precise shape knowledge is required such as geology studies.

**Traditional Machine Learning Techniques:** These are widely used but are sensitive to the dataset as well as being outdated. Given the lack of a comprehensive dataset for the Lunar Zebro's unique perspective, deeper, more resilient networks are preferred.

### Current Challenges

As mentioned earlier, there are several unique challenges to developing a functional algorithm for the current lunar zebro. The first being that in general, there are very few lunar images for which a model can be trained upon and with no method of extracting any new data as it would rquire deploying a lunar rover. The second is that of the few real and simulated lunar images, most are from a height between 1.3-2.2m height [3]. As the lunar zebro is uniquely low, ~15cm from the lunar surface. There is likely a very different perspective change between the dataset and what it will percieve.

## 3. Experiments

To design a fitting rock detection architecture for the lunar zebro rover, we will perform three experiments with the [artificial lunar landscape dataset](https://www.kaggle.com/datasets/romainpessia/artificial-lunar-rocky-landscape-dataset) dataset.This dataset contains 9766 photorealistic images of the Moon's surface with ground truth rock segmentation. The goal is to compare several object detection models based on their performance and lightweightedness. The one that turns out to be most suitable is then subjected to a second experiment where we compare evaluate how three data augmentation techniques might increase the performance of the model. Finally, the best performing model is tested on an unseen dataset that was retrieved from the actual lunar zebro rover in a lunar testbed. All of this to contribute to the development of a robust object detection algorithm for small rovers, addressing the challenges of limited training data and perspective shift.

### 3.1 Comparing Suitability of Object Detection Models

In the first experiment, we retrain and fine-tune two established one-stage object detection models, You Only Look Once (YOLO) and Single Shot Detector (SSD). Among the various iterations of YOLO we opted for YOLOv10, released in May 2024. This latest version is said to outperform the previous ones in accuracy and speed, as can be seen in the figure below. YOLOv10 is available in multiple model scales to suit different operational needs: YOLOv10-N (Nano), YOLOv10-S (Small), YOLOv10-M (Medium), YOLOv10-B (Balanced), YOLOv10-L (Large), and YOLOv10-X (Extra-large). We will take a look at these variations, which have an increasing number of parameters and thus complexity and evaluate their performance to select the most suitable one for our case. For more details on YOLOv10, please refer to the paper [4].

Single Shot Detection (SSD) is an approach which applies various aspect ratios and scales for each location in the feature maps. This enhances its ability to detect objects with different shapes and sizes. YOLO, however, makes use of predefined grids and bounding box shapes. In our case we would like to detect rocks. Rocks exist in many different shapes and sizes. Because of this reason, we decided to consider SSD for our comparison.

The decision to use one-stage models is driven by their design advantages for real-time operation. Unlike two-stage models, which first generate region proposals before classifying them, one-stage models such as YOLO and SSD integrate these steps into a single process. This allows for faster decision-making, which in turn reduces latency. Therefore, this type of detector will be useful to perform real-time object avoidance on the lunar surface.

#### Results
The models are assessed using standard performance metrics such as precision, recall, F1-score, and mAP50 (Mean Average Precision at IoU=0.50). Additionally, we evaluate their 'lightweightedness' because it will have to operate on resource-constrained systems such as the rover. The lightweightedness of each model is analyzed based on latency, the number of parameters, and the computational efficiency, measured in Floating Point Operations Per Second (FLOPs). All the results are summerized in the tables below. Due to limited available resources only a part of the dataset was used (300 images with 2706 labeled objects).

- **Precision:** The proportion of true positive predictions among all positive predictions expressed as value between 0 and 1.
- **Recall:** The proportion of true positive predictions among all actual positive instances expressed as value between 0 and 1.
- **F1-score:** The harmonic mean of precision and recall.
- **mAP50** (Mean Average Precision at IoU=0.50): The average precision for detecting objects, using a threshold of 0.50 for the Intersection over Union (IoU). It is a measure of the model's detection accuracy and is expressed as value between 0 and 1.
- **Latency:** The time it takes for a model to process an input and produce an output. It is important for real-time applications like ours and is measured in milliseconds (ms).
- **Number of Parameters:** The total number of parameters within a model, indicating its size and complexity. The number of parameters is measured in millions (M).
- **FLOPs** (Floating Point Operations Per Second): Measure of the computational efficiency of the model, which indicates how many operations the model performs per second. In our case the FLOPs are measured in billions (G).


| **Model** | **Precision** | **Recall** | **F1-score** | **mAP50** |
|-----------|---------------|------------|--------------|-----------|
| YOLOv10-N | 0.00833       | 0.28008    | 0.84024      | 0.06773   |
| YOLOv10-S | 0.29406       | 0.33402    | 1.00206      | 0.21624   |
| YOLOv10-M | 0.54144       | 0.42739    | 1.28217      | 0.40736   |
| YOLOv10-B | 0.35745       | 0.19087    | 0.57261      | 0.15722   |
| YOLOv10-L | 0.01429       | 0.45436    | 1.36308      | 0.01047   |
| YOLOv10-X | 0.50835       | 0.33679    | 1.01037      | 0.31332   |
| SSD (MobilenetV2)      |    0.65       |  0.39      |  0.4875        | 0.36080   |


    
| **Model** | **Latency (ms)** | **Computational FLOPs (G)** | **Params (M)** |
|-----------|------------------|-----------------------------|----------------|
| YOLOv10-N | 1.84             | 6.7                         | 2.3            |
| YOLOv10-S | 2.49             | 21.6                        | 7.2            |
| YOLOv10-M | 4.74             | 59.1                        | 15.4           |
| YOLOv10-B | 5.74             | 92                          | 19.1           |
| YOLOv10-L | 7.28             | 120.3                       | 24.4           |
| YOLOv10-X | 10.7             | 160.4                       | 29.5           |
| SSD (MobilenetV2)      | 208.05            | 0.05                        | 24.83          |
    

To compare the different models in a more visual way, the graph below shows the performance of each model (amount of parameters in millions are found between brackets after every model).
<img src="https://hackmd.io/_uploads/BJuZuqnHC.png" alt="yolo results" style="border: 1px solid #DDD; padding: 5px;"> 

<div style="text-align: center;">
    <i>Precision, recall and mean average precision for YOLOv10 model scales</i>
</div>



#### Discussion
There are two aspects to discuss: performance and lightweightedness. Starting with the performance of the models you see significant variation across the scales. The YOLOv10-N (Nano) scored very poorly. In the confusion matrix below, you can see that everything was categorized as background and not a single rock was recognized. This is likely due to the limited capacity of the model with too few parameters to accurately detect and classify the rocks.

![yolo_pictures_nano](https://hackmd.io/_uploads/rJsEOzdHR.jpg)
<div style="text-align: center;">
    <i>Normalized confusion matrix (left) and sample picture of the dataset (render0008.png) with ground truth and predictions (right) of model YOLOv10-N.</i>
</div>

---
One might expect a continuous increase in performance with the addition of more parameters, but this does not seem to be the case. YOLOv10-L (Large) and YOLOv10-X (Extra-large) show a decrease in precision and recall compared to the medium model. This could be due to overfitting, where the model becomes too complex and does not generalize well. As can be seen below the model seems to be overly sensitive, predicting everything to be a rock which explains the relatively high recall to the other models. This is disadventageous because even though you rather overestimate than underestimate the amount of rocks, seeing rocks everywhere will likely lead to a standstill of the rover. 

![yolo_pictures_large](https://hackmd.io/_uploads/H1KBOzdBC.jpg)
<div style="text-align: center;">
    <i>Normalized confusion matrix (left) and sample picture of the dataset (render0008.png) with ground truth and predictions (right) of model YOLOv10-L.</i>
</div>

---

The YOLOv10-M (Medium) appears to be the undisputed winner when it comes to performance. It achieves a precision of 0.54, a recall of 0.43, leading to an F1-score of 1.28 and a mAP50 of 0.41. Although it is slightly passed by YOLOv10-L in terms of recall, the large model performs very poorly in precision and accuracy, making it less reliable overall. In the ground truth of sample render0008 below, you can also see that some rocks are not marked with a bounding box even though they are correctly predicted by YOLOv10-M, which means that the model is likely to get higher metric scores with a better labeled dataset. Overall it can be said that using the full dataset would increase robustness and perhaps also confidence scores which are now often on the lower end.

![yolo_pictures_medium](https://hackmd.io/_uploads/H1jLdGdSC.jpg)
<div style="text-align: center;">
    <i>Normalized confusion matrix (left) and sample picture of the dataset (render0008.png) with ground truth and predictions (right) of model YOLOv10-M.</i>
</div>

---

Lastly we have to discuss the lightweightedness. The Lunar Zebro rover operates on a battery capacity of 40.8 Wh, and with a Raspberry Pi 5 with a dual ARM Cortex A9 processor capable of 614 MFlops per core. The final model should be efficient enough to match these specifications and the rover's movement speed of 3 cm/s. YOLOv10-M strikes as a viable option, balacing performance and efficiency, with a latency of 4.74 ms and computational requirement of 59.1 GFLOPs. The current rover speed is of course very slow but it is likely that it increases for future missions. Therefore it is good that the model can handle 200 frames per second (fps).

The SSD does show to be a worthy contender, as the mAP50 score outperforms all YOLO's apart from the YOLOv10-M. It is notable that the amount of parameters of the SSD model are similar to the YOLOv10-L model. However, the amount of FLOPs is significantly lower. This might be due to this model converging to a more sparse solution. The high latency is most likely due to the different GPU's used for the tests with the YOLO models and the test with the SSD model. At 0.05 GFLOPS the SSD model is the undisputed winner when considering energy usage of the model! However, when looking at some of the predictions made by the model, it looks like it has an abundance of False Negatives. YOLOv10-M looks like it has less False Negatives.
<div style="display: flex; justify-content: space-around; align-items: center; text-align: center">
    <img src="https://hackmd.io/_uploads/rkexPO3rA.jpg" alt="Image 1" style="max-width: 50%; height: auto; margin: 10px;">
    <img src="https://hackmd.io/_uploads/S1llPO2BR.jpg" alt="Image 2" style="max-width: 50%; height: auto; margin: 10px;">
</div>
<div style="text-align: center;">
    <i>Two samples of predictions made by the SSD. The left shows some pictures with proper detections. The right shows many rocks of significant size undetected.</i>
</div>

---
Based on this evaluation we will continue to do the next two experiments with YOLOv10-M to see if the accuracy can be improved with data augmentation and how well the model performs with unseen, actual data from Lunar Zebro.

### 3.2 Comparing different data augmentation methods

The limited datasets of lunar rocks can be enhanced through data augmentation to improve the robustness of the model. Continuing with the best model from the previous experiment (YOLOv10-M), three augmentation techniques will be evaluated: warping, histogram adjustment, and the pooling trick. 

- **Warping:** Distorting the image by pulling the two upper corners towards the center to enhance the model's ability to recognize lunar rocks from various angles and shapes.
- **Histogram:** Modifying the distribution of pixel intensities in the image to improve contrast and brightness of some features for better detection.
- **Pooling trick:** Cutting the image into strips and rearranging them to create several new variations with the purpose to make the model more generalizable as it creates new shapes and orientations of the rocks.

<h4 style="text-align: center;">Warping</h4>

Warping involved transforming the image, shrinking the reducing the top rows by 30% and performing cubic interpolation from the top downwards, thereby warping pixels into a trapezoid shape. This transformation was also applied to the bounding boxes to ensure accurate labeling of the newly stretched areas. However, unlike this example where images were cropped to simulate perspective changes, the dataset images were not cropped to avoid losing data outside the crop boundaries.

<!-- HTML within Markdown for side-by-side images -->
<div style="display: flex; justify-content: space-around; align-items: center;">
    <img src="https://hackmd.io/_uploads/rJN86H2HR.png" alt="Image 1" style="max-width: 70%; height: auto; margin: 10px;">
    <img src="https://hackmd.io/_uploads/SJQJaBnSA.png" alt="Image 2" style="max-width: 70%; height: auto; margin: 10px;">
</div>

<h4 style="text-align: center;">Histogram Equalization</h4>

Given that the dataset comprises simulated lunar landscapes, notable differences exist compared to real images, particularly in the distribution of pixel intensities. To address this, a pre-processing, namely histogram equalization of any image input (real and simulated) aims to equalize images to achieve similar appearances across both simulated and real datasets. This not only enhances visual uniformity but also potentially improves model performance by amplifying input pixel differences, leading to more significant gradients.

However, an analysis revealed a bias towards dark pixels in the images, which could potentially oversaturate them during equalization. To mitigate this, an approach excluding the lowest 25 pixel values (very dark pixels) was explored. The image and histogram comparison below illustrate this adjustment.

<div style="display: flex; justify-content: space-between; align-items: center;">
    <img src="https://hackmd.io/_uploads/BkPGmK2SA.png" alt="Image 1" style="width: 30%; max-height: 200px;">
    <img src="https://hackmd.io/_uploads/r1GHLthBC.png" alt="Image 2" style="width: 70%;">
</div>
<div style="text-align: center;">
    <i>Left: Regular histogram equalization shows excessive brightness levels, obscuring rocks.
Right: Our algorithm, excluding the lowest 25 pixel intensities (center), compared to normal histogram equalization (right).</i>
</div>




<div style="display: flex; justify-content: space-between; align-items: center;">
    <figure style="width: 70%; text-align: center;">
        <img src="https://hackmd.io/_uploads/H1nI3S2rA.png" alt="Image 1" style="width: 100%;">
        <figcaption>Original Image</figcaption>
    </figure>
    <figure style="width: 70%; text-align: center;">
        <img src="https://hackmd.io/_uploads/Hkq7hSnBA.png" alt="Image 2" style="width: 100%;">
        <figcaption>In-house Equalization</figcaption>
    </figure>
</div>
<div style="text-align: center;">
    <i>Left: Dataset image. Right: Our histogram equalization improves rock contrast, as expected (see bottom right of images).</i>
</div>


<h4 style="text-align: center;">Pixel Pooling</h4>


Finally, pooling was applied to able to increase the training dataset whilst also allowing for a better similarity between the training data and the real lunar data. A simple pooling method that took a set column and row number was implemented. In future a more random pooling technique is to be used in order to better simulate noise.

<div style="display: flex; justify-content: space-between; align-items: flex-end;">
    <div style="width: 38%; text-align: right;">
        <img src="https://hackmd.io/_uploads/BkQKaSnrR.png" alt="Image 1" style="max-height: 200px;">
    </div>
    <div style="width: 70%;">
        <img src="https://hackmd.io/_uploads/SJA5pS2S0.png" alt="Image 2" style="width: 100;">
    </div>
</div>
<div style="text-align: center;">
    <i>On the left the "even-even" pooled image and on the right is the original image.</i>
</div>




#### Results

The three techniques will be compared based on same performance metrics as in the previous experiment, accuracy, precision, recall, and F1 Score. 

| **Augmentation Technique**     | **Precision** | **Recall** | **F1-score** | **mAP50** |
|---------------|---------------|------------|--------------|-----------|
| YOLOv10-M without augmentation | 0.54144       | 0.42739    | 1.28217      | 0.40736   |
| YOLOv10-M with Warping       | 0.11534       | 0.35741    | 1.07223      | 0.0707    |
| YOLOv10-M with Histogram     | 0.01157       | 0.58268    | 1.74804      | 0.00898   |
| YOLOv10-M with Pooling Trick | 0.4971        | 0.36771    | 1.10313      | 0.34467   |

#### Discussion


Based on the findings, augmentation techniques notably diminished the model's performance. Particularly, histogram equalization, intended to enhance performance as a preprocessing method, it did not yield improvements and will not be implemented in the final dataset. A reason for this discrepancy is that histogram equalization enhances contrast primarily on smaller rocks, which are not labeled in the dataset used, resulting in further loss. However, it should be noted that the overall model performance is sufficiently low that the absence of certain labels does not fully explain the situation and further evaluation should be made.

Regarding image warping, compression sensitivity was evident upon image inspection. Future evaluations should consider a cropped perspective to assess potential impact. Overall, although preprocessing techniques showed some differences, the notable decrease in performance, particularly in recall, suggests that data augmentation may not be beneficial at all, especially in compairison to what was originally anticipated. Confusion matrices for each test and example results are provided below for reference.





![warping](https://hackmd.io/_uploads/ry7Qn52B0.png)
<div style="text-align: center;">
    <i>Normalized confusion matrix (left) and sample picture of the dataset (render0008.png) with ground truth and predictions (right) of model YOLOv10-M with warping.</i>
</div>


![histogram](https://hackmd.io/_uploads/H1bQ393H0.png)
<div style="text-align: center;">
    <i>Normalized confusion matrix (left) and sample picture of the dataset (render0008.png) with ground truth and predictions (right) of model YOLOv10-M with histogram preprocessing.</i>
</div>

![pooling_trick](https://hackmd.io/_uploads/HJzQnq3HA.png)
<div style="text-align: center;">
    <i>Normalized confusion matrix (left) and sample picture of the dataset (render0008.png) with ground truth and predictions (right) of model YOLOv10-M with pooling trick.</i>
</div>


### 3.3 Evaluate best performing model architecture on real dataset
Validate the effectiveness of the proposed approach with the physical rover.
To try and replicate the real-life scenario of a deployed lunar-zebro as well as possible. We took a prototype to the lunar test bed, which is located at the API building on the TU Delft campus. There, we took about 60 pictures of different scenarios with rocks on the testing bed. Then, we annotated the dataset using roboflow. Now, we will use the best scoring model from the previous sections and evaluate it on this dataset.
<div style="display: flex; justify-content: space-around; align-items: center; text-align: center">
    <img src="https://hackmd.io/_uploads/BkRhAOhH0.jpg" alt="Image 1" style="max-width: 50%; height: auto; margin: 10px;">
    <img src="https://hackmd.io/_uploads/HyJaC_3r0.jpg" alt="Image 2" style="max-width: 50%; height: auto; margin: 10px;">
</div>
<div style="text-align: center;">
    <i>Two samples the lunar test bed dataset.</i>
</div>


#### Results
| Ideal Model  | Precision | Recall | F1-score | mAP50 |
|--------|-----------|--------|----------|----------|
| YOLOv10-M without augmentation | 0.54144       | 0.42739    | 1.28217      | 0.40736   |
| Real Test Data | 0.1791	|0.5691	| 0.2725	| 0.1577


#### Discussion
Unfortunately, it seems as if the model performs significantly better on other samples from the same dataset as it was trained on.
<div style="display: flex; justify-content: space-around; align-items: center; text-align: center">
    <img src="https://hackmd.io/_uploads/HkGyXn3r0.jpg" alt="Image 1" style="max-width: 50%; height: auto; margin: 10px;">
    <img src="https://hackmd.io/_uploads/ry5kV2hH0.jpg" alt="Image 2" style="max-width: 50%; height: auto; margin: 10px;">
</div>
<div style="text-align: center;">
    <i>Left: Confusion matrix with a confidence threshold of 0.75. Right: Note that the precision significantly peaks at 0.9.</i>
</div>

In the confusion matrix above as well as the images below, we can see that the amount of False Positives are particularly high with these settings. At the same time, the recall is close to 0.5, which only shows that the model is not very good at differentiating between rock and not-rock (As if it is flipping a coin).

<div style="display: flex; justify-content: space-around; align-items: center; text-align: center">
    <img src="https://hackmd.io/_uploads/ryxrXnnSR.jpg" alt="Image 1" style="max-width: 50%; height: auto; margin: 10px;">
    <img src="https://hackmd.io/_uploads/rJ4SQ22rA.jpg" alt="Image 2" style="max-width: 50%; height: auto; margin: 10px;">
</div>
<div style="text-align: center;">
    <i>Two samples the lunar test bed dataset.</i>
</div>

The images make it even more clear that the model is making many guesses of rocks, except for the correct rocks. Whenever there is a large, obvious rock in the image, it still fails to see it, but it does classify many small pebbles, which this dataset did not include, as rocks. 

## 4. Conclusion and Further Work
We have performed a comprehensive research to determine which combination of model and data augmentation would perform the best for rock detection on a lunar surface. We have found that the best performing model is YOLOv10-M, with SSD with MobilenetV2 backbone a close runner-up. However, SSD did show a significantly lower amount of Floating Point operations than YOLOv10-M.

To enhance the model's adaptability to diverse rover perspectives and real lunar images, we conducted tests on multiple data augmentation techniques including histogram equalization, pixel pooling and perspective warping. Ultimately, however, none of these techniques yielded the expected improvements, leaving us to exclude them from the final training and testing on the real rover dataset.

In the end, we chose the best model to view it's performance on our lunar test bed dataset. The results showed a significant decrease in performance on the lunar test bed dataset as compared to other rendered images.
### 4.2 Further Work
Due to time constraints, the datasets shown have only been trained on 300 images out of the 9000 image dataset and we have only performed one epoch. Increasing the size of the dataset or the amount of epochs simply takes too much time that we did not have to fit the constraints of this assignment. This means that the full potential of the model is not shown in the metrics presented by this blogpost. The first step for improvement is to make a proper comparison between these models by training with the full dataset on a large amount of epochs.

We also recognize that we did use relatively large models in our comparison. There might be models out there that could show to be a better fit for the lunar zebro due to the energy consumption constraints. Thus, for further work we intend to compare different models with less parameters to see if these can still get decent enough results.

Finally, the data was created by using a dataset of renders of lunar surfaces which has been labeled with segmentation. Since we required bounding boxes for our labels, we have used opencv to draw the boxes around the contours found in the segmentation. This has lead to the data labels missing certain rocks. The labels of the dataset being off many times, might be the main driving factor behind our disappointing results. For future work we aim to spend some time to create a properly labeled dataset with lunar images. With this new dataset we do not rule out to try to perform the data augmentation again.

## References
[1] MVP Aerospace, 'KissCAM Datasheet and User Manual', 2024.

[2] B. Kuang et. al., 'Rock Segmentation in the Navigation Vision of Planetary Rovers', MDPI, 2021

[3] NASA, "Mars Science Laboratory: Curiosity Rover", https://science.nasa.gov/mission/msl-curiosity/, 2024

[4] A. Wang et al., ‘YOLOv10: Real-Time End-to-End Object Detection’, arXiv [cs.CV]. 2024.
