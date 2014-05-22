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

# PROTOTEXT

To train a model, we first need to define the model. The model is defined in *.prototxt files which is instance of previously defined in *.proto files. Refer to [mnish demo](http://caffe.berkeleyvision.org/mnist_prototxt.html) which is illustrated by the caffe team. 

### Things to Noticed

*What is Kernel_size* 


