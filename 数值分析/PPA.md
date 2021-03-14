<h1 align = "center">凸优化算例设计</h1>

姓名：葛伟     院系：材料与化工    学号：12032291



## 1. 问题描述

找出最接近的相关矩阵

![image-20201231162016823](C:\Users\flyer\OneDrive\笔记\Note\数值分析\PPA.assets\image-20201231162016823.png)



## 2. 算法方案

通过最小化问题来找出迭代后的解：

![image-20201231162204088](C:\Users\flyer\OneDrive\笔记\Note\数值分析\PPA.assets\image-20201231162204088.png)

其中，拉格朗日乘子：

![image-20201231162107849](C:\Users\flyer\OneDrive\笔记\Note\数值分析\PPA.assets\image-20201231162107849.png)

每次迭代的主要计算量在于奇异值分解，主要由$$[V,D] = eig(A)$$执行。

## 3. 数值结果

### 3.1 程序代码

#### PPA Classical：

```matlab
clear; close all;
n = 1000; %矩阵维数
tol = 1e-5; %精度
r = 2.0; s = 1.01/r; %迭代时的系数
gamma = 1.5;
rand('state',0);
C = rand(n,n); %随机生成n维矩阵
C = (C'+C)-ones(n,n)+eye(n); %生成C矩阵，且C是对称的
%function PPAC(n,C,r,s,tol)
X = eye(n); %X为n维单位矩阵
y = zeros(n,1); %生成n维0向量
tic; %启动秒表计时器
stopc = 1; %迭代精度，与停机准则比较作为判断依据
k = 0;
while (stopc>tol && k<=100)
%满足停机准则且k<=100时跳出迭代循环
    if mod(k,20)==0
        fprintf('k = %4d    epsm = %9.3e    \n',k,stopc);
        %每20次迭代，显示一次迭代结果
    end
    X0 = X; y0 = y; k = k+1;
    yt = y0-(diag(X0)-ones(n,1))/s; 
    %z（拉格朗日乘子）的迭代过程，y0:z^k; yt:z^(k+1)
    EY = y0-yt;
    %拉格朗日乘子迭代前后结果的差值
    A = (X0*r+C+diag(yt*2-y0))/(1+r);
    %求解X^(k+1)中的部分内容
    [V,D] = eig(A);
    %返回特征值的对角矩阵D和右矩阵V，其列是对应的右特征向量，使得A*V=V*D
    D = max(0,D);
    %将D中小于0的元素置0，保证其非负性
    XT = (V*D)*V';
    %X的迭代结果
    EX = X0-XT;
    %X前后迭代的差值，作为停机准则
    ex = max(max(abs(EX)));
    ey = max(abs(EY));
    stopc = max(ex,ey);
    %停机准则的选择，拉格朗日乘子以及X都需要满足精度
    X = XT; y = yt;
end
toc;
%计时停止
TB = max(abs(diag(X-eye(n))));
fprintf('k = %4d    epsm = %9.3e    max|X_jj-1|=%8.5f   \n',k,stopc,TB);
```

#### PPA Extend：

```matlab
clear; close all;
n = 1000; %矩阵维数
tol = 1e-5; %精度
r = 2.0; s = 1.01/r; %迭代时的系数
gamma = 1.5;
rand('state',0);
C = rand(n,n); %随机生成n维矩阵
C = (C'+C)-ones(n,n)+eye(n); %生成C矩阵，且C是对称的
%function PPAE(n,C,r,s,tol,gamma)
X = eye(n); %X为n维单位矩阵
y = zeros(n,1); %生成n维0向量
tic; %启动秒表计时器
stopc = 1; %迭代精度，与停机准则比较作为判断依据
k = 0;
while (stopc>tol && k<=100)
%满足停机准则且k<=100时跳出迭代循环
    if mod(k,20)==0
        fprintf('k = %4d    epsm = %9.3e    \n',k,stopc);
        %每20次迭代，显示一次迭代结果
    end
    X0 = X; y0 = y; k = k+1;
    yt = y0-(diag(X0)-ones(n,1))/s; 
    %z（拉格朗日乘子）的迭代过程，y0:z^k; yt:z^(k+1)
    EY = y0-yt;
    %拉格朗日乘子迭代前后结果的差值
    A = (X0*r+C+diag(yt*2-y0))/(1+r);
    %求解X^(k+1)中的部分内容
    [V,D] = eig(A);
    %返回特征值的对角矩阵D和右矩阵V，其列是对应的右特征向量，使得A*V=V*D
    D = max(0,D);
    %将D中小于0的元素置0，保证其非负性
    XT = (V*D)*V';
    %X的迭代结果
    EX = X0-XT;
    %X前后迭代的差值，作为停机准则
    ex = max(max(abs(EX)));
    ey = max(abs(EY));
    stopc = max(ex,ey);
    %停机准则的选择，拉格朗日乘子以及X都需要满足精度
    X = X0-EX*gamma; y = y0-EY*gamma;
    %扩展后的PPA仅仅改变了这一过程
end
toc;
%计时停止
TB = max(abs(diag(X-eye(n))));
fprintf('k = %4d    epsm = %9.3e    max|X_jj-1|=%8.5f   \n',k,stopc,TB);
```



### 3.2计算结果

#### 1. 结果图展示

![image-20201231153828681](C:\Users\flyer\OneDrive\笔记\Note\数值分析\PPA.assets\image-20201231153828681.png)

![image-20201231153916483](C:\Users\flyer\OneDrive\笔记\Note\数值分析\PPA.assets\image-20201231153916483.png)

#### 表格展示计算结果：

| n*n Matrix n= | Classical PPA k= | Extended PPA k= |
| ------------- | ---------------- | --------------- |
| 100           | 30               | 22              |
| 200           | 33               | 25              |
| 500           | 39               | 27              |
| 800           | 42               | 29              |
| 1000          | 48               | 31              |
| 2000          | 66               | 42              |

| n*n Matrix n= | Classical PPA t=（/s） | Extended PPA t=  (/s) |
| ------------- | ---------------------- | --------------------- |
| 100           | 0.236081               | 0.122978              |
| 200           | 0.677023               | 0.499786              |
| 500           | 5.925969               | 3.579605              |
| 800           | 22.588338              | 12.730078             |
| 1000          | 43.379604              | 23.158688             |
| 2000          | 378.583934             | 209.952937            |



## 4. 结论

1. 使用扩展后的PPA，与经典PPA相比，相同精度下，迭代次数与迭代时间都大大减小了，说明扩展后的PPA在相同的条件下效率更高。





