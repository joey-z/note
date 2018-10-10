**1.学习编程的本质:** 
**程序=算法+数据结构 程序设计=内容(程序)+编程范式**
编程范式 设计模式 
常见编程范式 面向过程 面向对象 函数式编程 伴随式编程(?)
c语言支持面向过程编程范式 c++少有的支持四种编程范式的语言
学一门语言 先找编程范式 再找语法特性 学会子集就可以开始编程了
2.输出函数说明
**printf函数** 
头文件 stdio.h 
                  常量字符串  ...声明函数的一种形式(代表后面是任意多的参数) (如何实现变参函数的时候会讲)       
原型: int  printf(const char *format, ...);
format: 格式控制字符串 
...: 可变参数列表
printf函数的输代表向输出流中输出了多少字符 
printf默认向标准输出中输出 
标准输入 0 标准输出 1 标准错误输出 2
返回值: 输出字符的数量

**scanf函数**
头文件 stdio.h
返回值: 成功读入的参数个数
3.函数完成的是一种映射  数组完成的是从数组下标到值的映射
数组是展开的函数  函数是压缩的数组
   记录式             计算式  
算法优化 记录式改计算式 节省大量存储空间 
4.深度神经网络 以任意精度 去逼近任意函数 
计算式的结构 数组映射的值规律很复杂的时候 用神经网络拟合函数  最后的到的结构就是函数结构
第五个编程范式  可微分编程

**代码演示**

```c
#include <stdio.h>

int main() {
    int n;
    while(scanf("%d", &n) != EOF) {
        printf(" has %d digits\n", printf("%d", n));
    }
    
    return 0;
}
```

```c
#include <stdio.h>

int main() {
    int n;
    char str[100];
    while(scanf("%d", &n) != EOF) {  //输入12 789
        printf("%d\n", sprintf(str, "%d", n));
        printf("str = %s", str); 
        //输出结果为 
        //2  3
        //str = 12   str = 789
    }
    return 0;
}//sprintf不仅把待输出的内容输出到字符数组中 而且在输出结束后在字符数组中的最后一位会添加一个\0 
```

```c
//str连续输出1-20
#include <stdio.h>

int main() {
    int n;
    char str[100];
    while(scanf("%d", &n) != EOF) {
        printf("%d\n", sprintf(str, "%d", n));
        for (int i = 1, j = 0; i <= 20; i++) {
            j += sprintf(str + j, "%d", i);
        }
        printf("str = %s\n", str);
    }
    return 0;
}

```

```c
//fpritnf
#include <stdio.h>

int main() {
    int n;
    char str[100];
    FILE *fout = fopen("/dev/null", "w"); //需要一个文件指针 写模式打开垃圾桶文件 
    while(scanf("%d", &n) != EOF) {
        printf("%d\n", fprintf(fout, "%d", n)); //将内容向垃圾桶文件输出 最终结果就只会输出字符个数 例: 23 3  456 3
    }
    return 0;
}
```

**随堂练习**

```c
#include <stdio.h>
//读入一串字符 含有空格  输出字符数量
int main() {
    char str[100];
    scanf("%[^\0]," str); //正则表达式 读入非\0的字符(\0为字符串末尾)
    int n = printf("%s", str);
    printf(" has %d chars\n", n);
    return 0;
}
```

**牛顿迭代实现sqrt**

```c
#include <stdio.h>
#include <math.h>
#include <time.h>

#define TEST_TIME(func) ({ \
	int begin = clock(); \
	double ret = func; \
	int end = clock(); \
	printf("%lfms\n", (end - begin) * 1.0 / CLOCK_PER_SEC * 1000) \
	ret; \
})
double _sqrt1(double x) {
    double head = -100, tail = 100, mid;
    #define EPS 1e-7
    while(tail - head > EPS) {
    	mid = (head + tail) / 2.0; 
    	if (mid * mid < x) head = mid;
    	else tail = mid;
    }
    #undef EPS
    return head;
}
double f1(double x, double n) {
    return x * x - n;
}
double f1_prime(double x) {
    return 2 * x;
}

double newton(double x0, double n, double (*f)(double double ), double (*f_prime)(double)) {
    double x = x0;
    int cnt = 0;
    #defien EPS 1e-7
    x -= f(x, n) / f_prime(x);
    x -= f(x, n) / f_prime(x);
    x -= f(x, n) / f_prime(x);
    x -= f(x, n) / f_prime(x);
    cnt += 1;
    #undef EPS
    printf("netwon run %d times\n", cnt);
}

int main() {
    double x;
    while(scanf("%lf", &x) != EOF) {
        printf("%lf\n", TEST_TIME(_sqr1t(x)));
        printf("%lf\n", TEST_TIME(newrton(1.0, x, f1, f1_prime)));
        printf("%lf\n", TEST_TIME(newrton(2.0, x, f1, f1_prime)));
        printf("%lf\n", TEST_TIME(newrton(3.0, x, f1, f1_prime)));
    }
    
    return 0;
}
```

