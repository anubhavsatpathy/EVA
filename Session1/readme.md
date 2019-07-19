## What are **CHANNELS** and **FILTERS**?

**CHANNELS** are containers of information and that is all they are. There are no boundaries on the kind of information they contain or if that information makes any perceptual difference to us as human observers. 

These *kinds of information* contained within channels are refered to hereafter as **FEATUTES**

**FILTERS** or **KERNELS** or **FEATURE EXTRACTORS** are they are mathematical functions that convert channels containing a particular set of features into channels containing another set of features. For example, the horizintal line kernel exemplified in the assignment code converts channels containing RGB amplitude features to channels containing horizontal edge amplitude features

In the case of **convolution filters**, the the mathematical operation performed is that of **Convolution**, one of the operands is the input channel or the image represented as a matrix or more generally a tensor of numbers and the other operand being a filter, also a matrix or more generally a tensor of numbers. The idea is that when **convolution** is performed using these **operands**, we will get output channels the represent the input channel in terms of the desired features

I will let the following image speak the remaining thousand words about channels and filters

![Convolution Filters](/images/channels.png)

