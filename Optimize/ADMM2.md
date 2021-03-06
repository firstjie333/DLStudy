## 4. Consensus and Sharing

==本节讲述的两个优化问题，是非常常见的优化问题，也非常重要，我认为是ADMM算法通往并行和分布式计算的一个途径：consensus和sharing，即一致性优化问题与共享优化问题。==

## Consensus

### 4.1 全局变量一致性优化（Global variable consensus optimization）（切割数据，参数（变量）维数相同）

所谓全局变量一致性优化问题，即目标函数根据数据分解成N子目标函数（子系统），每个子系统和子数据都可以获得一个参数解xi，但是全局解只有一个z，于是就可以写成如下优化命题：

![image-20181219161458671](/Users/test/Downloads/7-TestCode/__notebook/Optimize/image-20181219161458671-5207298.png)

![image-20181219161616838](/Users/test/Downloads/7-TestCode/__notebook/Optimize/image-20181219161616838-5207376.png)



==这种迭代算法写出来了，并行化那么就是轻而易举了，各个子数据分别并行求最小化，然后将各个子数据的解汇集起来求均值，整体更新对偶变量yk，然后再继续回带求最小值至收敛。当然也可以分布式部署（hadoop化），但是说起来容易，真正工程实施起来又是另外一回事，各个子节点机器间的通信更新是一个需要细细揣摩的问题。==

另外，对于全局一致性优化，也需要给出相应的终止迭代准则，与一般的ADMM类似，看primal和dual的residuals即可

![image-20181219161804120](/Users/test/Downloads/7-TestCode/__notebook/Optimize/image-20181219161804120-5207484.png)

### 4.2 带正则项的全局一致性问题

下面就是要将之前所谈到的经典的机器学习算法并行化起来。想法很简单，就是对全局变量加上正则项即可，因此ADMM算法只需要改变下zz-update步即可

![image-20181219161827231](/Users/test/Downloads/7-TestCode/__notebook/Optimize/image-20181219161827231-5207507.png)

**切割大样本数据，并行化计算**

在经典的统计估计中，我们处理的多半是大样本低维度的数据，现在则多是是大样本高维度的数据。对于经典的大样本低维度数据，如果机器不够好，那么就抽样部分数据亦可以实现较好估计，不过如果没有很好的信息，就是想要对大样本进行处理，那么切割数据，并行计算是一个好的选择。现在的社交网络、网络日志、无线感应网络等都可以这么实施。下面的具体模型都在受约束的凸优化问题中以及ℓ1-norm问题中提过，此处只不过切割数据，做成分布式模型，思想很简单，与带正则项的global consensus问题一样的处理。经典问题lasso、sparse logistic lasso、SVM都可以纳入如下框架处理。

![image-20181219162056549](/Users/test/Downloads/7-TestCode/__notebook/Optimize/image-20181219162056549-5207656.png)

![image-20181219162113843](/Users/test/Downloads/7-TestCode/__notebook/Optimize/image-20181219162113843-5207673.png)





### 4.3 一般形式的一致性优化问题（切割参数到各子系统，但各子系统目标函数参数维度不同，可能部分重合）

上述全局一致性优化问题，我们可以看到，所做的处理不过是对数据分块，然后并行化处理。但是更一般的优化问题是，参数空间也是分块的，即每个子目标函数fi(xi)的参数维度不同xi,∈Rni我们称之为局部变量。而局部变量所对应的的也将不再是全局变量z，而是全局变量中的一部分zg，并且不是像之前的顺序对应，而可能是随便对应到zz的某个位置。可令g=G(i,⋅)，即将xixi映射到z的某部位

![image-20181219162241277](/Users/test/Downloads/7-TestCode/__notebook/Optimize/image-20181219162241277-5207761.png)

后续想做平均化处理，即中间会发生重合的参数zizi取值一样的，那么zz-update将只能找他对应的那些xx进行平均化，也就是变成局部了，因为不是所有值都是要全局保持一致的。比如上面那个图中的z1,z2,z3,z4都分别只要求在部分xixi发生了共享需要保持一样，而不是像之前全局要求每个xi对应的都是z。即

![image-20181219162319801](/Users/test/Downloads/7-TestCode/__notebook/Optimize/image-20181219162319801-5207799.png)

## Sharing

### 4.4 共享问题（sharing）（横向切割数据，也可纵向切变量）

与之前的全局变量一致性优化问题类似，共享问题也是一个非常一般而且常见的问题。他的形式如下：

![image-20181219185707486](/Users/test/Downloads/7-TestCode/__notebook/Optimize/image-20181219185707486-5217027.png)

本节开头提过，sharing问题用来切分数据做并行化，也可以切分参数空间做并行化。这对于高维、超高维问题是非常有好处的。因为高维统计中，大样本是一方面问题，而高维度才是重中之重，如果能切分特征到低纬度中去求解，然后在合并起来，那么这将是一个很美妙的事情。上面利用regularized global consensus问题解决了切分大样本数据的并行化问题，下面利用sharing思想解决常见的高维数据并行化问题



**切割变量（特征）空间，并行化处理**

同样假设面对还是一个观测阵A∈Rm×nA∈Rm×n和响应观测b∈Rnb∈Rn，此时有n»mn»m，那么要么就降维处理，要么就切分维度去处理，或者对于超高维矩阵，切分维度后再降维。此时AA矩阵就不是像之前横着切分，而是竖着切分，这样对应着参数空间的切分：



