## Car image generation with GAN in pytorch

### Dataset: http://imagenet.stanford.edu/internal/car196/cars_test.tgz

#### Training Images
Input image size 128x128
![alt text](cars1.png "Training Images")

#### Generated Images
Generated image size 128x128
![alt text](Cars.png "Generated Images")

Input images are scaled to the values between -1 to 1

#### Discriminator:
- Has 5 Convolution Layers 
- Uses Leaky ReLU
- The last layer is a fully connected layer with output size 1

### Generator:
- Has 1 Fully connected Layer
- Has 5 Transpose Convolution Layers
- Uses ReLU
- The last layer is the tanh activation function
