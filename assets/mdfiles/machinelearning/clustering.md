# 聚类


　　聚类是依据数据之间通过某种度量，两两度量值较小的归为一类的分类，它可以实现自动分类，一般来说我们可以通过欧氏度量聚类也可以通过其它度量如相似度来进行聚类。聚类中的无监督学习是一种非常重要的机器学习方式，通过聚类，我们可以对数据进行自动分类，避免了人为分类的麻烦。

　　点：

<p align="center"><img src="https://latex.codecogs.com/gif.latex?X(x_1,x_2,x_3,x_4,...)"/></p>  


到点

<p align="center"><img src="https://latex.codecogs.com/gif.latex?Y(y_1,y_2,y_3,y_4,...)"/></p>  


欧氏距离公式：

<p align="center"><img src="https://latex.codecogs.com/gif.latex?L=&#x5C;sqrt{&#x5C;sum_{i=1}^{n}(x_i-y_i)^2}"/></p>  


　　在通过欧氏距离聚类的时候，距离近的点一般来说，会归为一类。

　　比如以下的点分为两类

<p align="center"><img src="https://latex.codecogs.com/gif.latex?(0,1),(0,1.2),(0.1,0.98),(0.1,1.1),(3,2),(3.3,2.1),(3.5,1.7)"/></p>  


其中

<p align="center"><img src="https://latex.codecogs.com/gif.latex?(0,1),(0,1.2),(0.1,0.98),(0.1,1.1)"/></p>  


会被分为一类，其余的为另一类，因为它们的数据相似度较高。

