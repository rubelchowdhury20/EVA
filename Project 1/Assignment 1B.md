# Assignment 1B

## What are Channels and Kernels(according to EVA)?
In EVA to explain the concept of channel we were given two examples. One was about fried rice and another one was about orchestra.
Let's take the first example first. The fried rice is made up of few main ingredients like rice, carrot, green peas etc. Similarly
images are also made up of ingredients. The ingredients can be RGB channel or it can be other features like horizontal edges, vertical
edges etc. The main thing to notice is once we add all those individual ingredients or chanels, we get the original thing back.

Same in orchestra also we have multiple instruments. If we take one instrument from an orchestra, it itself represent some music.
But once we add all those instruments together it becomes a full music. So in this example all these instruments can be considered
as channels or kernels.

## Why should we only (well mostly) use 3x3 Kernels?
The reasons behind using 3x3 Kernels for most of the cases are as follows:
  1. First of all we should always use odd dimensional Kernel. Because there won't be any line of symmetry in even sized kernel.
    When we have line of symmetry it is easier to make sense of right and left of the receptive fields.
  2. Now that we are clear that we need odd sized kernel, using 3x3 Kernel we can reach any output dimension. We can get the
    similar output of 5x5 kernel using two 3x3 kernels. So in this way we can reduce the total number of parameters. 
    Casue 5x5=25 > 2x3x3 = 18
    
## How many times do we need to perform 3x3 convolution operation to reach 1x1 from 199x199 (show calculations)?
199x199 => 197x197
197x197 => 195x195
   .          .
   .          .
   .          .
   .          .
  5x5   =>   3x3
  3x3   =>   1x1
  
Calculation: 
We know that, one convultion reduces the dimension by 2.
Now the initial dimension is 199x199 which is an odd number. And we know that we always get reminder 1 when any odd number is 
divided by 2. The reminder is the final output dimenion we are expecting.
To get the total number of convolutions we have to divide 199 by 2. The quotient value will be our desired number of convolution operations.
 
 So the final result is 99.
