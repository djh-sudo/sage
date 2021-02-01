## 求逆元
* ### inverse_mod
```
inv = inverse_mod(30,197)
inv = 46
```
## 扩展欧几里得
* ### xgcd
```
a = xgcd(30,197)
a = (1, 46, -7)
```
这里第一个数就是最大公约数，后面两个其实就是扩展欧几里得的系数
如果只要求最大公约，可以用gcd
## CRT中国剩余定理
* ### def CRT
```
 def CRT(modulus, remainders):
     Sum = 0
     prod = reduce(lambda a, b: a*b, modulus)
     for m_i, r_i in zip(modulus, remainders):
         p = prod // m_i
         Sum += r_i * (inverse_mod(p,m_i)*p)
     return Sum % prod
 CRT([3,5,7],[2,3,2]) #23
```
这里求解的其实是同余方程组
```
x ≡ r mod m
```
当然，这里```r```和```m```是长度相同的向量，要求```gcd(m) = 1```方程组一定有解，其余情况需要化简后判断是否有解
## 离散对数
* ### discrete_log
```
x = discrete_log(mod(13,23),mod(2,23))
x = 7
```
这里求的是```y ≡ g^(x) mod m```,即```13 ≡ 2^(x) mod m```
即离散对数问题，离散对数问题难解性,已知`x`求`y`是容易的，反之已知`y`求`x`是困难的。
## 取模求根
* ### nth_root
```
x^(22) ≡ 5 mod 41
```
求出`x`,在RSA中尤其是`e`比较小时，可以用这个方法爆破私钥`d`。
```
x = mod(5,41)
r = x.nth_root(22)
r = 6
```
## 欧拉函数
* ### euler_phi
```
x = euler_phi(71)
x = 70
```
## 近似表达式输出
* ### numerical_approx()
```
result=pi^2
result.numerical_approx()
9.86960440108936
```
## 椭圆曲线
* ### def
```
y^(2) ≡ x^(3) + ax + b
```
* 1.sage可以生成和绘制相关的椭圆曲线
```
a = -5; b = 4
E1 = EllipticCurve(RR, [a, b])
show(plot(E1, hue=.9))
```
此时会生成一张椭圆曲线的图片
* 2.生成一个有限域GF上的椭圆曲线，一般会选择一个素数
```
p = 137
F =GF(p)
E = EllipticCurve(F, [F.random_element(), F.random_element()])
show(plot(E,hue=.9))
E.points() #输出点数
```
