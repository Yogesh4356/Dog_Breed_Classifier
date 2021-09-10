# Dog Breed classification using CNN
This project is about detecting the dog's breed from the user supplied image. If a dog is detected in the image, it will provide an estimate of the dog's breed. If a human is detected, it will provide an estimate of the dog breed that is most resembling, otherwise it'll say "Neither a dog nor human detcted in the image".

First it'll try to detect if human face is in image and give the estimation of most resembling dog breed, if human not detected in image then it will try to detect if dog is in image and give the estimation of it's breed, if neither human nor dog is detected then it'll provide estmation based on "Imagenet" dataset.

Complete roadmap is here :

    1. Import dataset
    
    2. Detect humans
    
    3. Detect dogs
    
    4. Creating a CNN to detect dog breed(from scratch)
    
    5. Use a pretrained CNN to detect dog breed(from transfer learning)
    
    6. Write final algorithm
    
    7. Prediction
    
What is CNN and why CNN ?

A CNN is a supervised learning technique which needs both input data and target output data to be supplied. These are classified by using their labels in order to provide a learned model for future data analysis.

Typically a CNN has three main constituents - a Convolutional Layer, a Pooling Layer and a Fully connected Dense Network. The Convolutional layer takes the input image and applies m number of nxn filters to receive a feature map. The feature map is next fed into the max pool layer which is essentially used for dimensionality reduction, it picks only the best features from the feature map. Finally, all the features are flattened and sent as input to the fully connected dense neural network which learns the weights using backpropagation and provides the classification output.

Compared to MLP (Multilayer Perceptron) classifier, CNN gives better results as the MLP classifier takes a vector as input where as the CNN takes a 4-D Tensor as input (Thus having the spatial information)
    
## Step 1 : Import dataset
The dog dataset was downloaded from (https://s3-us-west-1.amazonaws.com/udacity-aind/dog-project/dogImages.zip), the human dataset was downloaded from (https://s3-us-west-1.amazonaws.com/udacity-aind/dog-project/lfw.zip). 

There were 133 total dog categories, 8351 total dog images, 6680 training dog images, 835 validation dog images, 836 test dog images and 13233 total human images.

## Step 2 : Detect humans
We used OpenCV's implementation of Haar feature-based cascade classifiers to detect human faces in images. OpenCV provides many pre-trained face detectors, stored as XML files on github(https://github.com/opencv/opencv/tree/master/data/haarcascades). We have downloaded one of these detectors and stored. Then we used this classifier to detect human faces in the image 

## Step 3 : Detect dogs
Here we used a pre-trained ResNet-50 model (a very deep CNN model) to detect dogs in images. Same weights that have trained on ImageNet dataset (a very large, very popular dataset having over 10 million images and over 1000 different categories) were used.

In data preprocessing step the images were converted to 4-D tensors and vertically stacked. In Imagenet dataset the key values from 151-268 inclusive contains all dog categories. so the dog detector will return true if the prediction of the ResNet-50 model lies between 151-268.

## Step 4 : Creating CNN from scratch
Here we have created a 5 layer CNN model 

