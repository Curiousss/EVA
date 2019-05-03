# EVA Assignment 1B

## What are Channels and Kernels (according to EVA)?
Channels are a bunch of features of a given data. Each channel represent a certain feature of the data and all channels together represent the data in its whole. A data can be reresented by any number of channels. For example: An image can be represent with 3 channels, Red, Green and Blue. We can add further channels where one channels can represent horozontal lines in the image, another for vertical lines. As you see as the number of channels increase the depth of the information of the data increases as well. 
Kernels are like filters that extract these features for each channel. The number of kernels used is as many as the number of channels we want to create.

## Why should we only (well mostly) use 3x3 Kernels?
Kernels can be of any size technically. But using kernels of certain size matters. 
1. Using a kernel of an odd size like 3x3 or 5x5, gives us a reference to the centre and the information about the direction around the center. This helps in capturing spacial information from the data.
2. 3x3 kernel are the smallest odd sized kernel and they preserve more input information than any larger kernels per step.
3. 3x3 is the smallest kernel size that can be used and it can be combined in any numbers to create a bigger a kernel. Although the effect or the output is the same, using many combined 3x3 kernel can reduce the number of multiplication operations performed.
E.g.: 5x5 requires 25 multiplications, 3x3 requires 9 multiplications. 5x5 can be achieved by 2 steps of 3x3 operations which will take 9+9=18 multiplication which is lesser than one 5x5 kernel which uses 25 multiplications.

## How many times do we need to perform 3x3 convolution operation to reach 1x1 from 199x199 (show calculations)
