---
layout: single
title: "Image Classification"
date: 2021-11-19 12:00:00 -0000
categories: neural network (nn) Convolutional nets  transfer learning  
excerpt: Classifying images using series of neural networks. 
---

In this project, we classify seires of images into ten classes using multi-layer perceptron, conveloutional neural network, and by using transfer learning from a pre-trained model (Inception). 

 
 <div align="center">
  <img src="/assets/images/blogs/ten_classes.png" width="600px" height="240" alt="Photo of a lighthouse.">
  <p>Ten sample images representing ten classes</p>
 </div>

## Transfer learning 

In this approach we could take would be to compute the latent vectors (the result of the images run through the Inception model) ahead of time and use those as our input features to the last few dense layers

In transfer learning, we use a network trained on one data set to provide a starting point for the modeling of other data.  As we are trying to model color images, we should look for another network trained on color images.  Luckily, we have already discussed such a network: the Inception network used in the Deep Dream notebook.

The following cell will load the model, omitting its classification layer (since we're not interested in classifying `ImageNet` images).

# include_top=False will discard avg_pool before prediction layer
inception = tf.keras.applications.inception_v3.InceptionV3(include_top=True, input_shape=(299, 299, 3))
inception = tf.keras.Model([inception.input], [inception.layers[-2].output]) # manually discard prediction layer


We used tranfer learning from the pre-trained *Inception* model. During the traing all the layers of the pre-trained model are frozen (will not train). In other words, the pre-trained model is utilized as feature extractor preprocessor.

<div align="center">
  <img src="/assets/images/blogs/pred_labels.png" width="500px" height="200" alt="Photo of a lighthouse.">
</div>
