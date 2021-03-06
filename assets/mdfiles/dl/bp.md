# BP神经网络



　　BP神经网络基本上指的是最简单的多层前馈神经网络，在这种神经网中，采用BP反向传播方法来进行参数优化。

　　今天我们来推导一下反向传播的知识，反向传播在很多的文章里都没有说清楚。

　　让我们来看一个基本的知识，就是多元函数的导数。

<p align="center"><img src="https://latex.codecogs.com/gif.latex?z=f(x,y)"/></p>  


　　这是一个二元函数，当然多元函数也是适用的，我们知道z增大的方向就是偏导数的方向，它的偏导数表示为：

<p align="center"><img src="https://latex.codecogs.com/gif.latex?&#x5C;bigtriangledown%20f%20=%20&#x5C;frac{&#x5C;partial%20z}{&#x5C;partial%20x}+&#x5C;frac{&#x5C;partial%20z}{&#x5C;partial%20y}"/></p>  


这样的一个公式能干什么用呢？

我们假定此时：

<p align="center"><img src="https://latex.codecogs.com/gif.latex?z_0=f(x_0,y_0)"/></p>  


我们想让

<p align="center"><img src="https://latex.codecogs.com/gif.latex?z_0"/></p>  


增大，怎么改变

<p align="center"><img src="https://latex.codecogs.com/gif.latex?x_0,y_0"/></p>  


的值。

如果你知道导数的含义其实你已经知道该怎么做了，那就是求出在

<p align="center"><img src="https://latex.codecogs.com/gif.latex?(z_0,x_0,y_0)"/></p>  


处的偏导数，然后将

<p align="center"><img src="https://latex.codecogs.com/gif.latex?x_0,y_0"/></p>  


往偏导数的方向移动一小步，那么

<p align="center"><img src="https://latex.codecogs.com/gif.latex?z_0"/></p>  


自然也会增大。

以上说了这么多只是复习一下，我们有了一个让函数增大或者减小的方法，那就是把变量往导数的方向或者反方向移动，这样以来，就可以找到函数的极大值或者极小值，通过不断的移动。

在深度学习中

<p align="center"><img src="https://latex.codecogs.com/gif.latex?LOSS=NET(W,BIAS)"/></p>  


我们以同样的方法来调整W、BIAS，让

<p align="center"><img src="https://latex.codecogs.com/gif.latex?LOSS"/></p>  

的值最小化。

方法就是计算每一项参数的偏导数，然后往导数的方向调整。

下面我们开始知识：

# １、前置知识

阅读这篇文章时，假定你了解以下知识：

## 1、神经网络输入输出的计算


## 2、损失函数


## 3、导数


　　我觉得在这之前，你必须要把上面三个概念弄清楚，因为接下来的内容是以上面三个知识为基础的讲解，所以我们还是来复习一下上面三个知识点，如果你有不清楚的，可以看我另一篇或是其它博文。

　　神经网络不说了，如果你不清楚定义，可以点上面的链接看我的另一篇博文，当然你可以查资料，但是在读这篇博文的同时请你务必要搞清楚，下面还是说一下损失函数和导数吧。

　　损失函数 <p align="center"><img src="https://latex.codecogs.com/gif.latex?loss"/></p>  
 ，我们回顾一下定义，其实就是网络的实际输出和你想要的输出之间的差距，是一个欧氏距离，这个你学过 几何应该知道怎么计算，也就是平方和，我们有一个专业名词叫L2范数。另外还有一个重要的概念就是，可以通过调整权重偏执等参数来使损失函数变小，我们现在所说的损失函数若没有说明，默认是指网络输出的一个N维的点和希望输出的目标点之间的距离。

# 2、导数


　　我们看看导数吧，这个很重要，因为导数是关键，它是让网络往目标更新的关键，我不像其它博文那样讲，我用最直观的来讲，就从导数本身开始。我们先来看看导数的定义，从定义出发总是没有错的，对于一个曲线来说，导数是什么？

　　我们以二维的曲线为例吧，对于一个连续的曲线来说，我们可以用一个函数来表示，假设我们令这个函数关系是：

<p align="center"><img src="https://latex.codecogs.com/gif.latex?y=f(x)"/></p>  


　　我们来看看导数的定义，对于某一个点(x0,y0)来说，在这个点的导数定义是：

<p align="center"><img src="https://latex.codecogs.com/gif.latex?f&#x27;(x_0)=&#x5C;lim_{x-&gt;0}&#x5C;frac{f(x_0+dx)-f(x_0)}{dx}"/></p>  



<p align="center"><img src="https://latex.codecogs.com/gif.latex?&#x5C;text{在}x_0&#x5C;text{处的导数定义}"/></p>  



　　最原始的导数定义，如果这个不会，你就去翻上学时的内容，对于我们来说，不难看出，**导数就是该点的斜率**；
<p align="center"><img src="https://latex.codecogs.com/gif.latex?&#x5C;text{如果我们要通过改变}%20x_0%20&#x5C;text{的值让}f(x0)%20&#x5C;text{变小，我们必须把}x0&#x5C;text{往导数反方向移动}"/></p>  

根据定义，这个动作可以写这样的赋值：
<p align="center"><img src="https://latex.codecogs.com/gif.latex?x_0=x_0-step*f&#x27;(x_0)"/></p>  


　　参数说明   

　　　　　　　　　step代表移动的步长系数，一般很小，不能移太大，因为移太大可能一步移过了最低点

　　　　　　　　f'(x0)代表在x0处的导数

　　如果<p align="center"><img src="https://latex.codecogs.com/gif.latex?f&#x27;(x_0)&gt;0"/></p>  
，则往左移动<p align="center"><img src="https://latex.codecogs.com/gif.latex?step*|f&#x27;(x_0)|"/></p>  
，右边竖线是导数的绝对值

　　如果<p align="center"><img src="https://latex.codecogs.com/gif.latex?f&#x27;(x_0)&lt;0"/></p>  
，则往右移动<p align="center"><img src="https://latex.codecogs.com/gif.latex?step*|f&#x27;(x_0)|"/></p>  
，右边竖线是导数的绝对值

　　经过不断的计算导数然后不断的这样移动后，我们的f(x0)就不断的变小，直到让它成0，无法再移动，这样f(x0)就达到了一个极小值。

　　我们有了一个让f(x0)缩小的方法了，我们再来看看我们接下来重要的内容，我知道上面的可能对有人来说很基础，对有人来说却很困难，所以这个一定要确保能理解上面的方法，才能看下面的内容。

　　我们来看看，在神经网络里，从通过类似上微小移动每个参数来改变<p align="center"><img src="https://latex.codecogs.com/gif.latex?loss"/></p>  
。现在我们要讲方法，所以请务必把上面的东西看完并确保能完全理解，因为那是最基础的，所有后面的知识都基于上面的知识。

　　我们找到了一个在连续曲线上找到较小值的方法，就是调整某个参数，按它的导数反向微小移动的方式。

　　我们知道神经网络有权重还有偏执，我们这里用符号来表示，权重使用<p align="center"><img src="https://latex.codecogs.com/gif.latex?w_1,w_2,w_3,w_4,w_5,w_n"/></p>  
,,,等来表示，偏执用<p align="center"><img src="https://latex.codecogs.com/gif.latex?b_1,b_2,b_3,b_4,b_5,b_n"/></p>  
,,表示，我们这些都是网络中的参数，我们最终的目的是要**调整这些参数的大小，让<p align="center"><img src="https://latex.codecogs.com/gif.latex?loss"/></p>  
最小。**

　　我们知道神经网络是一个从输入层输入一个数据，然后通过计算流程，最终输出一数据，再与目标数据计算出一个**loss**，我们一定要清楚这个，特别是**loss**不是输出数据，而是计算结果与期望目标的欧氏距离。那么，对于一个确定的固定的输入神经网络，**LOSS**的大小取决于权重和偏执，调整其中一个权重，就意味着**LOSS**就会变化，那么同样的，我们根据导数的定义：调整其中一个权重<p align="center"><img src="https://latex.codecogs.com/gif.latex?w_n"/></p>  
使权重改变一个很小的<p align="center"><img src="https://latex.codecogs.com/gif.latex?dw"/></p>  
，调整以后<p align="center"><img src="https://latex.codecogs.com/gif.latex?loss"/></p>  
就会改变，对应的<p align="center"><img src="https://latex.codecogs.com/gif.latex?loss"/></p>  
有一个小的改变量，我们简写为<p align="center"><img src="https://latex.codecogs.com/gif.latex?dloss"/></p>  
，那么根据导数的定义，我们可以得出：对于此刻的状态，损失对某个权重的导数可以表示为：

<p align="center"><img src="https://latex.codecogs.com/gif.latex?&#x5C;frac{dloss}{dw}"/></p>  


　　这个解释一下，就是説移动一个参数后**LOSS**也会移动，两个的比值就是一个导数，也可当成斜率。

　　这就是此刻状态**loss**对**wn**的导数，由于**wn**可以是任意一个权重，所以我们称以上式子为此刻**loss**对**wn**的偏导数
<p align="center"><img src="https://latex.codecogs.com/gif.latex?&#x5C;frac%20{&#x5C;partial%20loss}{&#x5C;partial%20w_n}"/></p>  

这个是函数里的定义，所以不要问为什么这么取名字，原因是有多个自变量，每个变量的导数就是偏导数。同理，我们可以求出**loss**对任意的某个权重或某个偏执的偏导数，因为你只要把这个参数移动改一个微小量，对比**loss**的变化量就行。这样我们从理论上可以计算**loss**对任意参数的偏导数了。

　　还记得我们的曲线找最小值的方法吗，没错，你只要把参数值往偏导数反方向移动一个微小的值，也等于减小**loss**。

# 3、训练调整参数


　　下面讲今天的主题，BP算法，也就是反向传播算法，它是干什么的，没错，它就是计算**loss**对每个参数的偏导数的，所以我们就来看看BP是怎么计算的，这里为了照顾入门的同学，我就不讲什么矩阵运算了，我们以例子来讲怎么计算偏导数。

　　我们把loss的计算列成一个算式，在某次计算中：**loss** = .........，这里的省略号代表前面的计算流程，就是一堆数字和各种运算组合，由加法、乘法、平方、和Sigmoid函数组成，那么，我们如何求某个参数的偏导呢？我们就把这个参数设为变量x，不把它写成一个数字，比如把<p align="center"><img src="https://latex.codecogs.com/gif.latex?w_n"/></p>  
写成自变量x，其它的所有参数都写成数字，于是我们就得到了一个只含有loss和x是变量的函数了，乘下的就是一元函数求导了，求loss对x的导数，求出导数以后，代入x值，就得到某参数的导数。

　　我还是来一个简单的例子，假设一个简单的网络，loss展开后。
```math
loss = (1/(1+exp(-(w1*x1 + w2*x3 + w3 * x3)) - 1)
```
      请注意了，x1,w1,w3,w3,w4，等在一个计算中都是已知的，我们把除了w1的其它都写成已知的数字：
```math
loss = (1/(1+exp(-(w1*0.5+ 0.3*0.7 + 0.8*0.35)) - 1)
```
　　我们发现，函数成了一个只含有loss和w1的函数了，然后一元函数求导：dloss/dw1，懂了吧？然后计算出的导数代入w1值，计算然出一个导数值，同理把式子写成只含有w2的式子，计算出w2的导数，这样就可以计算任意参数的导数了。

　　这样我们可以通过固定其它参数，把要求导数的参数写成自变量，就能求参数的偏导数了。哈哈，这下知道了吧，求参数偏导数，那么反向传播是什么？其实是因为求的是一个复合函数，所以求导要一层一层的求，还能回忆函数的导数求法吗？从最外层往里层求，对应网络是从后面朝向前面求的，所以叫反向传播。

　　计算量大，优化我不说了，在反向传播里，要规划计算的路径，以最小的计算量来完成，因为参数很多，某些网络有数亿参数，所以这个优化问题要在你充分理解自己来总结。

　　这下我们只需要每次前向计算一次，再反向计算一次各个参数的偏导数，我们更新一次参数就行了，这个过程就是训练，不断的调整参数减小loss，这里要提一下这个计算量非常大，所以要使用像GPU这种高速的并行，并行的问题有空我再讲讲，这里不提，简单的说就是分工计算，把能分工的计算任务给不同的独立计算提供者，我们不断的训练让loss变小再次变小，也就是loss对每个权重和偏执的导数接近0，不能再小为止，这样loss很小的情况下，网络就成了我们预期的样子，可以用来对图像分类了。


