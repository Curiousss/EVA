# EVA
What are Channels and Kernels (according to EVA)?
Channels are a bunch of features of a data. Each channel represent a certain feature of the data and all channels together represent the data in its whole. A data can be reresented by any number of channels. For example: An image can be represent for 3 channels, Red, Green and Blue. We can add further channels where one channels can represent shape of a face or just horozontal lines in the image, another for vertical lines. As you see as the number of channels increases the depth of the information of the data increases as well. 
Kernels are like filters that extract these features for each channel. The number of kernels used is as many as number of channels we want to create.

Why should we only (well mostly) use 3x3 Kernels?

How many times do we need to perform 3x3 convolution operation to reach 1x1 from 199x199 (show calculations)
