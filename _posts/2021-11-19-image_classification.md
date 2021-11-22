---
layout: single
title: "Image Classification"
date: 2021-11-19 12:00:00 -0000
categories: neural network (nn) Convolutional nets  transfer learning  
excerpt: Classifying images using series of neural networks. 
---

## Summary
In this project, we classify seires of images into ten classes using multi-layer perceptron, conveloutional neural network, and by using transfer learning from a pre-trained model (Inception). 

 
 <div align="center">
  <img src="/assets/images/blogs/ten_classes.png" width="600px" height="240" alt="Photo of a lighthouse.">
  <p>Ten sample images representing ten classes</p>
 </div>

## Transfer learning 
In this approach we computed the latent vectors (the result of the images run through a pre-trained network) ahead of time and use those as our input features to the last few dense layers. The pre-trained network that we used here is [`Inception`](https://keras.io/applications/). 

To build a classification model using keras API the following steps were taken:
1. Load the `inception` model:
  The following code snippet load the model and omit its classification layer, which is not required for our purposes. 
  ```python
  inception = tf.keras.applications.inception_v3.InceptionV3(include_top=True, input_shape=(299, 299, 3))
  inception = tf.keras.Model([inception.input], [inception.layers[-2].output]) # manually discard prediction layer
  ```
2. Upscale our images from $32\times32$ to `inception` native image shape: $299\times299$, using `tf.image.resize`

```markdown
_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
input_3 (InputLayer)         [(None, 32, 32, 3)]       0         
_________________________________________________________________
resizing_1 (Resizing)        (None, 299, 299, 3)       0         
_________________________________________________________________
functional_1 (Functional)    (None, 2048)              21802784  
=================================================================
Total params: 21,802,784
Trainable params: 0
Non-trainable params: 21,802,784
```
 


1. ith a smaller data set, such as this, it can be more efficient to pre-calculate the *latent vectors* that are the output of the pre-trained network.  These can be stored and used as input for training a smaller, separate network to make the predictions.  We recommend this approach for this miniproject.

Images should be fed to the `inception` network and then vectorized (you might want to refer to the `TF_DeepDream.ipynb` notebook).


We used tranfer learning from the pre-trained *Inception* model. During the traing all the layers of the pre-trained model are frozen (will not train). In other words, the pre-trained model is utilized as feature extractor preprocessor.

<div align="center">
  <img src="/assets/images/blogs/pred_labels.png" width="500px" height="200" alt="Photo of a lighthouse.">
</div>
