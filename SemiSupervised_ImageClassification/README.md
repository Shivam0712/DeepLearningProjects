# Semi-Supervised Learning for Image Classification

## Introduction:
Image classification refers to a process in computer vision that can classify an image according to its visual content. While detecting an object or classifying an image is a trivial task for humans, robust image classification is still a challenge in computer vision applications. The application of deep learning is rapidly growing in the field of computer vision and is helping in building robust classification and identification models. The large, structured, and labeled image datasets like Imagenet and CIFAR, has made it possible to develop networks such as ResNet or Inception Net which can register high performances for image classification tasks. **The good thing about these models are the knowledge learned by them can be transferred and fine-tuned to classify images of another Image classification tasks. This is known as transfer learning.** However, even with these transferrable models, in many image classification tasks, the labeled datasets is not enough to yield good accuracies. One widely used technique to tackle this problem is by augmenting the data. **In data augmentation we flip, rotate, crop or add noise to amplify the number of training samples exponentially. ** Even with the data augmentation, over-reliance on supervised image tasks leaves us with a dependence on large volumes of human-labeled data, a luxury that is not available across all domains. In contrast, it is comparatively easy to accumulate a large dataset of unlabeled images. This has led to the development of **semi-supervised techniques which aims to learn meaningful representation from the unlabeled datasets through unsupervised training.**

**One such semi-supervised technique is [FeatureLearningRotNet](https://github.com/gidariss/FeatureLearningRotNet) where prior to performing the designated image classification task, the network is trained to classify rotated images based on their angle of rotation. This helps the network to learn useful low-level features which in turn helps it to perform better on the designated image classification task.**

**In this project we aim to compare between, direct transfer learning, transfer learning with augmented datasets, and transfer learning in addition to semi-supervised learning.** We pick a task in which we are given a large class of flowers, 102 to be precise. We need to build a flower classification model which is discriminative between classes but can correctly classify all flower images belonging to the same class. There are a total of 20549 (train + test) images of flowers, and we need to predict the category of the flowers present in the test folder with reasonable accuracy.

## Data:

The data for this experiment was collected from [Garden Nerd: Flower Recognition Data Science Competition](https://www.hackerearth.com/problem/machine-learning/flower-recognition/). You can use this [link](https://he-public-data.s3-ap-southeast-1.amazonaws.com/HE_Challenge_data.zip) to download data or alternatively you can use [DataCollectionAndPreprocessing](https://github.com/Shivam0712/DeepLearningProjects/blob/master/SemiSupervised_ImageClassification/DataCollectionAndPreprocessing.ipynb) notebook.

[DataCollectionAndPreprocessing](https://github.com/Shivam0712/DeepLearningProjects/blob/master/SemiSupervised_ImageClassification/DataCollectionAndPreprocessing.ipynb) notebook will help you to collect, process, and store data into structured directories suitable for different methods used in this project.

### Exploratory Data Analysis:

The code for exploratory data analysis can be found in [ExploratoryDataAnalysis](https://github.com/Shivam0712/DeepLearningProjects/blob/master/SemiSupervised_ImageClassification/ExploratoryDataAnalysis.ipynb) notebook. 

We have 18540 training image samples which are classified into 102 different categories of flowers. We have to generate labels for 2009 image samples present in the test data.

The distribution of train data across different categories is:
<img src="https://github.com/Shivam0712/DeepLearningProjects/blob/master/SemiSupervised_ImageClassification/Plots/trainDistribution.png" width="600" height="450">

Some sample images from train data are:
<img src="https://github.com/Shivam0712/DeepLearningProjects/blob/master/SemiSupervised_ImageClassification/Plots/trainSample.png" width="800" height="600">

Some sample images from test data are:
<img src="https://github.com/Shivam0712/DeepLearningProjects/blob/master/SemiSupervised_ImageClassification/Plots/testSample.png" width="800" height="600">

## Methodology:

There are many pretrained image classification models present in pytorch torchvision package which can be used for the purpose of transfer learning.

In this project we have used inception_v3 model because of its low number of paramaters and low Top-1-Error in comparison to other available models.
<img src="https://github.com/Shivam0712/DeepLearningProjects/blob/master/SemiSupervised_ImageClassification/Plots/PerformanceVsParam.png" width="600" height="300">

### Direct Transfer Learning

The code for direct tranfer learning can be found in [DirectTransferLearning](https://github.com/Shivam0712/DeepLearningProjects/blob/master/SemiSupervised_ImageClassification/DirectTransferLearning.ipynb) notebook.

1. In this method We use the originally available training dataset with out any augmentation.
2. We take pretrained inception_v3 model available through TorchVision package.
3. Remove the already present final fully connected layer of inception_v3 and replace it with our custom layer with 102 output units.
4. Train the model for 25 Epochs and make it learn to classify the image of flower in 102 given categories.
<img src="https://github.com/Shivam0712/DeepLearningProjects/blob/master/SemiSupervised_ImageClassification/Plots/tl_model.png" width="600" height="300">

### Transfer Learning with Data Augmentation

The code for tranfer learning with data augmentation can be found in [TransferLearningAugmentedDataset](https://github.com/Shivam0712/DeepLearningProjects/blob/master/SemiSupervised_ImageClassification/TransferLearningAugmentedDataset.ipynb) notebook.

1. In this method we randomly flip or rotate the images in training datatsets to increase the number of traiing samples from n to 5n.  
2. Training of inception_v3 is done similar to that of direct transfer learning.
<img src="https://github.com/Shivam0712/DeepLearningProjects/blob/master/SemiSupervised_ImageClassification/Plots/tl_aug_transfer.png" width="600" height="300">

### Transfer Learning + Semi-Supervised Learning

The code for tranfer learning with Semi-Supervised Learning can be found in [SemiSupervisedLearning](https://github.com/Shivam0712/DeepLearningProjects/blob/master/SemiSupervised_ImageClassification/SemiSupervisedLearning.ipynb) notebook.

1. In this method we use all the images from training and test, and rotate them at an angle of 180 degrees to build a custom set with two categories Original and Inverted images.
<img src="https://github.com/Shivam0712/DeepLearningProjects/blob/master/SemiSupervised_ImageClassification/Plots/SSL_ImageSample.png" width="600" height="450">

2. Next we train the inception_v3 model to distinguish between these two categories of images. While learning to perform this task, the network learns useful information related to plants and flowers such as flowers grow towards sky, stamen is on top of petals etc. This helps the network to learn robust low level features about the images.

3. After this we fine tune this trained model on the  the augmented training dataset to output original 102 categories.

<img src="https://github.com/Shivam0712/DeepLearningProjects/blob/master/SemiSupervised_ImageClassification/Plots/SSL_learning.png" width="600" height="700">

## Results

### Training and Validation Curves:

The following image shows the training/validation loss/accuracy for all the three different methods:

<img src= "https://github.com/Shivam0712/DeepLearningProjects/blob/master/SemiSupervised_ImageClassification/Plots/Performance.png"
width="800" height="500">

**The training and validation loss and accuracy for Semi-Supervised learning is significantly smooth in comparison to the other methods. This smoothness is due to the robust low level features learned by the network during the semi-supervised task.**

### Performance on Test Set:

The following table shows the training/validation loss/accuracy for all the three different methods:

<img src= "https://github.com/Shivam0712/DeepLearningProjects/blob/master/SemiSupervised_ImageClassification/Plots/Results.png"
width="400" height="150">

**Stand alone data augmentation is able to improve performance by 1.55% points. Semi-supervised learning is able to improve performance by 2.87% points on top of data augmentation benchmark.**

## Conclusion

In this project we have discussed about Transfer Learning, Data Augmentation, and Semi-Supervised Learning for image classification. All the three methods are used to boost the capability of network for image clssification tasks. We have evaluated the three methods using the flower species classification challenge, and have shown that the three methods helps in significantly improving the performance of network.
Data Augmentation is able to perform better than direct transfer learning due to the presence of comparatively large datasets.
Semi-supervised learning performs even better than data augmentation by learning robust low level features through the arbitary semisupervised task.
In conclusion, we can say these three techniques can be used to boost performance of image classification models and reduce over reliance on large size of labelled datasets.

## Installation:

1. Clone the repository.
2. Install the requirements: pip install -r requirements.txt
3. Run [DataCollectionAndPreprocessing](https://github.com/Shivam0712/DeepLearningProjects/blob/master/SemiSupervised_ImageClassification/DataCollectionAndPreprocessing.ipynb) notebook.
4. Choose the method of your choice and run the respective notebook.
