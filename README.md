# EfficientNet-Signal-Vehicle-Counting
**Task**

The task was to take in a single image and output two numbers: 

a) the number of signals in the image (traffic lights and stop signs count as signals)

b) the number of vehicles in the image (cars, buses, trucks, trains, motorcycles, bicycles and boats count as vehicles)

**Dataset**

The dataset consisted of around 5k images of size 224 X 224 X 3.

**Overview**

I am using an ensemble model here and am running two models as part of my ensemble. One is for detecting signals and the other is for detecting the vehicles. And on top of that, I am adding a special function on the predicted values to further reduce MSE. 

**Model 1 (for signals)**

Here, I am using transfer learning. I am basically using EfficientNetV2B1, and adding a bunch of dense layers to it. 

I experimented with hyperparameter tuning and realized that a bunch of dense layers that keep reducing in width by a factor of 2 does the trick. 

I started with a dense layer of 128 and keep hoing till a dense layer of 32 units, and am keeping “relu” all the way as activation layer.  

I am not adding any convolution layers as I am doing global average pooling on top when reading from Efficient Net. 

I even tried using dropouts, but this gave a poorer result. 

In the end, there is an output neuron as the output layer to predict the count of signals. 

**Model 2 (for vehicles)**

Here too , I am using transfer learning. I am basically using EfficientNetV2B1 again, and adding a bunch of dense layers to it. 

I experimented with hyperparameter tuning and realized that a bunch of dense layers that keep reducing in width by a factor of 2 does the trick here too. 

But here, it gave better results when I started with a dense layer of 32 units and kept going till a dense layer of 4 units, and am keeping “relu” all the way as activation layer.  

I am not adding any convolution layers as I am doing global average pooling on top when reading from Efficient Net.

I even tried using dropouts, but this gave a poorer result. 

In the end, there is an output neuron as the output layer to predict the count of vehicles. 

**Final Function**

As we are using the “relu” activation function, it sometimes (albeit rarely) gives negative results. 

But since we know that the count of vehicles or signal cannot be negative, I am converting all the negative values to positive to further reduce MSE. 

**Results**

This assignment was the final project for our Advanced ML Class during my MS at UCLA. My Average MSE of 4.53 was the best in the whole class, which gave me a perfect score on the final project. 

(Signal MSE = 1.06 Vehicle MSE = 8.01)
