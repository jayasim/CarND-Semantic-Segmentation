# Semantic Segmentation Project - Advanced Deep Learning

## Introduction

The goal of this project is to construct a fully convolutional neural network based on the VGG-16 image classifier architecture for performing semantic segmentation to identify drivable road area from an car dashcam image (trained and tested on the KITTI data set).

## Approach

### Architecture

A pre-trained VGG-16 network was converted to a fully convolutional network by converting the final fully connected layer to a 1x1 convolution. The depth in this case is two: road and not-road. Performance is improved through the use of skip connections, performing 1x1 convolutions on previous VGG layers for layers 3 and 4 and adding them element-wise to upsampled using transposed convolution. The lower-level layers (i.e. the 1x1-convolved layer 7 is upsampled before being added to the 1x1-convolved layer 4). Each convolution and transpose convolution layer includes a kernel initializer and regularizer.

### Optimizer

The loss function used for the network is cross-entropy and as suggested in the theory an Adam optimizer is used to update network weights iterative based on the training data provided.

### Training

The hyperparameter confgurations used for training are:

  - keep_prob: 0.5
  - learning_rate: 0.0009
  - epochs: 50
  - batch_size: 5

## Results

Loss per batch tends to average below 0.095 after two epochs and below 0.066 after ten epochs. Average loss per batch at epoch 20: 0.048, at epoch 30: 0.058, at epoch 40: 0.062, and at epoch 50: 0.030.

## Performance

Semantic Segmentation system has been improvised using fusion quantisation and graph to binary optimisation. Using the following techniques the performance has been drastically improved.

  - Freezing Graphs
  - Graph Transforms
  a. Optimising for Inference
  b. Performing 8-bit calculations
  - Fusing Kernels (graph operations) - Batch normalisation, RELU, Convolution
  

### Samples

Below are a few sample images from the output of the FCN with the segmentation class.

![sample1](./samples/um_000007.png)
![sample2](./samples/um_000019.png)
![sample3](./samples/um_000029.png)
![sample4](./samples/um_000049.png)
![sample5](./samples/um_000059.png)
![sample6](./samples/um_000089.png)



### Setup
##### Frameworks and Packages
Make sure you have the following is installed:
 - [Python 3](https://www.python.org/)
 - [TensorFlow](https://www.tensorflow.org/)
 - [NumPy](http://www.numpy.org/)
 - [SciPy](https://www.scipy.org/)
##### Dataset
Download the [Kitti Road dataset](http://www.cvlibs.net/datasets/kitti/eval_road.php) from [here](http://www.cvlibs.net/download.php?file=data_road.zip).  Extract the dataset in the `data` folder.  This will create the folder `data_road` with all the training a test images.

### Start
##### Implement
Implement the code in the `main.py` module indicated by the "TODO" comments.
The comments indicated with "OPTIONAL" tag are not required to complete.
##### Run
Run the following command to run the project:
```
python main.py
```
**Note** If running this in Jupyter Notebook system messages, such as those regarding test status, may appear in the terminal rather than the notebook.

### Submission
1. Ensure you've passed all the unit tests.
2. Ensure you pass all points on [the rubric](https://review.udacity.com/#!/rubrics/989/view).
3. Submit the following in a zip file.
 - `helper.py`
 - `main.py`
 - `project_tests.py`
 - Newest inference images from `runs` folder  (**all images from the most recent run**)
 
 ## How to write a README
A well written README file can enhance your project and portfolio.  Develop your abilities to create professional README files by completing [this free course](https://www.udacity.com/course/writing-readmes--ud777).
