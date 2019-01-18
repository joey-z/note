## 从C到C++

- ｆ()和ｆ(void)的区别

  - c 　ｆ()可以传n个参数　ｆ(void) 不能传参
  - c++  无区别　都不能传参

- ｃ++是一种强数据类型的语言，ｃ++是ｃ的超集

- 异常和bug区别

- 编程范式　

  - 面向过程（随着问题规模的增大，难以维护，可移植性不好）
  - 面向对象（）
  - 泛型编程
  - 函数式编程

- 运算符里不能重载的只有５个

- C语言所有变量必须位于函数体的最前面，C++所有变量随用随定义

- C++中提供两种初始化方法：

  1. 复制初始化　`int x = 1024;`(C语言提供的初始化方式)
  2. 直接初始化`int x (1024);`

  

### 命名空间

- 简言之：化地方取名字

- 命名空间关键字：`namespace`

  ```c++
  namespace A {
      int x = 0;
      void f1();
      void f2();
  }
  cout << A::x <<  endl;
  A::f1();
  ```

### 引用类型

- 引用怎么用
  - 引用作为参数的时候可以不用初始化
  - 局部变量不能当引用使用

- 在计算机中，引用就是变量的别名

- 声明一个变量引用时，必须初始化（有小名必须有大名）

  ```c++
  //普通数据类型的引用
  int a = 3;
  int &b = a;
  b = 10;
  cout  << a << endl; // 10
  ```

- 结构体类型的引用（类比c语言）

  ```c++
  typedef struct {
      int x;
      int y;
  } Coor;
  
  int main() {
      Coor c1;
      Coor &c = c1;
      c.x = 10;
      c.y = 20;
      cout << c1.x <<" "<< c1.y; //10 20
      return 0;
  }
  ```

- **指针类型的引用**

  `类型　*&指针引用名 = 指针;`　

  ```c++
  int main() {
      int a = 10;
      int *p = &a;
      int *&q = p;
      *q = 20;
      cout << a << endl; //20
      return 0;
  }
  ```

- 引用作为函数参数

  ```c++
  //c语言
  void func(int *a, int *b) {
      int c = 0;
      c = *a;
      *a = *b;
      *b = c;
  }
  int main() {
  	int x = 10, y = 20;
  	func(&x, &y);
      return 0;
  }
  /****************************************/
  //C++引用
  void func(int &a, int &b) {
      int c = 0;
      c = a;
      a = b;
      b = c;
  }
  int main() {
      int x = 10, y = 20;
  	func(x, y);
      return 0;
  }
  ```

  

### 类和对象

- 类的定义

  ```c++
  //关键字 类名
  class Dog {
      //数据成员（也叫属性）
      char name[20];
      int age;
      int type;
      
      //成员函数（也叫方法）
      void speak();
      void run();
  };
  ```

  

- 类型 = 类型数据 + 类型操作

```c++
  #include <iostream>
  /*using std::cin;
  using std::cout;
  using std::end1;
  using std::string;*/
  using namespace std;//为了代码简单
  //：：
  namespace my_lib{
      class People {
          private;//私有的
          //属性
          	int age;
          	string name; //string是一个类
          	//double height;
          	//double weight;
          	//double salary;
          	//bool sex;
          public;
          //方法实现两种方式
          //构造函数
          	People(string &s) {
              name = s;
          }
          //成员函数
          int getAge() {
              return age;
          }
          string getName () {
              return name;
          }
      } ;
  }
  //using my_lib::People;
  int main() {
      People p("zoe1");
      People *p1 = new People("zoe");
      cout << p.getName() << end1;
      cout << p1->getName() << end1;
      //new跟delete是成对出现的 不然会内存泄露
      delete p1;
      return 0;
  }
```

## 访问限定符

- **public ：公共的**
- protecte ：受保护的
- **private ：私有的**

```c++
class TV {
    //希望暴露
    public:
    	char name[20];
    	int type;
    
    	void changeVol();
    	void power();
    private:
    //希望隐藏
    	电阻调节；
        像素配色；
}；
```

- 实例化对象/对象成员的访问

  ```c++
  class TV {
      public:
      	char name[20];
      	int type;
      
      	void changeVol();
      	void power();
  };
  //从栈中实例化对象/对对象成员访问
  int main() {
      TV tv;
      TV tv[20];
      //tv.type = 0;
      //tv.changeVol();
      return 0;
  }
  //从堆中实例化对象/对对象成员访问
  int main() {
      TV *p = new TV();
      TV *q = new TV[20];
      //p->type = 0;
      //p->changeVol();
      delete p; 
      p = NULL:
      return 0;
  }
  //数组 
  int main() {
      TV *p = new TV[5];
      for (int i = 0; i < 5; i++)  {
          p[i]->type = 0;
          p[i]->changeVol();
      }
      delete []p;
      p = NULL;
      return 0;
  }
  ```

- 字符操作

  ```c++
  #include <iostream>
  #include <string>
  using std::cin;
  using std::cout;
  using std::endl;
  using std::string;
  int main() {
      string s1;//空串
      string s2("ABC");
      string s3(s2);//将s3初始化为s2的一个副本
      string s4(3, 'b');//将s4初始化为字符b的3个副本
      return 0;chongzai
  }
  ```

  ![](/home/zoe/%E6%88%AA%E5%9B%BE/c++/string%E7%B1%BB%E5%9E%8B.png)

  ![](/home/zoe/%E6%88%AA%E5%9B%BE/c++/string%E5%AD%97%E7%AC%A6%E4%B8%B2%E8%BF%9E%E6%8E%A5%E6%96%B9%E5%BC%8F.png)

- ```c++
  /*题目描述：
  	1.提示用户输入姓名
  	2.接收用户的输入
  	3.然后向用户问好：hello XXX
  	4.输出用户名字的长度
  	5.输出用户名字的首字母
  	6.如果用户直接输入回车，提示用户输入为空
  	7.如果用户输入的是imooc，那么告诉用户是管理员*/
  #include <iostream>
  #include <string>
  using std::cin;
  using std::cout;
  using std::endl;
  using std::string;
  
  int main() {
      string name;
      cout << "please input you name : ";
      getline(cin, name);//cin输入流无法实现6功能，会一直等有输入
      if (name.empty()) {
          cout << "input is empty!" << endl;
          return 0;
      } else if (name == "imooc") {
          cout << "you are root user!" << endl;
      }
      cout << "hello " + name << endl;
      cout << "your name length is : " << name.size() << endl;
      cout << "the first word is : " << name[0] << endl;
      return 0; 
  }
  
  ```

- 找主函数 ->构造函数->

- 做工程先画UML图

- 类与对象

  ```c++
  #include <isotream>
  using std::cin;
  using std::cout;
  using std::endl;
  class Test {
      private:
          int i;
      	int j;
      public:
      	int a;
      	int getI() {
          	return i;
      	}
      	int getJ() {
          	return j;
      	}	
      	int getA() {
          	return a;
      	}
      	void setI(int value) {
          	i = value;
          	return ;
      	}
  };
  int main() {
      Test t;
      Test *t1 = new Test;
      t.a = 5;
      t1->a = 10;
      cout << t.getI() << endl;
      cout << t.a　<< " " << t1->a << endl; 
      return 0;
  }
  ```

  - 访问修改类里面的对象时要通过成员函数去做

## 内联函数

- 关键字：`inline`
- 例子：

```c++
inline void func() {
    cout << "Hello" << endl;
}
```

#### 内联函数与普通函数的区别：

- 普通函数：主函数调用func()函数要先找到func()函数的入口，然后运行里面相关的代码，运行结束后返回到主调函数，然后再运行主调函数的其他代码。

- 内联函数：编译时将函数体代码和实参代替函数调用语句。省去了调用的部分和返回的部分。效率更高，速度更快。

- 注意：内联函数必须是结构和逻辑都比较简单的代码

- 类内定义的成员函数，编译器会将其优先编译为内联函数，不会将inline写出来，但是会以inline的方式进行优先编译，复杂的函数无法编译成内联函数，就编译成普通的函数。

- 同文件类外定义：

  ```c++
  class Car {
      public:
      	void run();
      	void stop();
      	void changeSpeed();
  };
  void Car::run() {}
  void Car::stop() {}
  void Car::changeSpeed() {}
  ```

- 分文件类外定义（多数用）

  ```c++
  //car.h
  class Car {
       public:
      	void run();
      	void stop();
      	void changeSpeed();
  };
  ```

  ```c++
  //car.cpp
  #include "car.h"
  void Car::run() {}
  void Car::stop() {}
  void Car::changeSpeed() {}
  ```

  #### 对象初始化

  - 有且仅有一次
  - 根据条件进行初始化

## 数据类型的加强

1. 在c语言中有没有真正的常量
   - 枚举类型才是真正的常量
   - **const叫只读变量**
2. 怎么改变const的值

```c++
#include <stdio.h>

int main() {
    const int a = 5;
    //a = 6; 会提示不能修改
    //const是个只读变量 用指针就可以修改
    int *p = (int *)&a;
    *p = 6;
    printf("%d, %d \n", a, *p);
    return 0;
}
//gcc编译结果是6, 6
//g++编译结果是5, 6
//const 在c++中 例如const int a = 5;
/*c++*/
#include<iostream>
#include<cstdio>
int main() {
    const int a = 5;
    int *p = (int *)&a;
    *p = 6;
    printf("%d, %d\n", a, *p);
    return 0;
}
//
```

**c++**中**const**修饰的变量就是真正的常量 

**const 有作用域 有类型检查**

```c++
    #include <iostream> 
    #include <cstdio>
    using namespace std;

    int main() {
	    const int A = 5;
	    const int B = 6;
    	int array[A + B] = {0};
    	return 0;
    }
//c+C++不会有问题 c程序会出错
```

```c++
#include <iostream>
#include <cstdio>
void f() {
    #define N 100
    const int A = 100；
}
void g() {
    //printf("%d, %d\n", N, A);
    printf("%d\n", N);
}
int main() {
    g();
    f();
    return 0;
}
}
```

### 布尔类型

- C++中提供了逻辑bool类型，真值为true,假值为false，c中没有（用int类型的０和非０来实现）

- 非零即是true

  ```c++
  #include <iostream>
  using namespace std;
  int main(de) {
      int a = 5;
      bool b = false;
      cout << sizeof(b) << endl;//1
      cout << a << " " << b << endl;//5 0
      b++;
      cout << a << " " << b << endl;//5 1
      a = b + a;
      cout << a << " " << b << endl;//6 1
      return 0；
  }//在c++中 
  ```

  ```c++
  #include <iostream>
  using namespace std;
  int main() {
      int a = 1, b = 2;
      (a > b ? a : b) = 3;//c会报错 c++不会
      cout << a << " " << b << endl;
      return 0;
  }
  //c语言的三目运算符不能当左值 c++可以
  //c++中的三目运算符 返回一个变量的引用
  //如果换成（a > b ? a : 1） = 3 会报错 必须全是变量
  ```

- c语言中函数的参数不能有默认值 C++可以

- 函数声明时可以带默认值 实现不能代 ，有默认参数值的参数必须在参数表的最右端

  ```c++
  #include <iostream>???
  using namespace std;
  int add(int a = 3, int b = 5);
  int main() {
      int a = 6, b = 5;
      cout << add() << endl;
      return 0;
  }
  int add(int a = 9, int b = 0) {
      return a + b;
  }
  ```

- 函数的占位参数（只有类型没有实参）

## 函数重载

- 函数重载的规则(c不允许函数重载)

  - 重载只跟函数名和函数参数列表有关，与返回值无关（同一作用域）

    - 参数列表包括类型，顺序（类型不同 的）

  - 如何判断函数重载

    - **函数名** **参数列表** 函数实现 返回值

    - 同一作用域

    - 函数名相同

    - 参数列表不同（参数类型 参数个数 参数顺序）

    - 函数重载的本质是不同的函数

      - 地址不一样

      ```
      
      ```

    - 函数重载与指针一起用时

      - 参数个数相同
      - 参数类型相同
      - 返回值也必须相同

    - 编译器调用准则：

      - 所有的重载函数都作为备选对象
      - 编译器尝试寻找匹配的函数（精确匹配）
      - `f(int x = 1, int y = 2)`
      - `f()`-

- 后置运算符遵循这样的特点

  - 首先将i当前的值记录到一个临时变量中，然后对i进行自增操作，最后返回这个临时变量中。也就是说，后置运算符返回的是i执行自增操作之前的原始值，然后再进行自增操作。

- 函数没有被调用的时候，函数的形参并不占据实际的内存空间，也没有实质的值，当函数被调用的时候，系统会为ceshi形参分配内存空间，然后用实际参数为形参赋值。

- 主函数调用我们自己定义的函数时，会把实参传给一个形参类型和该实参相对应的函数，这个参数传递的过程，实际上是一个形参和实参相结合的过程，简称形实结合

  ```c++
  int i,j;
  int &ri=i;//建立一个int类型的引用ri，并将其初始化为i的一个别名
  j=10；
  ri=j;//相当于i=j;
  ```

- `&可以表示引用，也可以表示取地址`

  ```c++
  int a=3;
  int &ra=a; //定义引用
  int *p=&a; //取地址
  ```

- 定义函数可以定义默认形参，但是有默认值的形参必须放到形参列表的最后，也就是说，在有默认值的形参后面，不能出现没有默认值的形参

  `int add(int x,int y=5,int z=6); `是正确的

  `int add(int x=1,int y=5,int z);`　是错的
   `int add(int x,int y=5,int z);` 是错的

- 在c++中，如果使用`%s`读入字符串，只能将其保存在c风格的数组中，而不能直接将其保存到c++的`std::string`中，通过某些操作，可以实现`scanf`向`std::string`中输入，但是是不建议这样做。

- 使用Visual Studio时要注意，标准的`scanf`函数默认是不被编译器接受的，因为它不会检查读取的长度，这样就会给你的程序带来缓冲区溢出的漏洞。

- 如果想要使用`scanf`函数的话，可以在文件的开头进行以下预定义`#define _CRT_SECURE_NO_WARNINGS`

## 数据的封装

1.面向对象指导思想：以对象为核心（以谁做什么来表达程序的逻辑，将所有的数据操作转化为成员函数的调用，对象在程序中的所有行为都通过调用自己的函数来完成）

2.封装的好处：相比于直接赋值的情况，可以对传入的值进行非法判断等，对于有些数据成员我们只希望被外界进行读取，并不需要被外界来改变（只能读，不能写）



## new/delete

- new/delete

  - 是C++中的关键字
  - 在c中没有文件（stdlib.h）是不能用的　c++可以直接用
  - new 按数据类型分空间大小　（会保证至少给正好的空间　或者更多）
  - ？？malloc是根据

- 初始化`Test t5 = t3`

- 赋值`Test t5; t5 = t3;  `

- 不能用局部变量返回引用

- 

  ## 构造函数

  - 在对象实例化时被自动调用（一次）

  | 构造/析构函数           | 使用方法            |
  | ----------------------- | ------------------- |
  | 默认构造函数            | People a;           |
  | People(string name);    | People a("hug");    |
  | People(const People &a) | 拷贝构造，与=不等价 |
  | ～People();             | 无                  |

  全局区变量是有初值的　如果没初始化初值是０

  栈区堆区没有　是一个随机值　

  - 特点：
    - 没有返回值类型
    - 函数名必须与类名相同
    - 定义对象时自动调用
  - 构造函数可以重载（同一个类属于同一个作用域）重载时要遵循重载函数的规则
  - 实例化对象时即使有多个构造函数也只会用到一个构造函数
  - **当用户没有定义构造函数时，编译器自动生成一个构造函数**
  - 使用无参的构造函数不能写成`Test t3();`会被当做函数声明，要写成`Test t3;`
  - 当一个类是空类的时候，编译器会默认提供１个无参的构造函数
  - 构造函数的手动调用

- ```c++
  /*要求：开发一个数组类
  解决segmentfault:
  １．提供和获取长度的元素
  ２．提供获取数组元素的函数
  ３．提供修改数组元素的函数
  */
  #include <iostream>
  using namespace std;
  
  int main() {
      return 0;
  }
  ```

  拷贝构造函数

  - 在定义时，与普通的构造函数基本相同，只是在参数上有严格的要求；

    ```c++
    class Student {
        public:
        Student(){
            m_strName = "jim";
        }
        Student(const Student &stu) {
            //传与自己数据类型完全相同的引用　
        }
        private:
        	string m_strName;
    };
    ```

    

  - 如果类中没有定义拷贝构造函数时系统会自动生成一个默认的拷贝构造函数

  - 当采用直接初始化或复制初始化实例化对象时系统自动调用拷贝构造函数

  - 仅仅进行简单的值复制

  - 用已经？？初始化一个新的对象

  - 函数名是　类名（const class）一定要进行深拷贝　浅拷贝是拷贝之后物理状态相同　就是指向同一个地方　深拷贝是逻辑状态相同（对比了链表）

  - 手动实现拷贝构造函数必须深拷贝

  - ```c++
    #include <iostream>
    using std::cin;
    using std::cout;
    using std::endl;
    class Test {
    
        private:
        	int a;
        	int *p;
        public:
        Test() {
        	p = new int(1);
        }
        Test(const )
    }
    int main() {
        return 0;
    }
    ```

- 必须使用初始化列表来初始化

- 构造函数初始化列表

  ```c++
  class Student {
    public:
          Student():m_strName("jim"), m_iAge(10){
          }
      private:
          string m_strName;
      	int m_iAge;
  };
  ```

  

  - const 成员属性（真正常量/readonly?）
  - 类属性（类里有带参）
  - 注意事项：
    - 初始化列表的初始化顺序与成员属性的声明顺序相同
    - 初始化顺序与初始化列表中位置无关
    - 初始化列表优先函数体执行

- 尽量不要去使用全局对象（没有标准的顺序，用的时候可能没有）

- ｃ++标准中没有规定全局对象的构造顺序，所以不同的编译器

- 先父母再朋友再自己，析构顺序与构造顺序相反

### 构造函数总结

- **构造函数**：

  - 无参构造函数（默认构造函数）
  - 有参构造函数
    - 参数带默认值（所有参数都设置默认值——默认构造函数）
    - 参数无默认值

- 系统自动生成的函数:(如果我们手动定义了　系统就不会再生成)

  - 普通构造函数
  - 拷贝构造函数(不可以重载　没有返回值)

- > 初始化类列表必须在普通构造函数/拷贝构造函数的后边
  >
  > 用const修饰的常量只能使用初始化列表来初始化

## 析构函数

- 如果没有自定义的析构函数则系统自动生成
- 析构函数在对象销毁时自动调用
- 析构函数没有返回值，没有参数也不能重载

1. 定义格式：`~类名（）`

   ```c++
   class Student {
       public:
       Student() {
           cout << "Student" << endl;
       }
       ~Student() {
           cout << "~Student" << endl;
       }
       private:
       	string m_strName;
   };
   ```

2. 格式上不允许定义参数，也就不可能被重载

#### 对象的生命历程

申请内存——初始化列表——构造函数——参与运算——析构函数——释放内存　

- static 
  - 属于整个类　
  - 生命周期是整个程序　
  - 可以通过类名直接访问公有的静态成员变量
  - 所有对象都共享
  - 静态成员变量访问级别
- 静态成员方法的特性
  - 不依赖对象去访问属性
  - 静态成员函数不能直接访问成员变量
- 对象内存中存储方式
  - 对象
    - 属性　程序中要改变
    - 方法（函数）程序中不需要变得
    - 在内存中属性是自己的，方法是公有的
    - hanshuthis指针是某一个对象的地址（静态成员函数无this）
    - 构造函数也是成员函数有this指针

## const关键字

- const与基本数据类型

  `int x = 3;//变量`

  `const int x = 3; //常量　不可更改`

- const与指针类型

  `const int *p = NULL;`与

  `int const *p = NULL;`完全等价

  `const int * Sconst p = NULL;`与

  `int const * const p = NULL;`完全等价

  ```c++
  	int x = 3;
  	const int *p = &x;
  	p = &y;//正确
  	*p = 4;//错误　const修饰的是*p
  
  	int x = 3;
  	int *const p = &x;
  	p = &y;//错误　const修饰的Ｐ只能指向ｘ
  
  	const int x = 3;
  	const int *const p = &x;
  	p = &y;//错误
  	*p = 4;//错误
  ```

- const与引用

  ```c++
  	int x = 2;
  	const int &y = x;
  	x = 10;//正确
  	y = 20;//错误
  ```

  `const int x = 3; int *y = &x; //编译器禁止通过指针改变const常量`

- const对象的性质

  - const classname 变量名
  - 只读对象（里面的属性都是只读的　不能当左值用）
  - 在编译器里只读对象的成员属性不能被改变()
  - const 对象只能调用const 方法（const 方法　Type 函数（）const）

- const 方法定义

  - 类外 `Type classname::function() const {}`
  - 类内　`Type function() const {}`

- const 方法特性

  - const 对象只能调用const方法
  - const成员函数，内部只能调用const方法
  - const成员函数中不能更改变量的值

#### 继承就是为了代码复用

- 返回值优化

  ```c++
  #include <iostream>
  using std::cin;
  using std::cout;
  using std::endl;
  class Test {
      private:
          int i;
      public:
      Test(int v) {
          i = v;   
          cout << "Test(int i) : i = " << i << endl;
      }
      Test() {
          //Test(100);//产生了临时对象(密名对象) 生命周期/作用域只有这一行语句
          i = 0;
          cout << "Test() : i = " << i << endl;
      }
      Test(const Test &t) {
          i = t.i;//?? 
          cout << "Test(const Test &t) : i = " << i << endl; 
      }
      void printI() {
          cout << "i = " << i << endl;
      }
  };
  
  int main() {
      Test t = Test(100); //t = 10;
      t.printI();
      return 0;
  }
  
  ```

- 函数形参额初始化

`g++ test.cpp -fno-elide-constructors//默认开着返回值优化 执行此命令关掉`

## 继承

- 继承是类跟类之间的一种关系（继承 组合）

- 组合关系：

  - 类的对象被当做类的属性
  - 其他类的生命周期与当前类对象相同
  - 成员对象在用法上与普通成员相同

- 继承关系：类跟类的一种关系——单向关系

  ```c++
  //用法
  class A();
  class B:
  ```

  - 子类继承了父类的所有属性和方法（行为）
  - 子类是一种特殊的父类
  - 子类对象也可以当父类对象
  - **子类可以添加自己的属性和方法，还可以重写父类中的方法**

- 所有类的成员共享一套成员方法

继承方式（横排）

子类从父类中继承过来的属性方法访问权限（竖列）

![](/home/zoe/%E6%88%AA%E5%9B%BE/c++/%E7%BB%A7%E6%89%BF%E4%B8%AD%E5%AD%90%E7%B1%BB%E7%9A%84%E8%AE%BF%E9%97%AE%E6%9D%83%E9%99%90.png)

```c++

```

- 默认调用方式：

  要求父类构造函数必是无参或者是带默认参数的构造函数

- 继承的构造顺序：

  先去自动/手动调用父类的构造函数（必须有匹配的）

  再调用子类构造函数（构造函数调用的口诀：先父亲 再朋友 最后自己（可以递归使用））

1.子类对象构造时，需要先初始化父类各属性（需要调用父类构造函数）

2.构造函数函数顺序为先父亲后朋友再自己

3.**父类构造函数显式调用时**，**必须在子类构造函数的初始化列表里**

4.子类对象销毁时，同样需要调用父类析构函数（自动调用）

5.**先构造的后析构**

- 所有的方法都是共有的（每个对象的？？？？）

父子间同名冲突：子类与父类定义了相同名字的属性和方法（认为你想优先使用新定义的方法或者属性，自动的把父类的同名属性和方法隐藏）

- 子类和父类同名方法不构成重载关系（重写）
- 子类中定义父类中完全相反的函数
- 使用作用域分辨符区访问同名成员和方法



重写重载的区别：

```c++

```

父子兼容

- 子类是
- 父类对象指针可以指向子类对象
- 父类对象的引用可以引用子类对象

## 多态

编译期间编译器只能根据指针的类型去判断，调用父类的版本比较安全

### 对象模型

- 对象的成员属性和成员方法是分着存的
- 一个对象是一种特殊的结构体，运行时退化成结构体
  - 成员属性是依次排列的
  - 成员属之间可能存在内存空隙
  - 通过内存地址直接去访问
  - 访问权限只存在比编译器期有效，运行期无效

#### 多继承（尽量不要用）

- 多继承带来的问题：函数的二义性 数据冗余
- 解决的办法：虚继承（解决虚继承） 工程上不好管理 会带来多个？？指针
- 

## 多态

- 父子兼容时子类对象退化成父类对象。

- 多态：面向对象概念：不同的对象产生不同的行为

  

  ```c++
  //多态用法
  #include <iostream>
  #include <cstdio>
  #include <string>
  using namespace std;
  
  class Parent {
      public:
      virtual void say() {
          cout << "I'm Parent" << endl;
      }
  };
  
  class Child : public Parent {
      public:
      virtual void say() { //可以不写virtual 子类同名函数都会变成隐式多态函数
          cout << "I'm child" << endl;
      }
  };
  //父子兼容性，子类可以当父类
  //传父类子类对象都调父类函数，
  //父子兼容，子类对象退化成父类对象
  //为了安全调用父类的函数
  //希望根据对象的不同
  //多态：面向对象的概念，不同的对象产生不同行为
  //在子类中重写父类函数，传子类对象调子类函数，父类中调父类函数
  //关键字:virtual
  void how_to_say(Parent *p) {
      p->say();
  }
  int main() {
      Parent p;
      Child c;
      how_to_say(&p);
      how_to_say(&c);
      return 0;
  }
  
  ```

- 多态行为：根据实际对象调用重写函数 当指向父类对象时，调用父类对象函数，指向子类对象时，调用子类重写父类中同名函数

- c++支持多态的关键字是：virtual

- virtaul：声明多态  ？？？？？？被virtual修饰的函数叫虚函数

- 虚函数->特殊的一个叫纯虚函数->含有纯虚函数的类叫？？？？

- 多态的意义：

  1.在程序中表现出动态的特性 

  2.在子类中重写的父类同名函数必须声明成虚函数，否则没有意义

  3.多态是面向对象的基础

- 静态联编：程序在编译器件就知道调用哪个函数（函数重载）

- 动态联编：程序在运行期间才知道调用哪个函数（函数重写）

```c++
//通过一个小故事了解函数重写
#include <iostream>
#include <cstdio>
#include <string>
using std::cin;
using std::cout;
using std::endl;
using std::string;

class CompanyA_Boss {
    public:
    int battle() {
        int ret = 10;
        cout << "CompanyA_Boss::battle = " << ret << endl;
        return ret;
    }
};

class CompanyB_Boss {
    public:
    virtual int fight() {
        int ret = 9;
        cout << "CompanyB_Boss::fight = " << ret <<  endl;
        return ret;
    }
};

class CompanyB_NewBoss : public CompanyB_Boss {
    public:
    int fight() {
        int ret = CompanyB_Boss::fight()* 2;//调用成员方法，当前对象的父类方法 ：：作用域分辨符
        cout << "NewBoss::fight = " << ret << endl;
    }
};

void vs(CompanyA_Boss *c1, CompanyB_Boss *c2)  {
    int a = c1->battle();
    int b = c2->fight();
    if (a > b) {
        cout << "CompanyA is winner" << endl;
    } else {
        cout << "CompanyB is winner" << endl;
    }
}
int main() {
    cout << "first year" << endl;
    CompanyA_Boss c1;
    CompanyB_Boss c2;
    vs(&c1, &c2);
    cout << "second year" << endl;
    CompanyB_NewBoss nb;
    vs(&c1, &nb);
    return 0;
}
```

- c++中多态原理：virtual　编译器改变子类对象排布

  １．在类命名虚函数时，编译器会自动生成１个虚函数指针

  ２. 虚函数表是一个存储成员函数地址数据结构

  ３．虚函数表是由编译器自动生成和维护的（隐藏）

  ４．被virtual修饰的虚函数会被收入虚函数表中

  ５．存在虚函数时，每个对象会有指针指向虚函数表，指针在对象头部。

多态效率低于成员函数

- 总结：
  - 函数重写只能发生在父类和子类中间
  - 多态是指根据对象的具体类型去调用具体的函数
  - C++中virtual是支持多态的唯一方式
  - 被重写的函数具有多态性

#### 抽象类

- 被virtual修饰的函数叫虚函数
- 被virtual修饰，只有声明没有时间叫纯虚函数
- 一个类中含有纯虚函数，就是抽象类
  - 抽象类的特性：只能定义类型，不能产生对象；只能被继承，并重写相关函数的；某些相关函数没有被实现（纯虚函数）
- C++中没有真正的抽象类的概念，只能通过纯虚函数区简间接实现。
- 纯虚函数：只有声明，函数原型的成员函数
- 一个C++中的类，只要有纯虚函数，这个类就是抽象类。

```c++

```

- 接口是一种特殊的抽象类，是一组函数原型（ｃ++中没有直接的接口概念，可以用抽象类去模拟接口）

  - 这个抽象类中没成员变量
  - 所有成员函数都是公有的
  - 所有成员函数都是纯虚函数

  所以说接口类是一种特殊的抽象类

- 单继承和多接口

### 函数模板

#### 泛型编程：函数模板　类模板

- C++中交换两个变量的值有几种方法：

  - 宏：写的少　不安全
  - 全局（重载）被编译过　写的太多了

- 函数模板：一种泛型编程方式

- 泛型编程方式：不考虑具体数据类型的一种编程方式

- `template <typename T>`

  `template`

- 模板意义：１．在C++中泛型编程应用方式之一；２．能够根据实参类型进行参数类型推导；３．函数模板支持显示制定参数类型；４．函数模板是C++中代码复用的一种方式

- 自动推导实参参数类型

- 显式指定实参参数类型

- 函数模板使用注意事项：

  - 函数模板本身不支持类型的隐式转换
  - 在自动推导类型的时候，必须严格遵循类型匹配，而且不会进行隐式类型转换
  - 显式指定类型时，能够进行隐式类型转换

多个类型参数时：返回值类型无法进行推导；可以从左至右给出部分指定实参类型；如果有返回值类型？？？

优先看自？？？

编译器支持模板函数和普通函数构成重载函数

**不同函数的调用顺序：优先调用普通函数　然后模板函数　最后变参函数**

### 类模板

怎么判断一个变量是指针类型还是普通类型

不同的数据类型对数据进行操作

1. 类模板的用法`template <typename T>`
2. 系统不支持string类型相减　可以相加
3. 定义与声明不能分开写，会链接错误

类模板：

1. 当在类外实现成员函数时，返回值　class_nam?e<T>函数名　参数列表　函数体
2. **类模板的声明跟实现在同一个头文件中**　