# quadratic-network
#二阶网络介绍
二阶网络是传统网络结构的一种推广形式。在《Universal Approximation with Quadratic Deep Networks》一文中指出，二阶网络的参数数量仅为同结构普通网络参数的三倍，但是表示函数的效果却优秀许多。在都使用单隐层网络结构，且拟合精确度相同的情况下，二阶网络对任一径向基函数的拟合所需要的神经元个数是参数的常数倍，而一阶段网络所需要神经元个数为指数倍。这证明了二阶网络的优越性。
#简介
quad-gan-net从基础GAN生成对抗网络结构出发，将网络中的卷积层依次替换为二阶网络并进行实验。
quad—vgg—net使用的vgg16网络结构，改变卷积层以及全连接层为二阶网络进行实验，在cifar-10数据集上的测试，二阶网络严格优于一阶
quad-acgan——net对生成器于判别器分别使用了二阶网络，可以更快的生成肺结节图片数据，且对于判别器的分类作用而言，效果比一阶网络好
