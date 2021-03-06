> 《Quaternion kinematics for the error-state Kalman filter 》
>
> Joan Sol`a 
>
> November 8, 2017 



#### 1.1 Definition of quaternion

One introduction to the quaternion that I find particularly attractive is given by the Cayley- Dickson construction: If we have two complex numbers A = a + bi and C = c + di, then constructing Q = A + Cj and defining k , ij yields a number in the space of quaternions H, 

​						$Q = a + bi + cj + dk \in  H ,$ 

where {a, b, c, d} 2 R, and {i, j, k} are three imaginary unit numbers defined so that 

$i2 =j2 =k2 =ijk=1,$ 

$ij=ji=k, jk=kj=i, ki=ik=j.$



纯虚四元数

$Q=bi+cj+dk \in Hp ---H.$

----

$z=e^{i\theta}$ 可代表二维平面的旋转，$x^{'} = z.x$

$q = e(u_xi+u_yj+u_zk)\theta/2$ 可代表三维旋转,  $x^{'} = q\otimes x\otimes q^{*}$,

四元数

$Q=q_w +q_xi+q_yj+q_zk , Q=q_w +q_v ,$ 

$Q = <q_w,q_v> $
$$
q=\begin{bmatrix}
q_w\\ q_v
\end{bmatrix} =\begin{bmatrix}
q_w\\q_x 
\\q_y 
\\q_z 
\end{bmatrix}
$$
![image-20190313104732688](/Users/test/Downloads/7-TestCode/__notebook/Quaternions/image-20190313104732688-2445252.png)

#### 1.2 quaternion properties

![image-20190313104911948](/Users/test/Downloads/7-TestCode/__notebook/Quaternions/image-20190313104911948-2445351.png)

![image-20190313105014619](/Users/test/Downloads/7-TestCode/__notebook/Quaternions/image-20190313105014619-2445414.png)

![image-20190313105226876](/Users/test/Downloads/7-TestCode/__notebook/Quaternions/image-20190313105226876-2445546.png)

总结一下：

- 四元素没有交换律只有结合律
- 注意qL和qR怎么写，他们两都是反对称矩阵
- (17)很重要
- 可以得出左右四元素的乘积等价于四元素对应的矩阵交换

![image-20190313105726665](/Users/test/Downloads/7-TestCode/__notebook/Quaternions/image-20190313105726665-2445846.png)



#### 1.23  Identity

是一个实数$q1 = [1, 0 ]T$

$q1*q = q *q1 = q$



#### 1.24 共轭Conjugate

- 注意定义
- 有交换律

![image-20190313110547502](/Users/test/Downloads/7-TestCode/__notebook/Quaternions/image-20190313110547502-2446347.png)

![image-20190313110745423](/Users/test/Downloads/7-TestCode/__notebook/Quaternions/image-20190313110745423-2446465.png)

- 共轭开方



![image-20190313110913877](/Users/test/Downloads/7-TestCode/__notebook/Quaternions/image-20190313110913877-2446553.png)

- 四元素的逆的定义： q*q的共轭 = 单位四元素
- 有交换律
-  熟记（29）



![image-20190313111312755](/Users/test/Downloads/7-TestCode/__notebook/Quaternions/image-20190313111312755-2446792.png)

- ==归一化的四元素，其逆 = 其共轭 $q^{-1} = q^{*}​$==

- unit quaternion 虚部是单位向量 和一个夹角构成

----

#### 1.3 四元素其他一些性质

##### 1.3.1 四元素换向器

![image-20190313112350073](/Users/test/Downloads/7-TestCode/__notebook/Quaternions/image-20190313112350073-2447430.png)

##### 1.3.2 纯虚四元素的乘积

![image-20190313112604947](/Users/test/Downloads/7-TestCode/__notebook/Quaternions/image-20190313112604947-2447565.png)

![image-20190313112918429](/Users/test/Downloads/7-TestCode/__notebook/Quaternions/image-20190313112918429-2447758.png)

- $a X a = 0$所以有式子35

##### 1.3.3 纯虚四元素的幂级数

![image-20190313114001314](/Users/test/Downloads/7-TestCode/__notebook/Quaternions/image-20190313114001314-2448401.png)



##### 1.3.4  四元数指数是一个关于四元数的函数，类似于普通指数函数。与实指数情况完全一样，它被定义为绝对收敛幂级数

![image-20190313115009523](/Users/test/Downloads/7-TestCode/__notebook/Quaternions/image-20190313115009523-2449009.png)

![image-20190313125242660](/Users/test/Downloads/7-TestCode/__notebook/Quaternions/image-20190313125242660-2452762.png)

#####1.3.5一般四元数的指数

![image-20190313125340262](/Users/test/Downloads/7-TestCode/__notebook/Quaternions/image-20190313125340262-2452820.png)

![image-20190313125506940](/Users/test/Downloads/7-TestCode/__notebook/Quaternions/image-20190313125506940-2452907.png)

