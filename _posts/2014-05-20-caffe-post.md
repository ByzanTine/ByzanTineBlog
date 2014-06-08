---
layout: post
title: "Caffe Details"
description: "Notes about BLVC open source CNN architecture"
modified: 2014-05-20 23:04:59 -0400
category: [Deep Learning]
tags: []
image:
  feature: 
  credit: 
  creditlink: 
comments: 
share: 
---

# Google Tool Used 

[Google Protobuf](https://developers.google.com/protocol-buffers/docs/overview) and [Google Leveldb](https://code.google.com/p/leveldb/). 

## protobuf

protobuf is kinda same like xml and json which define the data transfer protocol. Basically, it is smaller, faster and more user-friendly than json, xml. 

## leveldb

A simple to use key-value pair local database. Developed by Jeff Dean and Sanjay Ghemawat...then what else.

# Source Code Analysis

### github path: /caffe/src/caffe/util/im2col.*

im2col.cpp and im2col.cu implements the matlab function [im2col](http://www.mathworks.com/help/images/ref/im2col.html). The basic format is 
{% highlight matlab %}
	im2col(A,[m n],block_type)
{% endhighlight %}
When block_type is distinct, it pool a m\*n distinct block and unwrap it to a colum vector. And when block_type is sliding, it pool each m\*n block(like a sliding window) and unwrap it to a colum vector. Then it will be easy to calculate the sum of the block and reshape it which achieve the effect of [Pooling](http://ufldl.stanford.edu/wiki/index.php/Pooling).

### github path: caffe/tools/convert_imageset.cpp,caffe/tools/compute_image_mean.cpp

Parse the image data like *"path_to_img/1.jpg 4"* which is aligned by filename and label. Translate Image to Datum and then write into leveldb. After that, since we need to normalize the data, so just extract all the data and compute mean is needed.

# PROTOTXT

To train a model, we first need to define the model. The model is defined in *.prototxt files which is instance of previously defined in *.proto files. Refer to [mnish demo](http://caffe.berkeleyvision.org/mnist_prototxt.html) which is illustrated by the caffe team. 

### Solver

Solver.prototxt is the top-level file which connect the training NN(neural network) and validation NN. They should be defined in train_net and test_net. We can refer to the solver source code to the procedure. [solver.cpp](https://github.com/BVLC/caffe/blob/master/src/caffe/solver.cpp) is the top-level file that we need for training.
{%highlight c++ %}
void Solver<Dtype>::Init(const SolverParameter& param);
net_.reset();
test_net_.reset(); 
{%endhighlight%}
First, the solver will init the two network defined in the val.prototxt and train.prototxt. 
{%highlight c++ %}
void Solver<Dtype>::Solve(const char* resume_file);
Dtype loss = net_->ForwardBackward(bottom_vec);
{%endhighlight%}
Here a forward pass is used to obtain the train loss.

{%highlight c++ %}
void Solver<Dtype>::Test();
{%endhighlight%}
Here a forward pass to obtain the test loss and test accuracy.

[Solver.hpp](https://github.com/BVLC/caffe/blob/master/include/caffe/solver.hpp) is also a good reference.

### Train Net

First Portal, the well-known [Imagenet Paper](http://www.cs.toronto.edu/~fritz/absps/imagenet.pdf). Basically, the imagenet deep network used CNN, relu, pooling layer to develope a Deep Neural network to challenge on Image net. 

##### LRN and overlap pooling

LRN(Local Response Normalization), which intuitively "smooth" the Feature with the adjacent units. Overlap pooling is used in the same sense.
 


