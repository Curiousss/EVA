# Step by step approach to build Convolutional Neural Network for MNIST dataset
## 1. First Iteration: 1stDNN.ipynb
### Initial Architecture:

* 3 3x3 convolution layers with ReLu activations.
* 1 bottle neck layer to reduce the channel size and extract important features to be carried further.
* 2 3x3 convolution layers with ReLu activations.
* 1 1x1 layer to reduce the number of parameters extract important features to be carried further.
* 1 7x7 convolution layer to get the final output,
* Flatten and softmax activation.

In assignment 3, 2 bottleneck layers was used and convolution layers were used to reach the receptive field of 28x28,
since we need not reach the RF of 28x28 for a simple image like MNIST. 

## Reduce parameters
The first aim is to reduce the number of parameters to keep it within 15k
* reduce the number of kernels in each layer.
* The 7x7 layers was replaced with multiple 3x3 layers which did not improve the performance, so the change was reverted back.

#### Accuracy 99.04%, epoch 31, time taken 11s/epoch, parameters 12,902, batch size 32

The number of kernels used in the first iteration after meeting the requirement of parameters within 15k, was kept constant in the further iterations to be able to measure the performance with respect to the changes made in each iteration. The epoch is set 40 through out all iterations for the same purpose.

## 2. Second Iteration 2ndDNN.ipynb
### Batch Normalization
Batch normalization was added after every convolution except the last convolution layer.
#### Accuracy 99.24%, epoch 16, time taken 39s/epoch, parameters 13,278, batch size 32
The network is now 3 times slower than the earlier version.

### Dropout
There was some overfitting, so a dropout of 0.1 was added. Dropout was added after every convolution, after Batch normalization, except the last convolution layer.  The dropout value is kept low since the number of parameters is very low.
#### Accuracy 99.37%, epoch 25, time taken 44s/epoch, parameters 13,278, batch size 32, drop out 0.1
The network seemed to be some underfitting in the beginning epochs. Later for bigger batch sizes there was slight overfitting in the later epochs. Since these variations are not too severe the drop out value of 0.1 is retained for the further steps and the final network.

## 3. Third Iteration 3rdDNN.ipynb
Experimenting with different batch size with drop out value 0.1.

### Batch size 1024
#### Accuracy 99.30%, epoch 33, time taken 6s/epoch, parameters 13,278, drop out 0.1

### Batch size 512
#### Accuracy 99.36%, epoch 39, time taken 7s/epoch, parameters 13,278, drop out 0.1
The network started to slightly overfit after 20 epochs.

### Batch size 256
#### Accuracy 99.41%, epoch 34, time taken 9s/epoch, parameters 13,278, drop out 0.1

### Batch size 128
#### Accuracy 99.46%, epoch 39, time taken 15s/epoch, parameters 13,278, drop out 0.1
#### crosses 99.4% at epoch 21

(Seems like the time taken for each epoch on other prosseses on colab. E.g. When there are many different program running on the same colab account.)

## 4. Fourth Iteration 4thDNN.ipynb
Used batch size of 128 and added the Learning rate Scheduler.
#### Batch size 128, Accuracy 99.43%, epoch 25, time taken 15s/epoch, parameters 13,278, drop out 0.1
#### The validation accuracy crosses 99.4% at 21st epoch.
The network seems to steadily increase in both training and test accuracy. The network start to overfit after 20 epochs. So the dropout was tuned to 0.15

#### With lr scheduler, Batch size 128, Accuracy 99.48%, epoch 30, time taken 15s/epoch, parameters 13,278, drop out 0.15
#### The validation accuracy crosses 99.4% at 18th epoch.
With dropout 0.15 the network continued to underfit till the final epoch of 40, but the validation accuracy increased.
