---
layout: post
title: '[Caffe] HDF5 Layer'
published: true
---
I have been working on a project in which we make predictions with caffe for non-image data. The very first step would be save the data in HDF5 file format.  
	
Hierarchical Data Format (HDF) is an open source file format for storing huge amounts of numerical data. Think of HDF as a file system within a file. It lets you organize the data hierarchically and manage large amount of data very efficiently. But HDF5 data doesn’t support data transformation. You have to pre-process your data with desired transformations before feeding them in.

In CAFFE, HDF5 data layer requires two files. One is .h5 file which contains your data and label, while the other is .txt file which specifies the path(s) to the .h5 file(s).

The dataset I am working on is saved as a matrix in a txt file, in which each row is a sample which could be considered as an flattened image.

```python
from __future__ import print_function
import numpy as np
import h5py
import os


import pandas as pd
data = np.genfromtxt("input.txt", delimiter=",")

# number of observations or number of images
size = data.shape[0]
# reshape the data into desired size, eg. Color*Height*Width=3*32*32
data = np.reshape(data, (size, 3, 32,  32))

# shuffle the dataset, make 4/5 be training and 1/5 be testing
import random
a = range(0, size)
random.shuffle(a)
test_size = int(round(size*0.2))

x_train = data[a[:test_size]]
x_test = data[a[test_size:]]

labels = pd.read_table("target.txt", delimiter=',', header=None)
y1 = np.array(labels.iloc[:, 0])
y2 = np.array(labels.iloc[:, 1], dtype=np.int8)


y1_train = y1[a[:test_size]]
y1_test = y1[a[test_size:]]
y2_train = y2[a[:test_size]]
y2_test = y2[a[test_size:]]


with h5py.File('data/train_data.h5', 'w') as f:
    f['data'] = x_train
    f['label1'] = y1_train
    f['label2'] = y2_train


with h5py.File('data/test_data.h5', 'w') as f:
    f['data'] = x_test
    f['label1'] = y1_test
    f['label2'] = y2_test


DIR = “directory link”
h5_train = os.path.join(DIR, 'train_data.h5')
h5_test = os.path.join(DIR, 'test_data.h5')

text_fn = os.path.join(DIR, 'train-path.txt')
with open(text_fn, 'w') as f:
    print(h5_train, file = f)

text_fn = os.path.join(DIR, 'test-path.txt')
with open(text_fn, 'w') as f:
     print(h5_test, file = f)

```