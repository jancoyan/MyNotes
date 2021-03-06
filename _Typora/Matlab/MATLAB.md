# MATLAB

## Matlab基础知识

> 科学计算软件

### 常识

变量命名：

- 大小写敏感
- 第一个字母必须是英文字母
- 可以有英文字母、下划线、数字
- 变量名最多63个字符

### 常见的通用命令

| 命令      | 含义                      |
| --------- | ------------------------- |
| clc       | 清除命令行窗口的内容      |
| clear     | 清除workspace中的所有变量     |
| clear x y z... | 清除workspace中的变量x, y, z等     |
| who、whos | 显示workspace中的变量信息 |
| help、doc | 在线帮助文档              |

- 一行中可以写多个命令，用分号隔开
- 用分号隔开的命令不会显示变量的值
- 较长的表达式可以在行尾加上三点（ ... ）省略号进行续行输入

路径相关问题

```matlab
path % 查看搜索路径
cd % 当前工作目录

userpath('Path') % 修改当前工作路径
savepath % 保存路径修改

pathtool % 打开路径管理工具的图形化窗口
```



**精度控制**

默认数据类型为 `double`

默认是4位小数精度 `short` 格式精度，可以改为15位精度 `format long`，或者四舍五入保留两位小数`format bank`, 用指数形式表示并且精确到4位/15位小数: `format short e` 、`format long e`



**逻辑表达式**

& 与，| 或，~ 非，xor 异或

**比较**

<  > <= >= ==  ~= (不等于)

关系运算符的运算方式

- 两个标量直接比较
- 位数相等的矩阵进行比较，生成 01 矩阵
- 标量和矩阵比较，一对多比较，生成01矩阵



### 一些数学函数和变量

| 函数                      | 作用                                 |
| ------------------------- | ------------------------------------ |
| exp(a)                    | e的a次方                             |
| rem(A, 3)                 | 返回A矩阵除 3 的余数（变量或者矩阵） |
| log10(x)                  | 以10为底的x的对数                    |
| log(x)                    | x的自然对数                          |
| sin(x) ; cos(x) ; tan(x)  | 三角函数（弧度）                     |
| asin(s); acos(x); atan(x) | 反三角函数（弧度）                   |

| 变量名 | 意义                      |
| ------ | ------------------------- |
| ans    | 最近计算的结果            |
| eps    | 正数的极小值 = 2.2204e-16 |
| pi     | Π                         |
| inf    | ∞                         |
| i、j   | 虚数单位                  |
| NaN    | not a number              |

- matlab启动时加载这些变量
- 被0除不会引起程序中断
- 用户可以临时覆盖这些变量， 但是在重启matlab或者clear之后会重新加载

左除和右除是不一样的， `a/b` 是右除，表示a/b, `a\b` 是左除，表示 b/a



### 复数运算

| 函数     | 作用                   |
| -------- | ---------------------- |
| real(z)  | 实部（笛卡尔坐标表示） |
| imag(z)  | 虚部（笛卡尔坐标表示） |
| angle(z) | 幅角（极坐标表示）     |
| abs(z)   | 模（极坐标表示）       |

## 向量与矩阵

| 语句                           | 作用                        |
| ------------------------------ | --------------------------- |
| `x = [1 2 3] 、 x = [1, 2, 3]` | 创建行向量                  |
| `x = [1; 2; 3]`                | 创建列向量                  |
| x' (单引号)                    | 转置                        |
| x = [1 2 3]'                   | 创建列向量                  |
| x(a, b)                        | 取出x向量的第a行第b列的数值 |

从已有变量创建新变量 `a = [1 2 3]; b = [2 3 4] c = [a; b];` 用空格链接表示并排组合，用分号连接表示上下组合排列

**创建等差元素的向量**

首元素为x1，跨度为q，q默认为1，末尾元素为x2，左闭右闭。

`x = [x1: q: x2]`

注意：向量的乘方应该在运算符前面加上句号（.）

| 语句              | 作用                            |
| ----------------- | ------------------------------- |
| linspace(a, b)    | 创建a和b之间含有100个元素的向量 |
| linspace(a, b, n) | 创建a和b之间含有n个元素的向量   |
| logspace(a, b, n) | 创建n个对数值相隔相同的向量     |

**函数创建向量**

`help elmat` 获取的矩阵生成和操作函数列表

| 函数                      | 作用            |
| ------------------------- | --------------- |
| ones(n)， ones(m,n)       | 生成全是1的矩阵 |
| zeros(n)，zeros(m,n)      | 生成全是0的矩阵 |
| reshape(n), reshape(m, n) | 重塑矩阵        |
| eye(n)                    | 生成单位矩阵    |

reshape：

- 数组元素的排列顺序从上到下按列排列
- 数组的元素总数不变

**向量的访问**

| 语句             | 作用                                                         |
| ---------------- | ------------------------------------------------------------ |
| a(n)             | 寻访第n个元素                                                |
| a(:)             | a的所有元素按列组合组成的向量                                |
| a(n) = m         | m的值赋给a(n)                                                |
| a([n m]) = [p q] | p赋值n，p赋值给m                                             |
| a([n1 n2 n5])    | 寻访第1，2，5个元素组成的子数组                              |
| a(n: m)          | 寻访第n到m个元素组成的子数组 [n, m]                          |
| a(n : d: m)      | 从n到m，按照下表递增d的方式组成子数组，d可以为负数           |
| a(n: end)        | 返第3个(包括)到最后的子数组，end表示最后一个，不是具体值，end可以参与表达式 |

注意：

- 数组元素可以被任意重复访问，构成长度大于原数组的新数组
  - `a([1 1 1 2 3 4 5 5 5])` 像这样，是可以的
- 下标值不可以越界，且只能取正整数或者逻辑值，下标从1开始

```matlab
a = [1 2 3 4 5; 1 2 3 4 5];
a(:,[2 3]);  % 第一个下表表示对于变量a中【所有的列】，第二个变量表示第2列和第3列
	1 (2 3) 4 5
	1 (2 3) 4 5
% 也就是括号括起来的部分
```

**双下标和单下标的转换**

sub2ind() 函数

```matlab
a = [1 2 3 4; 4 3 3 3; 5 6 6 6];
a(:, :, 2) = a - 10; % 用赋值的方式把二维数组变为三维数组，排列方式为“从前到后”
%a(所有行，所有行的所有列，第二页的值) = a - 10
% 也就是把第二页的所有元素赋值为 第一页-10
% 这时候，从前到后看数组为：
```

$$
第一页：
\begin{bmatrix}
1 & 2 &3 & 4 \\
4 & 3 & 3 & 3 \\
5 & 6 & 6 &6 \\
\end{bmatrix}
第二页：
\begin{bmatrix}
-9 & -8 & -7 & -6 \\
-6 & -7 & -7 & -7 \\
-5 & -4 & -4 & -4 \\
\end{bmatrix}
$$

```matlab
a(2, 1, 2); % 第2行第1列第2页，也就是 -6
sub2ind(size(a), 2, 1, 2); % 用单下标访问变量a中(2, 1, 2)位置的数据，返回这个单下标的大小
a(14); % 单下标14也就对应三维下标的 (2, 1, 2)
```

**单下标到双下标**

ind2sub() 函数

```matlab
b = zeros(3);
b(:) = 1:9;
ind = [3 4 5 6];
[x, y] = ind2sub(size(b), ind);
```

$$
结果为：
\\ x = 
\begin{bmatrix}
3&1&2&3
\end{bmatrix}
\\y =
\begin{bmatrix}
1&2&2&2
\end{bmatrix}
$$


$$
解读：ind为索引，其值为 [3\ 4\ 5\ 6]意为在单下标表示中第 3\ 4\ 5\ 6个下标对应的数据。\\
原数据为：
\begin{bmatrix}
1 & 4 & 7\\
2 & 5 & 8\\
3 & 6 & 9
\end{bmatrix}\\也就是说，第 3\ 4\ 5\ 6个下标对应的数据，他们的二维索引分别为(列优先)：\\
\begin{bmatrix}3&1\end{bmatrix}\ 
\begin{bmatrix}1&2\end{bmatrix}\ 
\begin{bmatrix}2&2\end{bmatrix}\ 
\begin{bmatrix}3&2\end{bmatrix}\\
也就是：\\
\begin{bmatrix}3\\1\end{bmatrix}\ 
\begin{bmatrix}1\\2\end{bmatrix}\ 
\begin{bmatrix}2\\2\end{bmatrix}\ 
\begin{bmatrix}3\\2\end{bmatrix}\\
亦即：\\
\begin{bmatrix}
3 & 1 & 2 & 3\\
1 & 2 & 2 &2
\end{bmatrix}
$$

**找到指定区间内的向量的位置**

```matlab
A = [4, 15, -45, 10, 6; 56, 0, 17, -45, 0];
find(A >= 10 & A < 20) %找到非0元素的位置
```

**注意：元素是按列排的**





### **特征化向量**

向量的*操作前面要加上点号

| 语句          | 作用                       |
| ------------- | -------------------------- |
| length(A)     | 返回向量的最大维数         |
| size(A)       | 返回向量的大小（行和列数） |
| max(A)/min(A) | 向量中最大最小的元素       |

如果变量中有复数，在用（.*）计算模的时候必须计算其共轭复数，用原向量 .\*共轭向量

`conj(A)` 计算A向量的共轭复数向量

`abs(A)` A向量的绝对值





### **向量的点乘和叉乘**

| 语句      | 作用                 |
| --------- | -------------------- |
| dot(a, b) | a和b的点乘（数量积） |

dot(a, a) 计算向量的模，适用于复数向量



### 空向量

- 有一维是0的数组
- 不占存储空间
- 最简单的空数组 0*0 的矩阵
- 复杂的空数组：有一位是0的矩阵（0 * 7 * 8的矩阵）
- 空数组不是全0数组

**数组降维**







### 字符矩阵

- 单引号界定一个字符串
- 方括号直接连接多个字符串变量
- 字符串中的单引号要用两个单引号（但是计算的时候按照一个单引号计算）
- length(A) 计算字符串长度

| 函数           | 作用                            |
| -------------- | ------------------------------- |
| double(string) | 查看ASCII码                     |
| char(A)        | 将ASCII码数组恢复成字符串的形式 |
| class(A)       | 判断A变量的类型                 |
| char(X)        | 判断X是不是char型               |

**一个变量存储多个字符串**

1. 可以用二位字符数组 `str = ['asd'; 'a  '; ' b ']`
   - 这个时候应该保证每个字符串的长度一样
   - 否则应该补齐短的
2. 可以使用 `char()`
   - 这个时候不用保证长度一样，因为函数会自动帮我们补齐
   - `str = char('asd', 'a', ' b')` 

| 函数         | 作用         |
| ------------ | ------------ |
| deblank(str) | 清除尾部空格 |

`str(1, :)` 第一行的全部元素，也就是第一个字符串

访问二维字符串的时候别忘了清楚尾部空格



| 函数               | 作用                             |
| ------------------ | -------------------------------- |
| strcmp(str1, str2) | 比较字符串，相同返回1，不同返回0 |





## 数据分析和统计



**对于一维数组**

| 函数            | 作用                                          |
| --------------- | --------------------------------------------- |
| y = max(X)      | X最大值赋给y，复数应取模                      |
| [y, I] = max(X) | X最大值赋给y，最大值的下表给I，按照模取最大值 |
| min 和以上同理  |                                               |
| sum(X)          | 向量的所有元素的和                            |
| prod(X)         | 向量的所有元素的乘积                          |
| mean(X)         | 向量的所有元素的算数平均值                    |
| median(X)       | 向量的所有元素的算数中间值                    |



**对于矩阵**

| 函数            | 作用                                                         |
| --------------- | ------------------------------------------------------------ |
| X = max(A)      | 返回每一列上的最大值组成的行向量                             |
| [Y, U]          | 返回每一列上的最大值组成的行向量，和他们的行号               |
| max(A, [], dim) | dim 取 1或2. 取1的时候等效于max(A); 取2的时候，返回一个列向量，其中第i个元素是A矩阵的第i行上的最大值 |
| min同理         |                                                              |
| sum(A)          | 返回每一列的所有元素的和组成的行向量                         |
| prod(A)         | 返回每一列的所有元素的积组成的行向量                         |
| mean(A)         | 返回每一列的所有元素的平均值组成的行向量                     |
| median(A)       | 返回每一列的所有元素的中位数组成的行向量                     |
| sum(A, dim)     | 求和，同理                                                   |
| prod(A, dim)    | 求积，同理                                                   |
| mean(A, dim)    | 平均值，同理                                                 |
| median(A, dim)  | 中位数，同理                                                 |



## 数据可视化

### plot

**plot(x)**

- x为向量时，以该元素的下标为横坐标、元素值为纵坐标绘出曲线

- x为实数二维数组时，则按列绘制每列元素值相对其下标的曲线，曲线数等于x数组的列数。

- x为复数二维数组时，则按列分别以数组的实部和虚部为横、纵坐标绘制多条曲线

**plot(x, y)**

- x、y为同维数组时，绘制以x、y元素为横纵坐标的曲线

- x为向量，y为二维数组、且其列数或行数等于x的元素数时，绘制多条不同颜色的曲线

- x为二维数组，y为向量时，情况与上相同，只是y仍为纵坐标。

```matlab
x = 0:pi/100:2*pi;
y = 2*exp(-0.5*x).*sin(2*pi*x);
plot(x, y)
```

<img src=".\MATLAB.imgs\image-20210322161050827.png" alt="image-20210322161050827" style="zoom: 50%;" />

参数方程的绘制：
$$
\begin{cases} 
x = tcos(3t)\\
t = tsin^2(t)
\end{cases}, -\pi \le t \le \pi
$$

```matlab
t = -pi:pi/100:pi;
x = t.*cos(3*t);
y = t.*sin(t).^2;
plot(x, y);
```

<img src=".\MATLAB.imgs\image-20210322161309782.png" alt="image-20210322161309782" style="zoom: 50%;" />

调制波形的绘制

调制波形：低频信号 \* 高频信号 的过过程 

```matlab
t = (0:pi/100:pi)';
y1 = sin(t) * [1, -1];
y2 = sin(t) .* sin(9*t);
t3 = pi*(0:9)/9;
y3 = sin(t3) .* sin(9*t3);
plot(t, y1, 'r:', t, y2, 'b', t3, y3, 'bo');
axis([0, pi, -1, 1]);
```

<img src=".\MATLAB.imgs\image-20210322161928024.png" alt="image-20210322161928024" style="zoom: 50%;" />



#### 多次叠绘

多次调用plot命令在一幅图上绘制多条曲线；需要hold指令的配合。

- hold on 保持当前坐标轴和图形，并可以接受下一次绘制。

- hold off 取消当前坐标轴和图形保持，这种状态下，调用plot绘制完全新的图形，不保留以前的坐标格式、曲线。

**绘制离散的波形**

```matlab
t = 2 * pi * (0 : 20) / 20;
y = cos(t) .* exp(-0.4*t);
stem(t, y, 'g');
hold on;
stairs(t, y, 'r');
hold off;
```



<img src=".\MATLAB.imgs\image-20210322163505937.png" alt="image-20210322163505937" style="zoom: 50%;" />



#### 双纵坐标 plotyy(x1. y1, x2, y2)

x1,y1在左，x2,y2在右边

```matlab
x = 0:0.01:20;
y1 = 200*exp(-0.05*x).*sin(x);
y2 = 0.8*exp(-0.5*x).*sin(10*x);
plotyy(x, y1, x, y2);
```

<img src=".\MATLAB.imgs\image-20210322164456442.png" alt="image-20210322164456442" style="zoom:50%;" />



#### 多子图

subplot(,m, n, k)

- 图形窗口包含（mxn）个子图，k为要指定的当前子图的编号。

- 其编号原则：左上方为第1子图，然后向右向下依次排序。该指令按缺省值分割子图区域。

- 使（mxn）幅子图中第k个子图成为当前图

subplot('postion'，[left，bottom，width，height])

- 在指定的位置上开辟子圈，并成为当前图

subplot（“postion'，[left，bottom，width，height]）用于手工指定子图位置.

- 指定位置的四元组采用归一化的标称单位，即认为整个圈形窗口绘图区域的高、宽的取值范围都是[0，1]，而左下角为（0，0）坐标。

- 产生的子图彼此独立。

- 所有的绘图指令均可以在子图中使用。



举例：

```matlab
t = (pi*(0:1000)/1000)';
y1 = sin(t);
y2 = sin(10*t);
y12 = sin(t).*sin(10*t);
subplot(2,2,1),plot(t,y1);axis([0,pi,-1,1]);
subplot(2,2,2),plot(t,y2);axis([0,pi,-1,1]);
subplot('position',[0.2,0.05,0.6,0.45]);
plot(t,y12,'b-',t,[y1,-y1],'r:');
```

<img src=".\MATLAB.imgs\image-20210322165902728.png" alt="image-20210322165902728" style="zoom:50%;" />





### 绘制图形的辅助操作

#### **曲线形状控制**

| 符号     | -    | ：   | -.     | --     |
| -------- | ---- | ---- | ------ | ------ |
| **含义** | 实线 | 虚线 | 电话线 | 双划线 |

#### **颜色控制**

b: 蓝

r：红

g：绿

c：青

m：品红

y：黄

k：黑

w：白

#### **数据点的控制**

| 符号 | .        | +      | \*       | <      | >      |
| ---- | -------- | ------ | -------- | ------ | ------ |
| 含义 | 实心黑点 | 十字符 | 八线符   | 左三角 | 右三角 |
|      | ^        | v      | d        | h      | o      |
|      | 上三角   | 下三角 | 菱形符号 | 六角形 | 空心圆 |
|      | p        | s      | x        |        |        |
|      | 五角星   | 方块符 | 叉字符   |        |        |

#### **刻度**

- grid on 开启
- grid off 关闭

#### **坐标**

**坐标框**

- box on 开启
- box off 关闭

**坐标轴**

xlabel、ylabel

图中的坐标的表示形式

- 所有的希腊字符都可以转义

#### **刻度设置**

set(gca, 'xtick', xs, 'ytick', ys)

- xs、ys是任何合法的师叔向量，用来设定x、y轴的刻度

```matlab
t = 6 * pi * (0:100)/100;
y = 1 - exp(-0.3*t).*cos(0.7*t);
tt = t(abs(y - 1)>0.05);
ts = max(tt);
plot(t,y,'r-');
grid on;
axis([0, 6*pi, 0.6, max(y)]);
title('y=1-exp(-\alpha*t*cos(\omega*t))');
hold on;
plot(ts, 0.95, 'bo');
hold off;
set(gca, 'xtick', [2*pi, 4*pi, 6*pi], 'ytick', [0.95, 1, 1.05, max(y)]);
grid on;
```

<img src=".\MATLAB.imgs\image-20210322171403108.png" alt="image-20210322171403108" style="zoom:50%;" />

（图中的点为ts）

### 特殊二维图形

#### 直方图

| 图形         | 指令                                                    |
| ------------ | ------------------------------------------------------- |
| 柱状图       | bar(x, y, args[])                                       |
| 累计式直方图 | bar(x, y, 'stack', args[])                              |
| 分组式直方图 | bar(x, y, 'group', args[])、barh(x, y, 'group', args[]) |



#### 饼图

pie(x, y, args[])



#### 离散杆图

stem(x, y, args[])



#### 极坐标图

$$
\rho = sin(2\theta)cos(2\theta) \\
polar(\theta, \rho, args[])
$$

polar(theta, tho, args[])



### 三维图形

#### 三维线图

plot3(x, y, z, args[])



#### 三维网线图、曲面图

步骤：

1. 确定取值范围和取值间隔
2. 构建格点矩阵
3. 计算格点上的函数值

```matlab
 x = -4: 0.01; 4;
 y = x;
 [x, y] = meshgrid(x, y);
 z = x.^2 + y.^2;
 subplot(1,2,1), mesh(x,y,z);  %三维网格图
subplot(1,2,2), surf(x,y,z);    %三维曲面图
colormap(cool); 
```

<img src=".\MATLAB.imgs\image-20210324201735451.png" alt="image-20210324201735451" style="zoom:80%;" />





### 图像处理

| 指令                   | 作用         |
| ---------------------- | ------------ |
| imread(filePath)       | 读取图像文件 |
| imshow(var)            | 显示图像     |
| imwrite(var, filePath) | 保存图像     |



## Matlab 程序设计

命令文件没有输入参数，也不返回输出参数；函数文件可以带输入参数，也可以返回输出参数。

命令文件对工作空间中的变量进行操作，文件中所有命令的执行结果也返回工作空间中；函数文件中定义的变量为局部变量，当函数文件执行完毕时，这些变量也被清除。

命令文件可以直接运行；函数文件不能直接运行，要以函数调用的方式来调用它。

**输入数据**

`A = input(提示信息, 选项)`

**输出数据**

`disp(a)`

**程序暂停**

`pause(暂停的秒数)`

`Ctrl + C 强行停止`



### 函数、选择、循环

函数单独写在一个文件中

```matlab
格式：
	for 循环变量=表达式1：表达式2：表达式3
		循环体
	end

【注】：表达式1：循环变量初值，表达式2：步长，为1时，可省略；表达式3：循环变量终值。

或：
     for循环变量 = 矩阵表达式
               循环体
     end

【注】：执行过程是依次将矩阵的各列元素赋给循环变量，
             然后执行循环体语句，直至各列元素处理完毕。
```



```matlab
while语句：
格式：
     while（条件）
           循环体
     end
```



```matlab
if 表达式
		程序模块1
     elseif
		程序模块2
     else
     	程序模块2
     end
```



```matlab
switch语句：

格式：
     switch 表达式
     case 数值1
       程序模块1
     case 数值2
       程序模块2
     case {数值3,4,5}
       程序模块3
     otherwise
       程序模块 n
     end
```



### 函数

基本结构

```matlab
function 输出形参表 = 函数名（输入形参表）
	注释
	函数体
```

- 输出形参多于一个应该用方括号括起来

1.关于函数文件名

函数文件名通常由函数名再加上扩展名.m组成。

当函数文件名与函数名不同时，Matlab将忽略函数名而确认文件名因此调用时使用函数文件名。

2.关于注释说明部分

注释说明包括3部分：

①紧随引导行之后以%开头的第一注释行。这一行一般包括**大写的函数文件名**和**函数功能简要描述**，供lookfor关键词查询和help在线帮助时使用。

②第一注释行及之后连续的注释行。通常包括函数输入/输出参数的含义及调用格式说明等信息，构成全部在线帮助文本。

③与在线帮助文本相隔一空行的注释行。包括函数文件编写和修改的信息，如作者和版本等。

3、关子return语句

如果在函数文件中插入了return语句，则执行到该语句就结束函教的执行，流程转至调用该函数的位置。通常也不使用return语句。



全局变量与局部变量

Matlab中，函数文件中的变量是局部变量。了如在若干函数中，都把某一变量定义为全局变量，那么这些函数将共用这个变量。

全局变量的作用域是整个Matlab的工作空间，所有函数都可以对它进行存取和修改。

全局变量用global命令定义，格式为：global变量名



### 例题

**例题1**

建立文件函数交换两个参数的值，返回执行后的结果

```matlab
%f_exchange.m
function [a,b] = exch(a,b)
c = a; a = b; b = c;

%命令行
x = 23;
y = [3, 4, 5];
[p, q] = f_exchange(x, y);
```

<img src=".\MATLAB.imgs\image-20210330110315924.png" alt="image-20210330110315924" style="zoom:67%;" />

**例题2**
$$
求方程 ax^2+bx+c=0的根
$$
程序如下

```matlab
a = input('a = ');
b = input('b = ');
c = input('c = ');
d = b*b - 4*a*c;
x = [(-b+sqrt(d))/(2*a),(-b-sqrt(d))/(2*a)];
disp(['x1 = ', num2str(x(1)), ' x2 = ', num2str(x(2))]);
```

运行截图为：

<img src=".\MATLAB.imgs\image-20210330102725081.png" alt="image-20210330102725081" style="zoom:67%;" />

**例题3**
$$
计算分段函数 
\begin{cases} 
	cos(x+1)+\sqrt{x^2 + 1},x=10\\
	x\sqrt{x+\sqrt{x}},x \ne 10
\end{cases}
$$
代码如下：

```matlab
x = input('请输入x的值：');
if x == 10
    y = cos(x+1)+sqrt(x*x+1);
else
    y = x*sqrt(x + sqrt(x));
end
disp(y);
```

运行截图如下：

<img src=".\MATLAB.imgs\image-20210330103408934.png" alt="image-20210330103408934" style="zoom:67%;" />

**例题4**

输入一个字符，若为大写字母，则输出其对应的小写字母；若为小写字母，则输出其对应的大写字母；若为数字字符则输出其对应的数值，若为其他字符则原样输出

代码如下：

```matlab
c = input('请输入一个字符', 's');
if c >='A' && c<='Z'
    disp(char(abs(c) + abs('a')-abs('A')));
elseif c>='a' && c<='z'
    disp(char(abs(c)- abs('a') + abs('A')));
elseif c>='0' && c<='9'
    disp(abs(c)-abs('0'));
else
    disp(c);
end
```

<img src=".\MATLAB.imgs\image-20210330103718784.png" alt="image-20210330103718784" style="zoom:67%;" />

**例题5**

某商场对顾客所购买的商品实行打折销售，标准如下：

price<200         没有折扣

200<=price<500    3%折扣

500<=price<1000   5%折扣

1000<=price<2500  8%折扣

2500<=price<5000  10%折扣

5000<=price       14%折扣

输入所售商品的价格，求其实际销售价格。

代码如下：

```matlab
price = input('请输入商品价格');
switch fix(price/100)
    case{0,1} 
        rate = 0;
    case{2,3,4}
        rate = 3/100; 
    case num2cell(5:9)
        rate = 5/100; 
     case num2cell(10:24)
        rate = 8/100;
     case num2cell(25:49)
        rate = 10/100; 
      otherwise
         rate = 14/100;
end
price = price*(1-rate) 
```

<img src=".\MATLAB.imgs\image-20210330104519216.png" alt="image-20210330104519216" style="zoom:67%;" />

**例题6**

矩阵乘法运算要求两矩阵的维数相容，否则会出错。先求两矩阵的乘积，若出错则自动转去求两矩阵的点乘。

```matlab
A = [1,2,3;4,5,6];
B = [7,8,9;10,11,12];
try 
    C = A*B;
catch
    C = A.*B;
end
C
lasterr
```

<img src=".\MATLAB.imgs\image-20210330104654187.png" alt="image-20210330104654187" style="zoom:67%;" />

**例题7**
$$
已知 y=\frac{1}{1^2} + \frac{1}{2^2} + \frac{1}{3^2} +...\frac{1}{n^2} , 当n=100时，求y的值。
$$

```matlab
y = 0;n = 100;
for i=1:n
    y = y+1/i^2;
end
y
```

<img src=".\MATLAB.imgs\image-20210330105535098.png" alt="image-20210330105535098" style="zoom:67%;" />

**例题8**

从键盘输入若干个数，当输入0时结束输入，求这些数的平均值和它们的和。

```matlab
sum = 0;
n = 0;
x = input('Enter a number(end in 0):');
while(x~=0)
    sum = sum+x;
    n = n+1;
    x = input('Enter a number(end in 0):');
end
if(n>0)
    sum
    mean=sum/n
end
```

结果截图：

<img src=".\MATLAB.imgs\image-20210330105856563.png" alt="image-20210330105856563" style="zoom:50%;" />

**例题9**

求[100,200]之间第一个能被21整除的整数。

```matlab
for n = 100:200
    if rem(n,21)~=0;
       continue
    end
    break
end
n
```

<img src=".\MATLAB.imgs\image-20210330110004611.png" alt="image-20210330110004611" style="zoom:80%;" />



**例题10**

求半径为r的圆的面积和周长

```matlab
% getCircleInfo.m

function [s, p] = getCircleInfo(r)
% getCircleInfo calculate the area and perimeter of a circle of radir
% r 半径
% s 面积
% p 周长
s = pi * r * r;
p = 2 * pi * r;
```

<img src=".\MATLAB.imgs\image-20210405160624369.png" alt="image-20210405160624369" style="zoom:67%;" />

**例题11**

利用函数文件实现直角坐标和极坐标之间的转换

```matlab
% tranDicarerPolar.m
function [tho, theta] = tranDicarerPolar(x, y)
tho = sqrt(x * x + y * y);
theta = atan(y / x);

% test.m
x = input('input x : ');
y = input('input y : ');
[rho, the] = tranDicarerPolar(x, y);
rho
the
```



**例题12**

算n！

```matlab
function f = myFactor(n)
% 计算 n 的阶乘
if n <= 1
    f = 1;
else
    f = myFactor(n - 1) * n;
end
```



**例题13**

```matlab
% 参数的数量可以改变
function out = charAry(a, b, c)
if nargin == 1
    out = a;
end
if nargin == 2
    out = a + b;
end
if nargin == 3
    out = (a * b * c) / 2;
end
```



**例题14**

全局变量的使用

```matlab
function f = weightAdd(x, y)
global ALPHA BETA
f = ALPHA*x + BETA * y
```



## MATLAB数值计算

### 多项式

表达：

- 由行向量表示

  - 元素是多项式的系数

  - 按照降幂次序排列

  - $$
    x^4-12x^3+25x+116 \\
    $$

    `p = [1 -12 0 25 116]` （没有的用0表示）

- 多项式是行向量，根是列向量

**求解多项式的根 `roots()`** 

  ```matlab
  p = [1 -12 0 25 116];
  roots(p)
  ```

  <img src=".\MATLAB.imgs\image-20210412160318955.png" alt="image-20210412160318955" style="zoom:67%;" />



**已知根，求解多项式 ：`poly()`**

```matlab
p = [1 -12 0 25 116];
r = roots(p);
poly(r)
```

<img src=".\MATLAB.imgs\image-20210412160553945.png" alt="image-20210412160553945" style="zoom:67%;" />

**多项式乘法`conv()`**

```matlab
a =[ 1 2 3 4 ];
b = [1 4 9 16];
c = conv(a, b);
c
```



<img src=".\MATLAB.imgs\image-20210412160841520.png" alt="image-20210412160841520" style="zoom:50%;" />

**多项式加法：`直接加，不够的补上 0 `**

```matlab
a =[ 1 2 3 4 ];
b = [1 4 9 16];
c = [1 2 3 4 5]
d = a + b;
e = d + [0 0 0 0]
```

<img src=".\MATLAB.imgs\image-20210412161044941.png" alt="image-20210412161044941" style="zoom:50%;" />

**实现任意长度多项式相加函数：**

```matlab
function rst =  poly_add(a, b)
% 任意长度多项式相加
if length(a) == length(b)
    rst = a + b;
elseif length(a) > length(b)
    rst = a + [zeros(1, length(a) - length(b)), b]; % zeros 产生1行多少列的0矩阵
else   
    rst = b + [zeros(1, length(b) - length(a)), a];
end
```



<img src=".\MATLAB.imgs\image-20210412161739535.png" alt="image-20210412161739535" style="zoom:50%;" />



**多项式除法` deconv() `**

```matlab
c = [0 6 20 50 75 84 64];
b = [1 4 9 16];
[q, r] = deconv(c, b);
% q 商
% r 余数
```

<img src=".\MATLAB.imgs\image-20210412162053853.png" alt="image-20210412162053853" style="zoom: 67%;" />

**多项式的导数 `polyder()`**

```matlab
b = [1 4 9 16];
d = polyder(b)
```

<img src=".\MATLAB.imgs\image-20210412162643883.png" alt="image-20210412162643883" style="zoom:50%;" />

**多项式的估值`polyval()`**
$$
绘制 p(x)=x^3+4x^2-7x-10在[-1, 3]上的曲线
$$

```matlab
x =  linspace(-1, 3); % x轴上的点
p = [1 4 -7 -10];
v = polyval(p, x); % x轴上的点对应的y值
plot(x, v) % 两个行向量
title('x^{3}+4x^{2}-7x-10');
xlabel('x');
```



<img src="R:\GITHUB\MyNotes\_Typora\Matlab\MATLAB.imgs\image-20210412163046190.png" alt="image-20210412163046190" style="zoom:50%;" />



### 函数的数值导数

matlab中没有直接求导的函数，只有计算向前差分的函数`diff()`

`DX=diff(x) % 计算向量X的向前差分`

`DX=diff(X, n) %X的n阶向前差分`



设x由[0, 2pi]间均匀分布的10个点组成，求sin(x)的1-3阶差分

一阶差分：`f(x+1)-f(x)`

2阶差分：`f(x+2)-f(x)`

n阶差分：`f(x+n)-f(x)`

```matlab
x = linspace(0, 2*pi, 10);
y = sin(x);
dy = diff(y)
d2y = diff(y, 2)
d3y = diff(y, 3)
```

<img src="R:\GITHUB\MyNotes\_Typora\Matlab\MATLAB.imgs\image-20210412165007007.png" alt="image-20210412165007007" style="zoom:50%;" />


$$
设f(x) = \sqrt{x^2+2x^2-x+12} + （x + 5）^{1/6} + 5x + 2 在[-3,3]内以0.01为步长求数值导数，并画图
$$

```matlab
f = inline('sqrt(x.^3+2*x.^2-x+12)+(x+6).^(1/6)+5*x+2'); % 内联函数
x = -3:0.01:3;
dx = diff(f([x, 3.01]))/0.01; % 根据定义求导数
% 求一阶差分之后少了一个点，所以应该补上一个3.01
% 这样计算之后x和dx 的长度是相等的
plot(x, dx)
```

<img src="R:\GITHUB\MyNotes\_Typora\Matlab\MATLAB.imgs\image-20210412165740650.png" alt="image-20210412165740650" style="zoom:67%;" />

### 数值定积分

一元函数的数值积分

常用积分指令 `quad`、`quadl`

调用格式：

```matlab
q = quadl(fun, a, b); % 被积函数， 上限， 下限
% 被基函数应该是用引号引起来的字符形式的函数
% 缺省参数 tol ： 控制绝对误差
% 缺省参数 
```


$$
求定积分 I=\begin{equation*}
\int_{0}^{1} xe^{-x}dx
\end{equation*}
$$


```matlab
fun = inline('exp(-x.*x)', 'x'); % 第二个参数x表示这个函数的变量为x
Isim = quad(fun, 0, 1), I8 = quadl(fun, 0, 1)
```

<img src="R:\GITHUB\MyNotes\_Typora\Matlab\MATLAB.imgs\image-20210412171051058.png" alt="image-20210412171051058" style="zoom:50%;" />


$$
\begin{equation*}
\int_{0}^{1} \sqrt{ln(\frac{1}{x})}\, dz
\end{equation*}
$$

```matlab
fun = inline('sqrt(log(1./x))', 'x');
Isim = quad(fun, 0, 1)
```

<img src="R:\GITHUB\MyNotes\_Typora\Matlab\MATLAB.imgs\image-20210412170900672.png" alt="image-20210412170900672" style="zoom:50%;" />



### 元素排序

`sort(X)` 返回一个对X中元素按照**每列升序**排列的新向量

也可以对矩阵A的各行或者各列重新排序：`[Y, I] = sort(A, dim)` **dim=1按列排序，=2，按行排序**，Y是排序后的矩阵，I记录Y中的元素在A中的位置。

```matlab
A = [1 -8 5; 4 12 6; 13 7 -13];
sort(A) % 每列升序排列的新向量
-sort(-A,2) % 每行降序排列 ，即：按行排列，升序排列A的相反数，排列之后再取相反数
```

<img src="R:\GITHUB\MyNotes\_Typora\Matlab\MATLAB.imgs\image-20210412172032704.png" alt="image-20210412172032704" style="zoom: 67%;" />

### 数据插值

一维数据插值：被插的函数只有一个单变量

一维数据插值`Y1 = interp1(X, Y, X1, method)` 函数根据X，Y的值计算函数在X1处的值。

XY是两个等长的已知向量，分别描述采样点和样本值。

X1是一个向量或标量，描述想要插值的点，Y1是一个与X1等长的插值结果。

method取值：

- linear  (默认)
- nearest
- cubic
- spline

​	表示四种插值方式

一般来说，3次样条和3次多项式的插值结果比线性插值和最近点插值方法好，但是插值方法的**好坏依赖于被插值的函数**



例：给出概率积分数据如下，用不同的插值方法计算f(0.472)

```matlab
x = 0.46:0.01:0.49
f = [0.4846555 0.4937542 0.5027498 0.5116683];
format long 
interp1(x, f, 0.472)  % 默认
interp1(x, f, 0.472, 'neraest') % 最近插值法
```

<img src="R:\GITHUB\MyNotes\_Typora\Matlab\MATLAB.imgs\image-20210419155643963.png" alt="image-20210419155643963" style="zoom:50%;" />



### 曲线拟合

用 `ployfit` 求最小二乘拟合多项式的系数，再用`polyval`函数按照所得的多项式计算所给出点上的函数的近似值。

```matlab
[P, S] = polyfit(X, Y, m)
% X 采样点
% Y 采样点的函数值
% m 产生m次的多项式
% P 多项式的系数
% S 误差向量
```



例题：

用一个三次多项式在区间0到2pi内逼近函数sinx

```matlab
x = linspace(0, 2*pi, 20); % 
y = sin(x);
p = polyfit(x, y, 3);
y1 = polyval(p, x);
plot(x, y, ':o', x, y1, '-*');
legend('sin(x)', 'fit');
```

<img src="R:\GITHUB\MyNotes\_Typora\Matlab\MATLAB.imgs\image-20210419160450112.png" alt="image-20210419160450112" style="zoom:67%;" />





## MATLAB符号运算

### 符号运算基础

符号对象的定义

- 定义符号对象的指令： `sym` \ `syms`
- `f = sym(arg)`  或者  `f = syms('arg1', 'arg2', ...)` 或者 `syms arg1, arg2...`
  - 将数字、字符串或者表达式arg转换为符号对象f
- 符号表达式可以进行四则运算

```matlab
syms x  y a b;
f1 = sin(x) + cos(y)
f2 = a - b;
f12 = f1 + f2;
f12
f3 = f1 * f2;
```

基本符号运算和操作

`collect(s)` `collect(s, v)`

s 是将要进行合并的函数

v 是以什么为基准合并，字符串

```matlab
clear
syms x y;
f = x^2*y + y*x-x^2-2*x;
collect(f);
collect(f, 'y');
```

<img src="R:\GITHUB\MyNotes\_Typora\Matlab\MATLAB.imgs\image-20210419162140048.png" alt="image-20210419162140048" style="zoom:50%;" />

因式分解

```matlab
clear
syms x y
factor(x^5-y^5)
factor(x^10-y^10)
```

<img src="R:\GITHUB\MyNotes\_Typora\Matlab\MATLAB.imgs\image-20210419162307004.png" alt="image-20210419162307004" style="zoom:50%;" />

化简 `simplify`  `simple`

展开 `expand`

嵌套形式 `horner`

找到分子和分母 `numden`



### 符号矩阵的创建与运算

使用sym创建符号数组

```matlab
a1 = sym('[1/3 1/2 sqrt(2)]')
or 
b1 = '[1/3 1/2 sqrt(2)]'
a2 = sym(b1);
a1
a2
// 没跑出来
```





创建符号常数数组

```matlab
a = reshape(1:9, 3, 3)
s_a = sym(a)
s_b = 1./ s_a
whos a s_a s_b

```

<img src="R:\GITHUB\MyNotes\_Typora\Matlab\MATLAB.imgs\image-20210419164349946.png" alt="image-20210419164349946" style="zoom: 50%;" />

创建一般符号数组

符号矩阵可以乘以普通标量、符号标量、点乘等



### 符号微积分

符号极限指令: 

- `limit(f, x, a)` 计算变量x->a的时候，函数f的极限值
- `limit(f, a)` 计算有findsym(f)确定的自变量->a的时候，函数f的极限值
- `limit(f)` 计算a = 0的时候函数f 的极限值
- `limit(f, x, 'right')` `limit(f, x, 'left')` 计算x->a时的右极限、左极限

```matlab
syms x t y h
f = sin(x)/x;
limit(f)
limit((1+2*t/x)^(3*x), x, inf)
limit(1/x, x, 0, 'right') % 右极限
limit(1/x, x, 0, 'left') % 左极限
limit((sin(x+h)-sin(x))/h, h, 0) % sin(x)的导数的概念
```

<img src="R:\GITHUB\MyNotes\_Typora\Matlab\MATLAB.imgs\image-20210419165716570.png" alt="image-20210419165716570" style="zoom:50%;" />



### 函数的符号微分与求导

MATLAB符号微分指令： `diff`

```matlab
syms x y;
f = x^2 + x*y + sin(x) + cos(y);
dy1 = diff(f, 'y') % 默认对x求导，用’y‘作为参数可以对y求导
dx2 = diff(f, 2) % 求2阶导数
dy2 = diff(f, 'y', 2) % 求 y 的二阶导数
```

<img src="R:\GITHUB\MyNotes\_Typora\Matlab\MATLAB.imgs\image-20210419170704038.png" alt="image-20210419170704038" style="zoom:50%;" />

### 符号积分

`int` 计算不定积分和定积分

```matlab
syms x w t;
int(1/x)
int(1/x^2)
int(sin(w*t), t) % 对 t 积分

```

<img src="R:\GITHUB\MyNotes\_Typora\Matlab\MATLAB.imgs\image-20210419171018559.png" alt="image-20210419171018559" style="zoom: 50%;" />

### 符号代数方程的求解

代数方程求解代数方程的指令：

- 线性方程组的求解：`linsolve`
- 一般代数方程组的解：`solve`

$$
求方程组 u*y^2+v*z+w=0,y+z+w=0 关于y，z的解
$$







## MATLAB应用举例



**求解方程的根**
$$
2x^5-3x^3+71x^2-9x+13=0
$$

```matlab
% 建立多项式系数行向量
% 每一个系数
p = [2, 0, -3, 71, -9, 13];
x = roots(p); % 求根
```





**求解线性方程组**
$$
\begin{cases} 
2x+3y-z=2 \\8x+2y+3z=4 \\45x+3y+9z=23
\end{cases}
$$

```matlab
a = [2, 3, -1; 8, 2, 3; 45, 3, 9]; % 建立系数矩阵a
b = [2; 4; 23]; % 建立列向量b
z = inv(a) * b;
```



---


$$
原方程组可化为
\begin{cases} 
2x+3y-z-2=0 \\8x+2y+3z-4=0 \\45x+3y+9z-23=0
\end{cases}
$$

```matlab
syms x y z; % 声明变量
[x, y ,z] = solve(2*x+3*y-z-z, 8*x+2*y+3*z-4, 45*x+3*y+9*z-23); % 求解变量
```



**求解定积分**
$$
\int_{0}^{1}{x\ln(1+x)}dx
$$

```matlab
quad('x.*log(1+x)', 0, 1);
```



**多项式曲线拟合**



```matlab
% 考虑以下实验数据
x = [1:1:10];
y = [1.2, 3, 4, 4, 5, 4.7, 5, 5.2, 6, 7.2];

% 一次多项式拟合
p1 = polyfit(x, y, 1);

% 三次多项式拟合
p3 = polyfit(x, y, 3);

% 画出原始数据和拟合曲线
x2 = 1:0.1:10;
y1 = polyval(p1, x2);
y3 = polyval(p3, x2);

% 3个一组，两个变量和变量的显示形式。
plot(x, y, '*', x2, y1, ':', x2, y3);
```



<img src=".\MATLAB.imgs\image-20210308162050858.png" alt="image-20210308162050858" style="zoom:75%;" />