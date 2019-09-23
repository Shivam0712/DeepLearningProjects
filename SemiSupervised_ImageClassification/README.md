# Semi-Supervised Learning for Image Classification

## Introduction:


## Objective:

We are given a large class of flowers, 102 to be precise. Build a flower classification model which is discriminative between classes but can correctly classify all flower images belonging to the same class. There are a total of 20549 (train + test) images of flowers. Predict the category of the flowers present in the test folder with good accuracy.

## Data:

The data for this experiment was collected from [Garden Nerd: Flower Recognition Data Science Competition](https://www.hackerearth.com/problem/machine-learning/flower-recognition/). You can use this [link](https://he-public-data.s3-ap-southeast-1.amazonaws.com/HE_Challenge_data.zip) to download data or alternatively you can use [DataCollectionAndPreprocessing](https://github.com/Shivam0712/DeepLearningProjects/blob/master/SemiSupervised_ImageClassification/DataCollectionAndPreprocessing.ipynb) notebook.

[DataCollectionAndPreprocessing](https://github.com/Shivam0712/DeepLearningProjects/blob/master/SemiSupervised_ImageClassification/DataCollectionAndPreprocessing.ipynb) notebook will help you to collect and process data, and make a structured data directory suitable for different methods used in this project.

### Exploratory Data Analysis:

We have xxx samples in Train Data classified into 102 different categories of flowers, and xxx image samples in test data for which we have to generate the labels.

The distribution of train data across different categories is:


Some sample images from train data are:

Some sample images from test data are:
1.Source and Refer CollectData

Refer EDA

2. Train, Test Size, Categories and Distribution 

3. Train Samples

4. Test Samples

## Methodology:

Pretrained Models, Transfer learning, Why inception

Transfer Learning

Data Augmentation

SemiSupervised Learning

## Results

Comparison of Train and Val of Different methods

Test Results of Different Methods

## Conclusion


