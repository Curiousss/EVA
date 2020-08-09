# Extensive AI projects

## Phase 2: Reinforcement Learning, LSTM, RNN, Embedding, Pytorch
## Phase 1: Computer Vision

### Phase2/Session 9: T3D OR TWIN DELAYED DDPG
Explaination with diagrams for existing code

### Phase2/Session 8: 
- Asynchronous Advantage Actor Critic (A3C): Flow chart of functions for existing code
- Deep Q Learning (DQN) agent on the CartPole-v0 task from the OpenAI Gym:  Flow chart of functions for existing code

### Phase2/Session 7: Self Driving car using Kivy and Neural network with Full connected layers
- Enhance the model in the existing code
- Update the parameters
- Test with different maps.

### Phase2/Session 5: MNIST Dataset classification in Pytorch with following features:
- less than 15k params
- uses dropout of 0.1 
- uses batchnorm
- uses randomrotate transform
- uses StepLR with step size = 6 and gamma = 0.1
- achieves 99.3% test accuracy
- less than 15 epochs. 

### Phase2/Session 3: Implementation of the internal LSTM layer from scratch.

### Phase2/Session 2: Exploring RNN and embedding layers.

### Phase2/Session 1:Precomputed Glove embeddings
Precomputed embeddings downloaded from https://nlp.stanford.edu/projects/glove. Train the GLOVE based model with 8000 samples

## Convolutional Neural Networks and Computer Vision

### Assignment 25: Car Image Generation with GANs using pytorch

### Assignment 20: Resnet 18 pretrained with Imagenet.
The Cifar 100 images were resized to 197x197, normalized, and then flip and rotation augmentations were applied.
Layer 3 and 4 of Resnet 18 were unfrozen and made trainable while all other bottom layers were frozen. This was necessary since I am adding one Fully connected layer to get 100 outputs for the classifier which would not be enough to learn the new classes of images.
Working with learning rate was tricky. In first 20 epcohs the accuracy was 79% Then again 5 epochs were run with very low learning rate to reach 80%

### Assignment 13: ResNet18 model:
Modular implementation of Conv in blocks (B1->B2->B3->B4)
Batch Size 128
Normalization values of: (0.4914, 0.4822, 0.4465), (0.2023, 0.1994, 0.2010)
Random Crop of 32 with padding of 4px
Horizontal Flip (0.5)
Optimizer: SGD, Weight-Decay: 5e-4
NOT-OneCycleLR
300 Epochs

### Assignment 1 : Types of Kernels and convolutional arithmetic
### Assignment 2 : Receptive field
### Assignment 3 : MNIST 99.4% with < 20000 Parameters, Vanilla network (no BN, DropOut, LR, larger batch size, change in Optimizer, etc)
### Assignment 4 : 99.4% accuracy Less than 15k Parameters(with BN, DropOut, LR, larger batch size, change in Optimizer, etc)


