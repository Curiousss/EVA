## Initial Architecture:

* Start with atleast 3 layers of 3x3 convolutions to extract as many features as possible, with ReLu activations.
* Use atleast one bottle neck layer to reduce the channel size and extract important features to be carried further.
* In assignment 3 I used 2 bottleneck layers and added as many convolution layers to reach the receptive field of 28x28,
since we need not reach the RF of 28x28 for a simple image like MNIST I am planning to retain only one 1x1 layer to reduce the number
of parameters, instead of the 2nd bottleneck layer.
* Finish with one 7x7 convolution layer to get the final output, further apply flatten and softmax activation.

## Reduce parameters
The first aim is to reduce the number of parameters
reduce the number of kernels in each layer.
replace 7x7 with multiple 3x3 layers. (later removed because it did not improve the performance)

## Better Accuracy
Add Batch normalization. There was no major increase in accurcay

## Overfitting
With Dropout 0.05 the network already reached the accuracy of 99.4% at Step 3

