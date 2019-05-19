### Descriptop and Order of Keypoints
-------

**1. Receptive field**

Number of pixels from the input image that a particular kernel would use to extract inforamtion at a particular layer is called `local receptive field`. For example a 1st layer 3x3 kernel would have a receptive field of  3x3. Similarly, a 2nd layer 3x3 kernel would have a recptive field would be 5x5. Number of pixels from the inout image that the last prediction layer kernel would use to extract the information is called `global receptive field`

**2. How many Convoution Layers** 

 It depends on the kernel size and input image size in a way or the object in the input image. Generally the number of layers is decided such that the last layer is able to see the object that we are trying to identify i.e glabal receptive field is equal to the size of the object in the input image
 
**3. 3x3 convolution**

It is most commonly used kernel size for image convolution. Generally odd nummbered kernel size is used for image convolution as symmetry is maintained while extracting the information from certain pixel and passed to next layer. As we loose information as part of convolution 3x3 is best option.



**4. Maxpooling**

Pooling is a technique to extract the features information from our feature maps and pass on to the next layers. They are effective in rapidly increasing our receptive field or decreasing channel size. Thus, help in decreasing parameters and build faster models. Maxpooling is pooling technique where the max of the selected pool is sent to the subsequent layers. It gives our model space invariance, orientation invariance and to an extent resolution invariance as well.

**5. 1x1 Convolution** 

General architecture of a cnn is to increase the number of channels so that we can understand more feautres of the input and then decrease the number of channels to combine these learning and equate them to our prediction channels. `1x1 convolution` is an effective way to decrease the number of channels or feature maps. It works very effectively as a aggregator of predominant features when back propagation is used to train the model. Earlier 3x3 convolution were used to decrease the channels as well but because of the ability of 1x1 to combine learned features into abstract patterns it is the widely used means to decrease number of channels in cnn.

**6. Concept of transition layer** 

A Maxpooling and 1x1 convolution together are considered as transition layer. As a thumb rule from cnn we try to extract the information in the following order:
 - Edges and gradients 
 - Textures and patterns 
 - Parts of object 
 - object 

As a practise we try to increase kernels from input to subsequents convolution layers and then use these transition layers to sort of summarise our learnings to detect edges and gradients and continue the same process to arrive at parts of textures and paterns till the we detect the image itself. This process can go on till the receptive field is equal to the object size.

**7. Position of max pooling** 

As discussed in the 6th point we use max pooling(as part of transition layer) generally after the layers where the receptive field is enough to see some sort of texture or pattern or parts of object. It very subject and we decide after a bit of experimentaion. For example, in 400x400 image we need to reach atleast 11x11 receptive with around 512 kernels to see some interpretable edge information of the input image extracted by kernels. So we place of maxpooling(transition layer) and work towards parts textures and gradients.

Also, max pooling should not be placed in the initial layers of the cnn model as the objective of the initial layers is to learn as many features as posible. And we also avoid using max pooling in last cnn layers as we indent to grasp as much information as possible from the layers where the model is learning from abstract features from earlier layers and would more or less have formed a fine interpretation of the image.

**8. The distance of MaxPooling from Prediction** 

we also avoid using max pooling in last cnn layers as we indent to grasp as much information as possible from the layers where the model is learning from abstract features from earlier layers and would more or less have formed a fine interpretation of the image. 

`Max pooling should be atleat 2 cnn layers away from the Prediction layer` 


**9. Position of Transition layer** 

As discussed in the 6th point we use transition layer generally after the layers where the receptive field is enough to see some sort of edges/gradients or texture/ pattern or parts of object. It very subject and we decide after a bit of experimentaion. For example, in 400x400 image we need to reach atleast 11x11 receptive field with around 512 kernels to see some interpretable edge information of the input image extracted by kernels. So we place of maxpooling(transition layer) and work towards parts textures and gradients.

**10. Softmax** 

Softmax a function that is used to convert the a vector of inputs which here are the activation values from the last cnn layer and then convert into a propabability like numbers. It basically enhances the difference between the rest highest value and the rest of the values. We should be careful while using softmax to predict classes. It is probability like and not prob exactly. For senistive predictions it is advisable to not use softmax fucntion.

**11. Kernels and how do we decide the number of kernels?**

Kernel is sort of filter which is used in convolution and helps us extract information/ features of the image. Number of kernels is a very subective concept and is based on the many constraints in hand for the respective problem. Some of the points you can consider while deciding the number of kernels: 
- Input image size: If it high(400x400) then it advisable to start with atleast 32 kernels and increase from there in the following layers in accordance with the concept explained as part of point 7. 
- Porcessing power: If you have less processing power then increasing the number of kernels would increase the parameters and hence the time and complexity of the model traning process.

**12. Image Normalization**

Image Normalization is done as we do not want the pixel values(which range from 0 - 255) to influence the kernel parameters formulation as part of back propagation thus introducing the instability in the model. In simple terms it used to bring large varying pixel values of the image to smaller variations i.e. in between 0-1. 

**13. When to add validation checks**

Add validation checks at every epoch for the following reasons 
1. You do not have to wait till the last epoch to understand the model performance.
2. You do not have to use the last epoch model. If you check validation accuracy at every epoch you can figure out the best model and use it.

**14. When do we stop convolutions and go ahead with a larger kernel or some other alternative (which we have not yet covered)** 

While designing architecture of the cnn model we generally stop convolution when we reach a resolution like 9x9 or 7x7 or less as 3x3 convolution(standard practice) would at max look at the information of each pixel only once or twice. This does not give any extra information from that feature map. So we stop 3x3 and directly reduce the 7x7 to 1x1 by larger size kernel 7x7 


**15. Batch Normalization**

Back propagation happens by optimizing the kernel parameters towards reaching least loss. Multiple epochs are run to reinforce confindence in stability of the model. With in a epoch, paramters are tuned after calculating loss for a batch of images. It can be anything from all images to 1 image at a time. 

`Batch Normalization is done decrease the bias that can be introduced because of particularly high or low activation output from a nueron`.

**16. The distance of Batch Normalization from Prediction**

We generally make sure that there is batch normalization added before the prediction layer.

**17. How do we know our network is not going well, comparatively, very early** 

While making changes to the cnn model and training it. You can discard the current iteration by observing the trainiing and testing accuracy at the first epoch and compare it with the previous best iteration of model and discard or consider accordingly.

**18. DropOut**

Dropout layer is added to cnn model to decrease the overfiting because of training images. It randomly stops certain number of kernels during training phase thus forcing the model to learn more robust feautres.   

**19. When do we introduce DropOut, or when do we know we have some overfitting** 

While training a model, If you see that the training accuracy to be very different from the validation/ test accuracy then that is an indication of overfitiing. We can add Drop out layer then.

**20. Number of Epochs and when to increase them** 

During training through back propagation,if we see that by last epoch the loss function or test accuracy or validation accuracy are changing drastically then it indicates that further epochs are required for learning. 

**21. Learning Rate** 

During a model training, for every epoch we find the gradient to understand the direction of change(DL/dp where L -loss function and p is parameter) and change the parameter by the following value : 
p = p - k(dL/dp). `Here K, the learning rate is the constant or scale by which we tune our parameters so that we move towards the minima of loss function thus arriving at the best possible model fit`.

**22. LR schedule and concept behind it** 

A constant learning rate may or may not help us tuning the paramters towards the lowest loss. A bigger learning rate would help us converge faster but we towards the end we might not reach the global minima if the stride by which we tweak our parameters is way to high than needed. Similarly a low learning rate would increase training time. So we schedule the learning rate such that initial strides are high but the learning rate decrease as the loss also decreases.

**23. Adam vs SGD** 

Currently as per my knowledege, there is no significant change between ADAM and SGD which are optimizers like stochaistic gradient descent.

**24. Batch Size, and effects of batch size** 

As discussed in point 15, Batch size is the number of images that optimizers process before tuning the parameters towards least loss. (Total number of images/ batch size) is the number of times parmeters are tuned by the optimizers in an epoch.

Increasing batch size is generally favourable as learning of the model at every step is good but the number of feature maps and images that can loaded at once in memory is constrained by the Hardware used. 
It also increases the speed of training. Where as smaller batch sizes take a lot of time to train i.e. epoch run time increases. 


### Reasoning Behind the order of above
--------

I can imagine the above points  into 2 broader groups:
**1. (1-11):** Points that have to be noted while designing and architecture or vanilla model.
**2. (12-24):** Points that have to be noted while training and testing the model. 
  -  Input image processing 
  -  Improvements to the existing vanilla model


 


