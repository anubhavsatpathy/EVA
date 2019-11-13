
### Baseline

In this article, David summons our attention to the Stanford's DAWNbench competition in which teams and individuals compete on aspects like training speed and cost while acheiving a benchmark asccuracy on a standard dataset like CIFAR10, ImageNet etc. In particular he draws our attention to **Ben Jhonson's** winning entry that had taken 341 seconds on a single GPU to train to 94% validation accuracy on the CIFAR10 dataset.

A deeper examination of the network yeilds the following results:
- A forward and backward pass through the network would take around 2.8E09 FLOPs (Floating point operations per second)
- The tesla V100 GPU gives 125 teraFLOPs i.e 125E12 FLOPs
- Given this information - It is easy to compute that training for 35 epochs should take about 40 seconds assuming 100% compute efficiency

This is the target - thet David sets for himself - In this section - he makes a few improvements:

- He removes the redundant Batch Norm - Relu group afetr the first convolution layer - This alone leads to a training time of 323 seconds
- Doing some pre-processing jobs like padding, Normalization etc once before beginning of training instead of repeatedly for every epoch shaves off a further 15 seconds and brings training time down to 308 secs
- For random pre-processing jobs like cutout, random flips etc - random number generators are called - Collating all these calls to the begining of the epoch shaves a further 7 seconds 
- Performing data pre-processing on the main thread instead of spawning a separate process subtracts another 4 seconds of the training time so we have 297s 

**At the end of this section training time is 297seconds**

### Mini-Batches:

In this experiment, David does the following:
- He increases batch size from 128 to 512
- He increases learning rate by 10%

By doing so, the network trains to 94% accuracy in 256 seconds

This does not make complete sense at all and to understand why - we have to understand what SGD actually means:

- SGD simply delays parameter updates till the end of the batch - it sums up all the gradients and then taken a step according to that sum
- Thus curvature penalties are incurred on lasge step sizes iff we first order effects dominate second order effects - Increadsing LR beyond this point penalizes the model

Now, the previously set LR was set using LR finder which said that was the maximum optimal LR. Then how can we still increase batch size without incurring curvature penalties. Think - larger batch size = larger steps due to summation.

David explains this aparent contradiction by introducing something that he calls **Catastrophic Forgetting**

![Image of Forgetting]()



