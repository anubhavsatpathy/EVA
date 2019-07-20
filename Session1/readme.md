## What are **CHANNELS** and **FILTERS**?

**CHANNELS** are containers of information and that is all they are. There are no boundaries on the kind of information they contain or if that information makes any perceptual difference to us as human observers. 

These *kinds of information* contained within channels are refered to hereafter as **FEATUTES**

**FILTERS** or **KERNELS** or **FEATURE EXTRACTORS** are they are mathematical functions that convert channels containing a particular set of features into channels containing another set of features. For example, the horizintal line kernel exemplified in the assignment code converts channels containing RGB amplitude features to channels containing horizontal edge amplitude features

In the case of **convolution filters**, the the mathematical operation performed is that of **Convolution**, one of the operands is the input channel or the image represented as a matrix or more generally a tensor of numbers and the other operand being a filter, also a matrix or more generally a tensor of numbers. The idea is that when **convolution** is performed using these **operands**, we will get output channels the represent the input channel in terms of the desired features

I will let the following image speak the remaining thousand words about channels and filters

![Convolution Filters](https://github.com/anubhavsatpathy/EVA/blob/master/Session1/images/channels.png)

## Why should we only (well mostly) use 3x3 kernels?

Two reasons:

- We can reduce any input channel to a 1x1 channel with GRF of the whole image using 3x3 channels
- We can use the line of symmetry of the 3x3 kernel to express various features efficiently

Well the whole idea behind a network that employs a layered convolution is to arrive at a 1x1 output after n layers of convolution and ensure that the Global receptive field of this output is the whole image / input channel. Now let's take an example of a 5x5 image:

Applying a 5x5 convolution to our image results in a 1x1 output channel

5x5 | Conv2D - 5x5 | 1x1

However we can employ 2 3x3 convolutions to acheive the same result:

5x5 | Conv2D - 3x3 | 3x3
3x3 | Conv2D - 3x3 | 1x1

And there does not seem to be a loss in information since the GRF of the output channel in both cases is the whole 5x5 input channel - Hence we find that if we use 3x3 kernels, we would be able to reduce any odd sized input channel to a 1x1 output over n layers.

One might ask what about even - sized input channels - well we ideally employ techniques of max pooling or padding to avoid these scenarios.

Another advantage of using 3x3 kernels instead of even sized kernels is that the 3x3 kernels have **line of symmetry** that even sized kernels wont have. This lends the 3x3 kernels a power of expression that is essential for feature extraction. For example - we can say enhance the values alligned with the vertical line of symmetry and reduce the values on either side of it to get a vertical edge detector - Similar expressions of features are not rendered possible by even sized kernels


## How many times do we need to perform 3x3 convolution operation to reach 1x1 from 199x199 (show calculations)

**With Max Pooling **

*Steps : 23

- 199x199 | Convolution 3x3 | 197x197
- 197x197 | Convolution 3x3 | 195x195
- 195x195 | Convolution 3x3 | 193x193
- 193x193 | Convolution 3x3 | 191x191
- 191x191 | MaxPooling 2x2 | 95x95
- 95x95 | Convolution 3x3 | 93x93
- 93x93 | Convolution 3x3 | 91x91
- 91x91 | Convolution 3x3 | 89x89
- 89x89 | Convolution 3x3 | 87x87
- 87x87 | MaxPooling 2x2 | 43x43
- 43x43 | Convolution 3x3 | 41x41
- 41x41 | Convolution 3x3 | 39x39
- 39x39 | Convolution 3x3 | 37x37
- 37x37 | Convolution 3x3 | 35x35
- 35x35 | MaxPooling 2x2 | 17x17
- 17x17 | Convolution 3x3 | 15x15
- 15x15 | Convolution 3x3 | 13x13
- 13x13 | Convolution 3x3 | 11x11
- 11x11 | Convolution 3x3 | 9x9
- 9x9 | Convolution 3x3 | 7x7
- 7x7 | Convolution 3x3 | 5x5
- 5x5 | Convolution 3x3 | 3x3
- 3x3 | Convolution 3x3 | 1x1

**Without Max Pooling ** 

*Steps : 100*

- 199x199 | Convolution 3x3 | 197x197
- 197x197 | Convolution 3x3 | 195x195
- 195x195 | Convolution 3x3 | 193x193
- 193x193 | Convolution 3x3 | 191x191
- 191x191 | Convolution 3x3 | 189x189
- 189x189 | Convolution 3x3 | 187x187
- 187x187 | Convolution 3x3 | 185x185
- 185x185 | Convolution 3x3 | 183x183
- 183x183 | Convolution 3x3 | 181x181
- 181x181 | Convolution 3x3 | 179x179
- 179x179 | Convolution 3x3 | 177x177
- 177x177 | Convolution 3x3 | 175x175
- 175x175 | Convolution 3x3 | 173x173
- 173x173 | Convolution 3x3 | 171x171
- 171x171 | Convolution 3x3 | 169x169
- 169x169 | Convolution 3x3 | 167x167
- 167x167 | Convolution 3x3 | 165x165
- 165x165 | Convolution 3x3 | 163x163
- 163x163 | Convolution 3x3 | 161x161
- 161x161 | Convolution 3x3 | 159x159
- 159x159 | Convolution 3x3 | 157x157
- 157x157 | Convolution 3x3 | 155x155
- 155x155 | Convolution 3x3 | 153x153
- 153x153 | Convolution 3x3 | 151x151
- 151x151 | Convolution 3x3 | 149x149
- 149x149 | Convolution 3x3 | 147x147
- 147x147 | Convolution 3x3 | 145x145
- 145x145 | Convolution 3x3 | 143x143
- 143x143 | Convolution 3x3 | 141x141
- 141x141 | Convolution 3x3 | 139x139
- 139x139 | Convolution 3x3 | 137x137
- 137x137 | Convolution 3x3 | 135x135
- 135x135 | Convolution 3x3 | 133x133
- 133x133 | Convolution 3x3 | 131x131
- 131x131 | Convolution 3x3 | 129x129
- 129x129 | Convolution 3x3 | 127x127
- 127x127 | Convolution 3x3 | 125x125
- 125x125 | Convolution 3x3 | 123x123
- 123x123 | Convolution 3x3 | 121x121
- 121x121 | Convolution 3x3 | 119x119
- 119x119 | Convolution 3x3 | 117x117
- 117x117 | Convolution 3x3 | 115x115
- 115x115 | Convolution 3x3 | 113x113
- 113x113 | Convolution 3x3 | 111x111
- 111x111 | Convolution 3x3 | 109x109
- 109x109 | Convolution 3x3 | 107x107
- 107x107 | Convolution 3x3 | 105x105
- 105x105 | Convolution 3x3 | 103x103
- 103x103 | Convolution 3x3 | 101x101
- 101x101 | Convolution 3x3 | 99x99
- 99x99 | Convolution 3x3 | 97x97
- 97x97 | Convolution 3x3 | 95x95
- 95x95 | Convolution 3x3 | 93x93
- 93x93 | Convolution 3x3 | 91x91
- 91x91 | Convolution 3x3 | 89x89
- 89x89 | Convolution 3x3 | 87x87
- 87x87 | Convolution 3x3 | 85x85
- 85x85 | Convolution 3x3 | 83x83
- 83x83 | Convolution 3x3 | 81x81
- 81x81 | Convolution 3x3 | 79x79
- 79x79 | Convolution 3x3 | 77x77
- 77x77 | Convolution 3x3 | 75x75
- 75x75 | Convolution 3x3 | 73x73
- 73x73 | Convolution 3x3 | 71x71
- 71x71 | Convolution 3x3 | 69x69
- 69x69 | Convolution 3x3 | 67x67
- 67x67 | Convolution 3x3 | 65x65
- 65x65 | Convolution 3x3 | 63x63
- 63x63 | Convolution 3x3 | 61x61
- 61x61 | Convolution 3x3 | 59x59
- 59x59 | Convolution 3x3 | 57x57
- 57x57 | Convolution 3x3 | 55x55
- 55x55 | Convolution 3x3 | 53x53
- 53x53 | Convolution 3x3 | 51x51
- 51x51 | Convolution 3x3 | 49x49
- 49x49 | Convolution 3x3 | 47x47
- 47x47 | Convolution 3x3 | 45x45
- 45x45 | Convolution 3x3 | 43x43
- 43x43 | Convolution 3x3 | 41x41
- 41x41 | Convolution 3x3 | 39x39
- 39x39 | Convolution 3x3 | 37x37
- 37x37 | Convolution 3x3 | 35x35
- 35x35 | Convolution 3x3 | 33x33
- 33x33 | Convolution 3x3 | 31x31
- 31x31 | Convolution 3x3 | 29x29
- 29x29 | Convolution 3x3 | 27x27
- 27x27 | Convolution 3x3 | 25x25
- 25x25 | Convolution 3x3 | 23x23
- 23x23 | Convolution 3x3 | 21x21
- 21x21 | Convolution 3x3 | 19x19
- 19x19 | Convolution 3x3 | 17x17
- 17x17 | Convolution 3x3 | 15x15
- 15x15 | Convolution 3x3 | 13x13
- 13x13 | Convolution 3x3 | 11x11
- 11x11 | Convolution 3x3 | 9x9
- 9x9 | Convolution 3x3 | 7x7
- 7x7 | Convolution 3x3 | 5x5
- 5x5 | Convolution 3x3 | 3x3
- 3x3 | Convolution 3x3 | 1x1
