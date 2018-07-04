## Introduction

In a past life I was a real estate broker. As a broker, I noticed that real estate price prediction algorithms didn't seem to adequately account for the things that most affected my clients’ purchasing behavior. My clients would spend much of their time discussing the number of trees on a block, the trash on the street, the number of abandoned houses on a block, and the construction on a block. Real estate algorithms seemed to analyze price/sq.ft, adjacency to a school, or crime in a neighborhood. All good factors to consider, but not the gritty, on the ground analysis my clients needed. Especially in redeveloping neighborhoods in old cities, young buyers are looking to purchase potential.


I listened to a podcast about a year and a half ago regarding two data scientists that trained an algorithm to identify year, make and model of vehicles on the street via Google Street View. [They were able to use this information to very accurately predict election results](images/pnas.pdf).

Fundamentally, real estate is local and grounded in the physical space directly viewable to the human eye. In Philadelphia, being a very provincial city, this is even more the case than many cities. Anecdotally, I bought a house 4 blocks away from a friend. My house cost 5 times less. It is difficult for a big picture algorithm to take into account the small details of the literal, on the ground, built environment that buyers take into account when purchasing real estate.

# Curb appeal


## Objective

Curb Appeal is my attempt to capture **one small piece** of the on-the ground factors affecting real estate prices.

**Driving Question:** Do the number of trees on a block affect real estate prices?

**Objective:** **Using a convolutional neural network, build an algorithm to count the number of trees on a block**

## Table of Contents

1. [Dataset: Collection, Preprocessing and Creation](#dataset-collection-preprocessing-and-creation)

	* [Fetch](#fetch)
	* [Label](#label)
	* [Resize](#resize)
	* [Feed Network](#feed-network)


2. [Results](#results)

	* [The Numbers](#the-numbers)
	* [The Visuals](#the-visuals)
	* [The Output](#the-output)

3. [Next Steps](#next-steps)

4. [Tech Stack](#tech-stack)

5. [Sources](#sources)





## Dataset: Collection, Preprocessing and Creation

My pipeline moves in the following fashion:

	FETCH -> LABEL -> RESIZE -> FEED

#### Fetch

I wrote [fetch_images.py](fetch_images.py) to utilize [Google Street View API](https://developers.google.com/maps/documentation/streetview/) (GSV) and [GSV meta data API](https://developers.google.com/maps/documentation/streetview/metadata) to perform operations in the following manner.

1. Given a **street name** and a **block range**, (e.g. 'N 26th st', 1300-1500 blocks) my script will **calibrate its heading**, then set the camera to take pictures at a **90 degree angle to heading*** The heading resets at the beginning of every block
<p align=“center”>
 <img alt="90 degrees" src="images/90_degrees.png" height=500>
</p>

2. Often GSV will have one picture for multiple addresses, or GSV will have the same picture for many addresses at the end of the block. In [fetch_images.py](fetch_images.py) **each picture** is **checked** against the **last picture** to make sure it is not a repeat.

3. Each original picture is saved as house number, street name, city, state and zip. E.g. '1338_n_26th_st_philadelphia_pa_19121.jpg'

4. At the end of each series of fetches, the script will **write** to a pandas data frame the **time, date, and number of fetches** and report this back to the user (GSV will allow 25,000 free images a day).

5. I selected 4 differing neighborhoods within Philadelphia. From my knowledge of the region I know that each neighborhood contained differing house architecture, street architecture and number of trees, as well as reflecting vastly different average price points. I had my function fetch all pictures from each neighborhood.


#### Label
After fetching, the process moves through [label_pics.py](label_pics.py). Label pics heavily utilizes [OpenCV](http://opencv.org/). Many thanks to the excellent OpenCV tutorials at [pyimagesearch](https://www.pyimagesearch.com/)

The OpenCV build [is specific](https://github.com/opencv/opencv_contrib) and can be installed via **'pip install opencv-contrib-python'**.

One of the **challenges** of labeling is to decide what **is a tree** and what **is not a tree.**

Since I am trying to measure curb appeal, I decided on a strict criteria:

1. I want to count trees that are a part of the sidewalk architecture.
<p align=“center”>
	<img alt="Original Picture" src="images/1205_n_31st_st_philadelphia_pa_19121 copy.jpg" width=450>
</p>

2. Trees visible in the background **do not** count.
<p align=“center”>
	<img alt="No tree" hspace=“25” src="images/1206_n_31st_st_philadelphia_pa_19121.jpg_pic1.jpg" width=250>
</p>

3. **Intersections** prove especially problematic. I decided that trees must be **on** a **parallel running block** to the one the "car" is on. Stated another way, I am looking trees that are **orthogonally adjacent** to the path of the "car."
<p align=“center”>
	<img alt="No tree" hspace=“25” src="images/1207_n_myrtlewood_st_philadelphia_pa_19121.jpg_flip2.jpg" width=250>
</p>

4. A portion of the tree trunk, however small, must be visible for me to label as a tree. **Only leaves**, or **only branches** is **not enough**.
<p align=“center”>
	<img alt="No tree" hspace=“25” src="images/2910_cambridge_st_philadelphia_pa_19130.jpg" width=450>
</p>


Again, the process of labeling happens within [label_pics.py](label_pics.py) using the Labeler class. The labeling happens in the following manner:

1. I wrote my function to **randomly choose a block** in the neighborhood I specified, then **fetch all pictures** associated with that block up to **the number of pics I specify**

2. The Labeler **fetches** a picture
<p align=“center”>
 <img alt="Original Picture" src="images/1205_n_31st_st_philadelphia_pa_19121.jpg" width=450>
</p>

3. To **avoid over or under counting trees**, and provide **more data to train on**, the Labeler then **splits the photo** vertically and displays each image for labeling.
<p align=“center”>
 <img alt="Split into two" src="images/1205_n_31st_st_philadelphia_pa_19121.jpg_pic1.jpg" width=250>
 <img alt="Split into two" src="images/1205_n_31st_st_philadelphia_pa_19121.jpg_pic2.jpg" width=250>
</p>

4. I then label as **YES** tree or **NO** tree for each split image.

<p align=“center”>
 <img alt="yes_tree" hspace=“25” src="images/yes_tree.jpg" width=250>
 <img alt="no_tree" hspace=“25” src="images/no_tree.jpg" width=250>
</p>

5. The Labeler than **mirrors** each photo with my assigned label and saves the picture

<p align=“center”>
 <img alt="Split into two" src="images/1205_n_31st_st_philadelphia_pa_19121.jpg_pic1.jpg" width=250>
 <img alt="Split into two" src="images/1205_n_31st_st_philadelphia_pa_19121.jpg_flip1.jpg" width=250>
</p>

Labeler Review:

	original image -> image split into image1, image2 -> image1 displayed and assigned label -> image1 and image2 mirrored -> images saved

	From the original **one** image **four** images are labeled and saved in following manner:

	address_pic1
	address_pic1_flip
	address_pic2
	address_pic2_flip

6. Every 100 pics, the labeler will **save** the **filename and label** to a pandas data frame as well as saving a backup of the data frame.

#### Resize
After labeling, the pictures are resized using the Resizer class in [label_pics.py](label_pics.py) in the following manner:

1. The folder of labeled pics is specified.

2. Each picture is resized. This can be specified, in my particular case images are 600x600 from GSV(max resolution from GSV is 1000x1000). They are then split vertically, so when split they become 600x300. When resized the images become 100x50.
<p align=“center”>
 <img alt="Original Picture" src="images/107_morris_st_philadelphia_pa_19147_pic1.jpg" width=50>
</p>

3. The resized image is saved for record keeping and bookkeeping purposes.

4. When reading an image, OpenCV **converts** it to a **numpy array**. The **filename and array** is saved to a pandas data frame.

#### Feed Network

Neural Network Architecture:

I used a Convolutional Neural Network using [Keras](https://keras.io/) and [Tensorflow](https://www.tensorflow.org/) on the backend. My model is built in [cnn.py](cnn.py) with the following architecture:

1. I trained my model on [AWS](aws.amazon.com) using a p2.8xlarge instance. I used this instance, because being a GPU instance my network took on average about **2 minutes to train**. As a comparison, on my own macbook air it took about 45 minutes to train my model.

2. I decided to keep my network **straight forward** for experimentation purposes.  I used two convolution layers and one pooling layer.

3. Each layer uses the **hyperbolic tangent** activation function, as this produced the best accuracy for my models.

4. My pooling layers drops out 25% of the neurons before and after pooling to prevent overfitting.

Train the Network:

1. My labeled data frame and numpy array data frame **joined** on 'filename'

2. I split my data in the following manner:

	80% Train, 20% Test

	The 80% Train data is then split 80%/20% train/validation during training.

3. The numpy arrays are **scaled** and formatted in the correct manner to feed into Keras.

4. The information passes through the CNN and I am able to see the accuracy of the model against my validation set.

5. After training, I test the model against my test data. If the accuracy of the model beats previous model accuracies, then the model is saved to used for the prediction stage.

## Results

#### The Numbers

My data set contains approximately 15,000 images. Therefore the Network trained on  ~9,500 images, validated on ~2,500 images and tested on ~3,000 images.

The model achieved the following results on the previously unseen test set.

Accuracy = 87%

Precision = 59%

Recall = 57%

F1 score = .58

Specificity = 93%

RMSE = 3.3

These results are by no means world changing, however, they are results I can build on!

**Most important** is what the data and the trained network are telling me in order for me to **learn** and adjust the model moving forward.

I decided to dig in a little deeper:

What is going on with the **false positives** to drive the **precision** down?

#### The Visuals

To see all the predictions in an interactive manner [go here](http://ec2-34-233-124-51.compute-1.amazonaws.com:1717/map)

**Note:** The website takes about 45 seconds to load

Analysis:

The model likes phone poles. But specifically, this one makes sense, the phone pole looks like a trunk and the leaves make it look like a trunk with a tree. I can build on this.
<p align=“center”>
	<img alt="labels" src="images/phone_pole.png" width=250>
</p>

The model is overfitting on trees that do not fit my criteria. It definitely likes a lot of green leaves in the picture.
<p align=“center”>
	<img alt="labels" src="images/tree.png" width=250>
</p>

Overall, the model likes seeing a lot of leaves. If it sees leaves an not a trunk, it still seems likely that it will predict a tree.

## Next Steps

**Unbalanced data**

My data consists of ~15,000 images, of which ~2,250 are labeled as 'TREE' or approximately an 85%/15% imbalance. I knew that given the small amount of images and imbalanced nature of my data, predicting on the test set would be a challenge. I adjusted the weights within my model to account for this imbalance, however, balanced data would still be best.



**Increase complexity of Neural Network**

In my quest to provide a proof of concept, I chose to keep the neural network very straight forward and to live with the results. I could reasonably expect my network to improve with greater depth.

**Larger images**

The actual size of the images I passed into the neural network were 100x50
<p align=“center”>
 <img alt="Original Picture" src="images/107_morris_st_philadelphia_pa_19147_pic1.jpg" width=50>
</p>

I would like to explore images that are a bit larger and see where that gets me.

**Good criteria?**

I chose very stringent criteria for my model. The goal is to use my model as a feature in real estate price predictions. With this in mind, does being able to see a tree down the block or in the distance affect an individual's purchase decision? If I constructed my model around this hypothesis I'd have a more precise feature to pass into my real estate prediction model and be able to test its' validity.

## Tech Stack

<p align=“center”>
 <img alt="Tech Stack" src="images/tech_stack.png">
</p>

## Sources

[Impetus for project: Estimate demographic makeup of US using GSV and machine learning](http://ai.stanford.edu/~tgebru/papers/pnas.pdf)

[Keras](https://keras.io/)

[A list of helpful articles](https://adeshpande3.github.io/adeshpande3.github.io/The-9-Deep-Learning-Papers-You-Need-To-Know-About.html)

[Machine learning for everyone](https://www.youtube.com/watch?v=mWl45NkFBOc&feature=youtu.be)

[Many thanks to the excellent stackoverflow community](https://stackoverflow.com/)
