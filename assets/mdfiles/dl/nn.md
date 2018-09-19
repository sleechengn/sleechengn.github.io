# 1、什么是神经网络，它是如何计算的。
  
  
  
  
　　首先来看神经网络长什么样子：
  
![image](http://www.ml4ai.com/images/20180322134236904.png )
  
**神经网络**
  
　　图中表示的是一个输入层是4，中间层为3，输出层2的神经网络，每个圈表示一个神经元，比如,,等都是神经元。上图是一个的神经网络。实际网络可以有任意的输入，任意的中间层，任意的输出数量。比如可以是这样任意的层数。
  
<p align="center"><img src="https://latex.codecogs.com/gif.latex?1000*100*10*5"/></p>  
  
  
　　图中每一条连接的线叫做**权重**，比如<img src="http://latex.codecogs.com/gif.latex?x_1->h_1"/>这条线。
  
我们表示为:
  
<img src="http://latex.codecogs.com/gif.latex?W_{x_1h_1}"/><br/>
  
　　了解了这些以后，我们来看一下神经网络的计算
  
　　神经网络是从输入层计算，到中间层，一层一层计算到输出，首先对输入层赋值，然后计算第二层，最后计算y1,y2输出。
  
h1的计算方法是：
  
假定我们用<img src="http://latex.codecogs.com/gif.latex?W_{x_ih_j}"/>代表连接<img src="http://latex.codecogs.com/gif.latex?x_i"/>和<img src="http://latex.codecogs.com/gif.latex?h_j"/>的权重，则<img src="http://latex.codecogs.com/gif.latex?h_1"/>的计算可以写为：
  
<p align="center"><img src="https://latex.codecogs.com/gif.latex?h_1=&#x5C;sum_{i=0}^4{x_iw_{x_ih_1}}+bias_{h_1}"/></p>  
  
  
本层神经元的输入定义：
  
<p align="center"><img src="https://latex.codecogs.com/gif.latex?h_j=&#x5C;sum_{i=0}^{features}{x_iw_{x_ih_j}}+bias_{h_j}"/></p>  
  
  
这里说明一下，输入层神经元下标i,输出层下标j,这样就定入了神经元的净输入，根据上面的网络图再结合公式理解。其实就是一个加权求和的过程，注意bias代表神经元的偏执。
  
**神经元的净输入**
  
 bias-偏执（表示本层每个神经元的偏执，注意，每个本层神经元都有一个偏执，就是一个数字） xi代表输入层第i个神经元的值，wij代表连接输入层第i个神经元，本层第j个神经元的权重。
  
  
  
　　每个神经元的输入，就是与这个神经元相连的上一层神经元乘以权重然后再神经元处相加，后面再加上偏执，这就是神经元的输入。
  
每个神经元的输出等于神经元输入应用一个激活函数，比如SIGMOID，公式如下：
  
<p align="center"><img src="https://latex.codecogs.com/gif.latex?output%20=%20sigmoid(input)"/></p>  
  
  
　　参数：output-输出    input-神经元输入   sigmoid-一个S形函数，原型：
<p align="center"><img src="https://latex.codecogs.com/gif.latex?y=%20&#x5C;frac{1}{1+e^{-x}}"/></p>  
  
  
神经网络就这样计算到最后一层，每条连线都会发生计算，最后到y1、y2计算出一个输出值。
  
  
  
# 2、神经网络用来干什么。
  
  
  
  
　　神经网络就是这样的一个计算网络，人们可能问，这个有什么用，网络本身可以根据一个输入，产生一个输出。
  
　　在我们上面学习的过程中，我们已经了解网络中有哪些东西可以影响输出值，不难想象，给定输入值，网络中还有权重和偏执，权重和偏执的值可以影响网络的输出。那么可以得出一个结论，调整每个权重和每个神经元的偏执可以改变网络输出。
  
　　网络是一个计算流程图，假定我们输入数组x，结果输出数组y，X和Ｙ都是一个数组，我们知道一个向量或者一个坐标点也可以数组表示，这里我们把向量或坐标Ｘ和Ｙ的映射关系表示为函数：
  
<p align="center"><img src="https://latex.codecogs.com/gif.latex?Y=net(X)"/></p>  
  
  
　　X向量经过net网络，输出Y，这样我们就可以通过一个定量的方式来表示数据，X数组的数字个数称为X的维度，那么图中X的维数是4，Y的维数是2，那么net函数的功能就是输入一个4维的点，输出一个二维的点。假定一个网络输入是M维，输出是N维，那么这个网络的功能就是输入一个M维的点，输出一个N维的点。
  
　　我们知道改变权重和偏执可以改变网络的输出，那么可以得出一个结论：通过调整权重和偏执参数，可以把网络塑造成不同的函数。
  
　　我们想象，如果左边输入的是一个图像的像素数组，大家都知道像素是０－２５５的数字。假如我们有一个100*100的图像，我们定义一个 <p align="center"><img src="https://latex.codecogs.com/gif.latex?10000%20*%201000%20*%20100%20*%202"/></p>  
 的网络，我们期望能通过调整参数的方式，让函数具有这样的功能：当左边输入人的图片时，结果输出<p align="center"><img src="https://latex.codecogs.com/gif.latex?(1,0)"/></p>  
这个点，当输入汽车时，结果输出<p align="center"><img src="https://latex.codecogs.com/gif.latex?(0,1)"/></p>  
，也就是说，可以用函数来分类，输入一个图像，让函数输出结果成为对应的类型，可以识别图像是人还是车。
  
如果我们不做任何操作，那么网络是办不到的，因为它的计算结果我们无法确定，那么我们要改变这种计算结果，调整里面的权重和偏执就可以办到，可以将权重和偏执调整，然后网络就可以识别了。调整权重和偏执的值可以改变网络的输出，那么怎么调整就成为关键，调整参数的目标是让网络按我们预期的输出，具体的来说，我们希望通过调整参数，能让这个网络输入图像像素数组，输出类别<p align="center"><img src="https://latex.codecogs.com/gif.latex?(0,1)"/></p>  
还是<p align="center"><img src="https://latex.codecogs.com/gif.latex?(1,0)"/></p>  
，是人还是车。
在实际网络中，输出的点不一定是以上的，那么我们可以让输出的点与上面两个点做一个度量，离代表人的点的距离与代表车的点的距离，离谁近，就判断是哪类。
  
# 3、调整参数，让网络计算的输出按我们预期的那样。
  
  
  
  
我们调整参数也不能乱调，因为乱调是没有结果的。那么我们调整一个参数是否有效怎么来判断呢？
  
比如：我们输入人的像素，我们希望经过网络以后，输出是<p align="center"><img src="https://latex.codecogs.com/gif.latex?(1,0)"/></p>  
，当我们输入是车，希望经过输出结果是<p align="center"><img src="https://latex.codecogs.com/gif.latex?(0,1)"/></p>  
。
  
下面就来看看我们怎么调整参数。
  
我们开始输入一张人的图片，输出一个<p align="center"><img src="https://latex.codecogs.com/gif.latex?(y_1,y_2)"/></p>  
，那么开始输出的<p align="center"><img src="https://latex.codecogs.com/gif.latex?(y_1,y_2)"/></p>  
不是<p align="center"><img src="https://latex.codecogs.com/gif.latex?(1,0)"/></p>  
，我们想通过不断调整权重和偏执让它变为<p align="center"><img src="https://latex.codecogs.com/gif.latex?(1,0)"/></p>  
，我们有办法吗？
  
我们就要找差距，我们用<p align="center"><img src="https://latex.codecogs.com/gif.latex?(1,0)"/></p>  
 <p align="center"><img src="https://latex.codecogs.com/gif.latex?(y_1,y_2)"/></p>  
，两个点距离公式:    
<p align="center"><img src="https://latex.codecogs.com/gif.latex?L%20=%20&#x5C;sqrt{(1-y_1)^2%20+%20(0-y_2)^2}"/></p>  
  
代表差距，这个不会说了吧，我们可以把我们的输出和希望的输出得出一个距离，这个距离就是输出和目标的差距离，我们用LOSS来表示，专业术语叫做损失。我们只要调整权重不断的减小这个损失，就可以能让网络更接近我们的目标。
  
我们先来看一种笨办法，我们随机选一个权重，我们让它变大一点，计算出一个LOSS，让它变小一点计算出一个LOSS，两个LOSS比较一下，如果谁小就说明谁离调整的目标更近，就是有效的更新，如果通过暴力计算，我们对每个权重和偏执做调整 。让LOSS变得最小，那么我们的函数就最接近我们的预期，比如我们输入人和输的图片，输出的点离<p align="center"><img src="https://latex.codecogs.com/gif.latex?(1,0)"/></p>  
近，说明是人，离<p align="center"><img src="https://latex.codecogs.com/gif.latex?(0,1)"/></p>  
近，说明是车。这样，我们就有一个识别网络。我们把调整参数，让LOSS最小的动作叫训练。
  
　　现在的问题成为，如何调整参数让：目标与输出距离缩小。不断调整参数让预期点与输出的点的距离缩小。
  
　　我们定义了LOSS，LOSS称为损失。
  
　　我们复习一下函数的定义，自变量X和因变量Y。X->Y的映射F叫(X,Y)的函数。
  
　　对于某次固定的输入值，我们把权重W看成自变量，LOSS看成因变量，那么我们把它写成函数：
  
<p align="center"><img src="https://latex.codecogs.com/gif.latex?LOSS%20=%20F(W)"/></p>  
  
  
　　我们看到这个函数以后，我们要让LOSS变小，那么我们怎么调整W呢？我们学过导数知道,dy/dx，也就说是说，我们把x往导数反方向移动，可以让函数值变小，那么我们就这样调整：对于 y=f(x)来说：x0 = x0 - (dy/dx) * delta ，delta是一个很小量，这样就能减小y值，同理，我们的LOSS求对W的导数，将W值往反向调整，也可以减少LOSS，这样我们就有了调整W的方法，这样，我们就有办法调整W让LOSS减小了。
  
　　这就是反向传播算法BP。BP主要是求LOSS对每个权重和偏执参数的偏导数，并把参数往偏导数的反向调整减小以减小LOSS，这样我们求出偏导数就可以对参数进行更新了。
  
BP算法是部分神经网络调整参数的一种方法，其核心思想是通过计算参数的偏导数来调整参数降低损失值。
  
下次我讲讲ＢＰ算法。
  
　　有问题也欢迎加入深度学习与人工智能交流群，一起交流学习讨论，QQ群号码 374685750。谢谢大家的支持，我有时间会发更多的文章，谢谢大家的支持。
  
　　本文可以转载，但是必须声明出处链接和说明；
  
关于ML4AI
  
网站：www.ml4ai.com
  
代码: https://gitee.com/sleechengn/ml4ai
  
  
  
  
  
  