# 第一章

## 行列式

---

&#8195;&#8195;本章主要介绍n阶行列式的定义、性质及其计算方法，此外还要介绍用n阶行列式求解n元线性方程组的克拉默(Cramer)法则。

## 1、二、三阶行列式


### 一、二元线性方程组与二阶行列式。


用消元法解二元线性方程组

<p align="center"><img src="https://latex.codecogs.com/gif.latex?&#x5C;begin{cases}%20		a_{11}x_1+a_{12}x_2=b_1&#x5C;&#x5C;%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20a_{21}x_1+a_{22}x_2=b_2	&#x5C;end{cases}"/></p>  

<p align="center">(1)</p>

&#8195;&#8195;为消去未知数<p align="center"><img src="https://latex.codecogs.com/gif.latex?x_2"/></p>  
，分别以<p align="center"><img src="https://latex.codecogs.com/gif.latex?a_{22}"/></p>  
和<p align="center"><img src="https://latex.codecogs.com/gif.latex?a_{12}"/></p>  
乘以方程的两端，然后两个方程相减，得

<p align="center"><img src="https://latex.codecogs.com/gif.latex?(a_{11}a_{22}%20-%20a_{21}a_{12})x_1%20=%20a_{22}b_1%20-%20a_{12}b_2"/></p>  


类似的消去<p align="center"><img src="https://latex.codecogs.com/gif.latex?x_1"/></p>  
得

<p align="center"><img src="https://latex.codecogs.com/gif.latex?(a_{12}a_{21}%20-%20a_{11}a_{22})x_2=b_1a_{21}%20-%20a_{11}b_2"/></p>  


当<p align="center"><img src="https://latex.codecogs.com/gif.latex?a_{11}a_{22}-a_{21}a_{12}"/></p>  
不为0时<p align="center"><img src="https://latex.codecogs.com/gif.latex?x_1"/></p>  
的解是：

<p align="center"><img src="https://latex.codecogs.com/gif.latex?x_1=&#x5C;frac{b_1a_{22}-a_{12}b_2}{a_{11}a_{22}-a_{21}a_{12}}"/></p>  
,
<p align="center"><img src="https://latex.codecogs.com/gif.latex?x_2=&#x5C;frac{b_1a_{21}-a_{11}b_2}{a_{12}a_{21}-a_{11}a_{22}}"/></p>  


<p align="center">(2)</p>

&#8195;&#8195;(2)式中的分子、分母都是四个数分两对相乘再相减而得,其中分母是由方程组(1)四个系数确定的，把这四个数按它们在方程组(1)的位置排成二行二列(横排的称为行，坚排的称为列)的数表

<p align="center"><img src="https://latex.codecogs.com/gif.latex?&#x5C;begin{matrix}%20%20%20%20%20%20%20%20%20%20a_{11}&amp;a_{12}&#x5C;&#x5C;%20%20%20%20%20%20%20%20%20%20a_{21}&amp;a_{22}%20%20%20%20%20%20%20%20%20%20&#x5C;end{matrix}"/></p>  
,

<p align="center">(3)</p>

&#8195;&#8195;表达式<p align="center"><img src="https://latex.codecogs.com/gif.latex?a_{11}a_{22}-a_{12}a_{21}"/></p>  
称为数表(3)所确定的二阶行列式，并记作

<p align="center"><img src="https://latex.codecogs.com/gif.latex?&#x5C;left|%20&#x5C;begin{matrix}%20%20%20%20%20%20%20%20%20%20a_{11}&amp;a_{12}&#x5C;&#x5C;%20%20%20%20%20%20%20%20%20%20a_{21}&amp;a_{22}%20%20%20%20%20%20%20%20%20%20&#x5C;end{matrix}%20%20%20%20%20&#x5C;right|"/></p>  


<p align="center">(4)</p>

&#8195;&#8195; 数<p align="center"><img src="https://latex.codecogs.com/gif.latex?a_{ij}(i=1,2;j=1,2)"/></p>  
称为行列式(4)的元素或元。
