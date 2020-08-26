### 剑指offer 14-I 剪绳子

给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m - 1] 。请问 $k[0]*k[1]*...*k[m - 1] $可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。



#### 数学推导

$n=n_1+n_2+n_3+....+n_a$

$obj: max(n_1*n_2*....*n_a)$

##### 算数几何均值不等式

$\frac{n_1+n_2+n_3+....+n_a}{a}>=\sqrt{n_1*n_2*....*n_a}$ 

当且仅当$n_1 = n_2 = n_3 =....=n_a$等式成立

$obj = x^a=x^{\frac{n}{x}}=(x^{\frac{1}{x}})^n$

$y = x ^{\frac{1}{x}}$对两边求导

得到x = e得到极值

x=2或者x=3;

$2^{\frac{1}{2}} < 3^{\frac{1}{3}}$

因此x=3是最好的

用n对3取余

取余为0，直接出结果

取余为1，则拆掉一个3，和1组成2+2；

取余为2，直接出结果

```java
class Solution(){
    public int cuttingRope(int n){
        if(n < 3){
            return n-1;
        }
        int a = n / 3;
        int b = n % 3;
        if(b == 0){
            return (int)Math.pow(3, a);
        }
        if(b == 1){
            return (int)Math.pow(3, a-1) * 4;
        }
        if(b == 2){
            return (int)Math.pow(3, a) * 2;
        }
        return 0;
    }
}
```

