# BP神经网络


　　BP神经网络基本上指的是最简单的多层前馈神经网络，在这种神经网中，采用BP反射传播方法来进行参数优化。

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

关于ML4AI

网站：www.ml4ai.com

代码: https://gitee.com/sleechengn/ml4ai
