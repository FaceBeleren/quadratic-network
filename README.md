# quadratic-network
## 二阶网络介绍
二阶网络是传统网络结构的一种推广形式。在[《Universal Approximation with Quadratic Deep Networks》](https://arxiv.org/abs/1808.00098)一文中指出，二阶网络的参数数量仅为同结构普通网络参数的三倍，但是表示函数的效果却优秀许多。在都使用单隐层网络结构，且拟合精确度相同的情况下，二阶网络对任一径向基函数的拟合所需要的神经元个数是参数的常数倍，而一阶段网络所需要神经元个数为指数倍。这证明了二阶网络的优越性。
## 代码介绍
### quad-gan-net
从基础GAN生成对抗网络结构出发，将网络中的卷积层依次替换为二阶网络并进行实验。\
代码遵循原始GAN网络论文中的结构进行搭建，初始化数据分布为正态分布，初始化生成器为线性分布。\
生成器使用三层隐藏结构，判别器使用4层隐藏结构，生成器使用三层隐藏结构，使得在线性网络的情况下，判别器可以正确判别出生成器的复杂度，生成器的生成图像不至于完全无法欺骗判别器。\
使用相同的优化参数控制变量，收集生成器，判别器，以及均方误差损失
>在GAN原文中，作者设计了这样的一个网络结构，利用等差数列分布设置为初始生成器分布，去学习一个被设定为正态分布函数的初始输出分布。其中生成器和判别器都设计为简单的多层感知机结构，生成器的激活函数使用的是softplus，而判别器使用的为tanh，最后一层用sigmoid函数将判别器输出结果映射到0，1之间，反映判别器对输入值的判别：是原始数据分布还是经过生成器生成的分布。判别器目的是分辨出数据来源，而生成器目标是学习到一个最佳的对初始分布的拟合，使得生成的数据可以骗过判别器。\
其中可以改变的参数为：生成器与判别器网络层数，每段不同的激活函数，训练步数与步进数等等。引入二阶网络后还可以改变的是不同网络层中是否使用二阶网络。改变超参数会导致生成器的效果的改变。为了证明二阶网络的优越性，在该实验中，我们可以控制其他超参数不变，单独判定某个网络结构使用二阶的效果与该处网络结构不使用二阶的效果的对比，其中的判别标准即为各采样点与对应点实际值的均方误差。\
在共享的超参数设置为：初始分布为均值为4方差为0.5的正态分布，初始生成器在[-8,8]进行了平均的12个采样，生成器使用三层感知机，单层节点个数为4；为保证判别器能够准确判别，判别器参数规模要比生成器大。判别器使用四层感知机，单层节点个数为8。\
我们分别对比了生成器第一层，一二两层，生成器全体，判别器第一层，第二层，以及全体使用二阶网络的网络结构与初始线性结构的对比
### quad—vgg—net
使用的vgg16网络结构，改变卷积层以及全连接层为二阶网络进行实验，在cifar-10数据集上的测试，二阶网络严格优于一阶\
![线性网络准确率](https://img-blog.csdnimg.cn/20201214103838169.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2RhdmlkMTk5NjA1MTY=,size_16,color_FFFFFF,t_70)
### quad-acgan——net
对生成器于判别器分别使用了二阶网络，可以更快的生成肺结节图片数据，且对于判别器的分类作用而言，效果比一阶网络好\
网络结构来源[《Quadratic Autoencoder (Q-AE) for Low-dose CT Denoising》](https://arxiv.org/abs/1901.05593)

