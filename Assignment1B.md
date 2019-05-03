# EVA Assignment 1B

## What are Channels and Kernels (according to EVA)?
Channels are a bunch of features of a given data. Each channel represent a certain feature of the data and all channels together represent the data in its whole. A data can be reresented by any number of channels. For example: An image can be represent with 3 channels, Red, Green and Blue. We can add further channels where one channels can represent horozontal lines in the image, another for vertical lines. As you see as the number of channels increase the depth of the information of the data increases as well. 
Kernels are like filters that extract these features for each channel. The number of kernels used is as many as the number of channels we want to create.

## Why should we only (well mostly) use 3x3 Kernels?
Kernels can be of any size technically. But using kernels of certain size matters. 
1. Using a kernel of an odd size like 3x3 or 5x5, gives us a reference to the centre and the information about the direction around the center. This helps in capturing spacial information from the data.
2. 3x3 kernel are the smallest odd sized kernel and they preserve more input information than any larger kernels per step.
3. 3x3 is the smallest kernel size that can be used and it can be combined in any numbers to create a bigger a kernel. Although the effect or the output is the same, using many combined 3x3 kernel can reduce the number of multiplication operations performed.
E.g.: 5x5 requires 25 multiplications, 3x3 requires 9 multiplications. 5x5 can be achieved by 2 steps of 3x3 operations which will take 9+9=18 multiplication which is lesser than one 5x5 kernel which uses 25 multiplications.

## How many times do we need to perform 3x3 convolution operation to reach 1x1 from 199x199 (show calculations)
Assuming the stride is 1 and no padding:
199x199 Input size
  |      3x3 convolution 1
  v
197x197
  |      3x3 convolution 2
  v
195x195
  |      3x3 convolution 3
  v
193x193
  |      3x3 convolution 4
  v
191x191
  |      3x3 convolution 5
  v
189x189
  |      3x3 convolution 6
  v
187x187
  |      3x3 convolution 7
  v
185x185
  |      3x3 convolution 8
  v
183x183
  |      3x3 convolution 9
  v
181x181
  |      3x3 convolution 10
  v
179x179
  |      3x3 convolution 11
  v
177x177
  |      3x3 convolution 12
  v
175x175
  |      3x3 convolution 13
  v
173x173
  |      3x3 convolution 14
  v
171x171
  |      3x3 convolution 15
  v
169x169
  |      3x3 convolution 16
  v
167x167
  |      3x3 convolution 17
  v
165x165
  |      3x3 convolution 18
  v
163x163
  |      3x3 convolution 19
  v
161x161
  |      3x3 convolution 20
  v
159x159
  |      3x3 convolution 21
  v
157x157
  |      3x3 convolution 22
  v
155x155
  |      3x3 convolution 23
  v
153x153
  |      3x3 convolution 24
  v
151x151
  |      3x3 convolution 25
  v
149x149
  |      3x3 convolution 26
  v
147x147
  |      3x3 convolution 27
  v
145x145
  |      3x3 convolution 28
  v
143x143
  |      3x3 convolution 29
  v
141x141
  |      3x3 convolution 30
  v
139x139
  |      3x3 convolution 31
  v
137x137
  |      3x3 convolution 32
  v
135x135
  |      3x3 convolution 33
  v
133x133
  |      3x3 convolution 34
  v
131x131
  |      3x3 convolution 35
  v
129x129
  |      3x3 convolution 36
  v
127x127
  |      3x3 convolution 37
  v
125x125
  |      3x3 convolution 38
  v
123x123
  |      3x3 convolution 39
  v
121x121
  |      3x3 convolution 40
  v
119x119
  |      3x3 convolution 41
  v
117x117
  |      3x3 convolution 42
  v
115x115
  |      3x3 convolution 43
  v
113x113
  |      3x3 convolution 44
  v
111x111
  |      3x3 convolution 45
  v
99x99
  |      3x3 convolution 46
  v
97x97
  |      3x3 convolution 47
  v
95x95
  |      3x3 convolution 48
  v
93x93
  |      3x3 convolution 49
  v
91x91
  |      3x3 convolution 50
  v
89x89
  |      3x3 convolution 51
  v
87x87
  |      3x3 convolution 52
  v
85x85
  |      3x3 convolution 53
  v
83x83
  |      3x3 convolution 54
  v
81x81
  |      3x3 convolution 55
  v
79x79
  |      3x3 convolution 56
  v
77x77
  |      3x3 convolution 57
  v
75x75
  |      3x3 convolution 58
  v
73x73
  |      3x3 convolution 59
  v
71x71
  |      3x3 convolution 60
  v
69x69
  |      3x3 convolution 61
  v
67x67
  |      3x3 convolution 62
  v
65x65
  |      3x3 convolution 63
  v
63x63
  |      3x3 convolution 64
  v
61x61
  |      3x3 convolution 65
  v
59x59
  |      3x3 convolution 66
  v
57x57
  |      3x3 convolution 67
  v
55x55
  |      3x3 convolution 68
  v
53x53
  |      3x3 convolution 69
  v
51x51
  |      3x3 convolution 70
  v
49x49
  |      3x3 convolution 71
  v
47x47
  |      3x3 convolution 72
  v
45x45
  |      3x3 convolution 73
  v
43x43
  |      3x3 convolution 74
  v
41x41
  |      3x3 convolution 75
  v
39x39
  |      3x3 convolution 76
  v
37x37
  |      3x3 convolution 77
  v
35x35
  |      3x3 convolution 78
  v
33x33
  |      3x3 convolution 79
  v
31x31
  |      3x3 convolution 80
  v
29x29
  |      3x3 convolution 81
  v
27x27
  |      3x3 convolution 82
  v
25x25
  |      3x3 convolution 83
  v
23x23
  |      3x3 convolution 84
  v
21x21
  |      3x3 convolution 85
  v
19x19
  |      3x3 convolution 86
  v
17x17
  |      3x3 convolution 87
  v
15x15
  |      3x3 convolution 88
  v
13x13
  |      3x3 convolution 89
  v
11x11
  |      3x3 convolution 90
  v
9x9
  |      3x3 convolution 91
  v
7x7
  |      3x3 convolution 92
  v
5x5
  |      3x3 convolution 93
  v
3x3
  |      3x3 convolution 94
  v
1x1

