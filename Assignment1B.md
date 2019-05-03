# EVA Assignment 1B

## What are Channels and Kernels (according to EVA)?
Channels are a bunch of features of a given data. Each channel represents a certain feature of the data and all channels together represent the data in its whole. A data can be reresented by any number of channels. For example: An image can be represent with 3 channels, Red, Green and Blue. We can add further channels where one channels can represent horozontal lines in the image, another for vertical lines. As you see as the number of channels increase the depth of the information of the data increases as well. 
Kernels are like filters that extract these features for each channel. The number of kernels used is as many as the number of channels we want to create.

## Why should we only (well mostly) use 3x3 Kernels?
Kernels can be of any size technically. But using kernels of certain size matters. 
1. Using a kernel of an odd size like 3x3 or 5x5, gives us a reference to the centre and the information about the direction around the center. This helps in capturing spacial information from the data.
2. 3x3 kernel is the smallest odd sized kernel and it preserves more input information than any larger kernels per step.
3. 3x3 is the smallest kernel size that can be used and it can be combined in any numbers to create a bigger kernel. Although the effect or the output is the same, using many combined 3x3 kernel can reduce the number of multiplication operations performed.
E.g.: 5x5 requires 25 multiplications, 3x3 requires 9 multiplications. 5x5 can be achieved by 2 steps of 3x3 operations which will take 9+9=18 multiplication which is lesser than one 5x5 kernel which uses 25 multiplications.

## How many times do we need to perform 3x3 convolution operation to reach 1x1 from 199x199 (show calculations)
Assuming the stride is 1 and no padding: <br /> 
199x199 Input size  <br /> 
    |  <br /> 
    |      3x3 convolution 1  <br /> 
    v <br /> 
197x197 <br /> 
  |      3x3 convolution 2 <br /> 
  v <br /> 
195x195 <br /> 
  |      3x3 convolution 3 <br /> 
  v <br /> 
193x193 <br /> 
  |      3x3 convolution 4 <br /> 
  v <br /> 
191x191 <br /> 
  |      3x3 convolution 5 <br /> 
  v <br /> 
189x189 <br /> 
  |      3x3 convolution 6 <br /> 
  v <br /> 
187x187 <br /> 
  |      3x3 convolution 7 <br /> 
  v <br /> 
185x185 <br /> 
  |      3x3 convolution 8 <br /> 
  v <br /> 
183x183 <br /> 
  |      3x3 convolution 9 <br /> 
  v <br /> 
181x181 <br /> 
  |      3x3 convolution 10 <br /> 
  v <br /> 
179x179 <br /> 
  |      3x3 convolution 11 <br /> 
  v <br /> 
177x177 <br /> 
  |      3x3 convolution 12 <br /> 
  v <br /> 
175x175 <br /> 
  |      3x3 convolution 13 <br /> 
  v <br /> 
173x173 <br /> 
  |      3x3 convolution 14 <br /> 
  v <br /> 
171x171 <br /> 
  |      3x3 convolution 15 <br /> 
  v <br /> 
169x169 <br /> 
  |      3x3 convolution 16 <br /> 
  v <br /> 
167x167 <br /> 
  |      3x3 convolution 17 <br /> 
  v <br /> 
165x165 <br /> 
  |      3x3 convolution 18 <br /> 
  v <br /> 
163x163 <br /> 
  |      3x3 convolution 19 <br /> 
  v <br /> 
161x161 <br /> 
  |      3x3 convolution 20 <br /> 
  v <br /> 
159x159 <br /> 
  |      3x3 convolution 21 <br /> 
  v <br /> 
157x157 <br /> 
  |      3x3 convolution 22 <br /> 
  v <br /> 
155x155 <br /> 
  |      3x3 convolution 23 <br /> 
  v <br /> 
153x153 <br /> 
  |      3x3 convolution 24 <br /> 
  v <br /> 
151x151 <br /> 
  |      3x3 convolution 25 <br /> 
  v <br /> 
149x149 <br /> 
  |      3x3 convolution 26 <br /> 
  v <br /> 
147x147 <br /> 
  |      3x3 convolution 27 <br /> 
  v <br /> 
145x145 <br /> 
  |      3x3 convolution 28 <br /> 
  v <br /> 
143x143 <br /> 
  |      3x3 convolution 29 <br /> 
  v <br /> 
141x141 <br /> 
  |      3x3 convolution 30 <br /> 
  v <br /> 
139x139 <br /> 
  |      3x3 convolution 31 <br /> 
  v <br /> 
137x137 <br /> 
  |      3x3 convolution 32 <br /> 
  v <br /> 
135x135 <br /> 
  |      3x3 convolution 33 <br /> 
  v <br /> 
133x133 <br /> 
  |      3x3 convolution 34 <br /> 
  v <br /> 
131x131 <br /> 
  |      3x3 convolution 35 <br /> 
  v <br /> 
129x129 <br /> 
  |      3x3 convolution 36 <br /> 
  v <br /> 
127x127 <br /> 
  |      3x3 convolution 37 <br /> 
  v <br /> 
125x125 <br /> 
  |      3x3 convolution 38 <br /> 
  v <br /> 
123x123 <br /> 
  |      3x3 convolution 39 <br /> 
  v <br /> 
121x121 <br /> 
  |      3x3 convolution 40 <br /> 
  v <br /> 
119x119 <br /> 
  |      3x3 convolution 41 <br /> 
  v <br /> 
117x117 <br /> 
  |      3x3 convolution 42 <br /> 
  v <br /> 
115x115 <br /> 
  |      3x3 convolution 43 <br /> 
  v <br /> 
113x113 <br /> 
  |      3x3 convolution 44 <br /> 
  v <br /> 
111x111 <br /> 
  |      3x3 convolution 45 <br /> 
  v <br /> 
109x109 <br /> 
  |      3x3 convolution 46 <br /> 
  v <br /> 
107x107 <br /> 
  |      3x3 convolution 47 <br /> 
  v <br /> 
105x105 <br /> 
  |      3x3 convolution 48 <br /> 
  v <br /> 
103x103 <br /> 
  |      3x3 convolution 49 <br /> 
  v <br /> 
101x101 <br /> 
  |      3x3 convolution 50 <br /> 
  v <br /> 
99x99 <br /> 
  |      3x3 convolution 51 <br /> 
  v <br /> 
97x97 <br /> 
  |      3x3 convolution 52 <br /> 
  v <br /> 
95x95 <br /> 
  |      3x3 convolution 53 <br /> 
  v <br /> 
93x93 <br /> 
  |      3x3 convolution 54 <br /> 
  v <br /> 
91x91 <br /> 
  |      3x3 convolution 55 <br /> 
  v <br /> 
89x89 <br /> 
  |      3x3 convolution 56 <br /> 
  v <br /> 
87x87 <br /> 
  |      3x3 convolution 57 <br /> 
  v <br /> 
85x85 <br /> 
  |      3x3 convolution 58 <br /> 
  v <br /> 
83x83 <br /> 
  |      3x3 convolution 59 <br /> 
  v <br /> 
81x81 <br /> 
  |      3x3 convolution 60 <br /> 
  v <br /> 
79x79 <br /> 
  |      3x3 convolution 61 <br /> 
  v <br /> 
77x77 <br /> 
  |      3x3 convolution 62 <br /> 
  v <br /> 
75x75 <br /> 
  |      3x3 convolution 63 <br /> 
  v <br /> 
73x73 <br /> 
  |      3x3 convolution 64 <br /> 
  v <br /> 
71x71 <br /> 
  |      3x3 convolution 65 <br /> 
  v <br /> 
69x69 <br /> 
  |      3x3 convolution 66 <br /> 
  v <br /> 
67x67 <br /> 
  |      3x3 convolution 67 <br /> 
  v <br /> 
65x65 <br /> 
  |      3x3 convolution 68 <br /> 
  v <br /> 
63x63 <br /> 
  |      3x3 convolution 69 <br /> 
  v <br /> 
61x61 <br /> 
  |      3x3 convolution 70 <br /> 
  v <br /> 
59x59 <br /> 
  |      3x3 convolution 71 <br /> 
  v <br /> 
57x57 <br /> 
  |      3x3 convolution 72 <br /> 
  v <br /> 
55x55 <br /> 
  |      3x3 convolution 73 <br /> 
  v <br /> 
53x53 <br /> 
  |      3x3 convolution 74 <br /> 
  v <br /> 
51x51 <br /> 
  |      3x3 convolution 75 <br /> 
  v <br /> 
49x49 <br /> 
  |      3x3 convolution 76 <br /> 
  v <br /> 
47x47 <br /> 
  |      3x3 convolution 77 <br /> 
  v <br /> 
45x45 <br /> 
  |      3x3 convolution 78 <br /> 
  v <br /> 
43x43 <br /> 
  |      3x3 convolution 79 <br /> 
  v <br /> 
41x41 <br /> 
  |      3x3 convolution 80 <br /> 
  v <br /> 
39x39 <br /> 
  |      3x3 convolution 81 <br /> 
  v <br /> 
37x37 <br /> 
  |      3x3 convolution 82 <br /> 
  v <br /> 
35x35 <br /> 
  |      3x3 convolution 83 <br /> 
  v <br /> 
33x33 <br /> 
  |      3x3 convolution 84 <br /> 
  v <br /> 
31x31 <br /> 
  |      3x3 convolution 85 <br /> 
  v <br /> 
29x29 <br /> 
  |      3x3 convolution 86 <br /> 
  v <br /> 
27x27 <br /> 
  |      3x3 convolution 87 <br /> 
  v <br /> 
25x25 <br /> 
  |      3x3 convolution 88 <br /> 
  v <br /> 
23x23 <br /> 
  |      3x3 convolution 89 <br /> 
  v <br /> 
21x21 <br / <br /> > 
  |      3x3 convolution 90 <br /> 
  v <br /> 
19x19 <br /> 
  |      3x3 convolution 91 <br /> 
  v <br /> 
17x17 <br /> 
  |      3x3 convolution 92 <br /> 
  v <br /> 
15x15 <br /> 
  |      3x3 convolution 93 <br /> 
  v <br /> 
13x13 <br /> 
  |      3x3 convolution 94 <br /> 
  v <br /> 
11x11 <br /> 
  |      3x3 convolution 95 <br /> 
  v <br /> 
9x9 <br /> 
  |      3x3 convolution 96 <br /> 
  v <br /> 
7x7 <br />
  |      3x3 convolution 97 <br /> 
  v <br /> 
5x5 <br /> 
  |      3x3 convolution 98 <br /> 
  v <br /> 
3x3 <br /> 
  |      3x3 convolution 99 <br /> 
  v <br /> 
1x1 <br /> 

