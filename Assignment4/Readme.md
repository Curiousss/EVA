# Step by step approach to build Convolutional Neural Network for MNIST dataset
## 1. First Iteration: 1stDNN.ipynb
### Initial Architecture:

* 3 3x3 convolution layers with ReLu activations.
* 1 bottle neck layer to reduce the channel size and extract important features to be carried further.
* 2 3x3 convolution layers with ReLu activations.
* 1 1x1 layer to reduce the number of parameters, instead of the 2nd bottleneck layer.
* 1 7x7 convolution layer to get the final output,
* Flatten and softmax activation.

In assignment 3 I used 2 bottleneck layers and added as many convolution layers to reach the receptive field of 28x28,
since we need not reach the RF of 28x28 for a simple image like MNIST I am planning to retain only

## Reduce parameters
The first aim is to reduce the number of parameters to keep it within 15k
* reduce the number of kernels in each layer.
* The 7x7 layers was replaced with multiple 3x3 layers which did not improve the performance, so the change was reverted back.

#### Accuracy 99.04%, epoch 31, time taken 11s/epoch, parameters 12,902

The number of kernels used in the first iteration after meeting the requirement of parameters within 15k, was kept constant in the further iterations to be able to measure the performance with respect to the changes made in each iteration. The epoch is set 40 through out all iterations for the same purpose.

## 2. Second Iteration 2ndDNN.ipynb
### Batch Normalization
#### Accuracy %, epoch , time taken 39s/epoch, parameters 13,278
The network is now 3 times slower than the earlier version.

## Overfitting
With Dropout 0.05 the network already reached the accuracy of 99.4% at Step 3

## 3. Third Iteration 3rdDNN.ipynb
#### Accuracy %, epoch , time taken s/epoch, parameters 13,278

## 4. Fourth Iteration 4thDNN.ipynb
#### Accuracy %, epoch , time taken s/epoch, parameters 13,278
