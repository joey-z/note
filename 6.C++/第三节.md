## 从C到C++

- ｆ()和ｆ(void)的区别
  - c 　ｆ()可以传n个参数　ｆ(void) 不能传参
  - c++  无区别　都不能传参
- ｃ++是一种强数据类型的语言
- ｃ++是ｃ的超集
- 异常和bug区别
- 编程范式　
  - 面向过程（随着问题规模的增大）　
    - 难以维护
    - 可移植性不好
  - 面向对象（）
  - 泛型编程
  - 函数式编程
- 运算符里不能重载的只有５个

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

- 访问限定符

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
      return 0;
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

  

## 两个关键字

- new/delete

  - 是C++中的关键字
  - 在c中没有文件（stdlib.h）是不能用的　c++可以直接用
  - new 按数据类型分空间大小　（会保证至少给正好的空间　或者更多）
  - ？？malloc是根据

- 初始化`Test t5 = t3`

- 赋值`Test t5; t5 = t3;  `

- 不能用局部变量返回引用

- 命名空间的嵌套

  ```c++
  #include <iostream>
  
  ```

- 类与对象

  - 访问权限

    - public(公共访问权限)

    - private(私有的访问权限)

    - protected(受保护的访问权限)

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

      

  - 访问修改类里面的对象时要通过　去做

- 构造函数

  - | 构造/析构函数           | 使用方法            |
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
    - 构造函数可以重载（同一个类属于同一个作用域）
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

  - 当类中没有定义拷贝构造函数时会默认定义一个拷贝构造函数

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

  - const 成员属性（真正常量/readonly?）
  - 类属性（类里有带参）
  - 注意事项：
    - 初始化列表的初始化顺序与成员属性的声明顺序相同
    - 初始化顺序与初始化列表中位置无关
    - 初始化列表优先函数体执行

- 尽量不要去使用全局对象（没有标准的顺序，用的时候可能没有）

- ｃ++标准中没有规定全局对象的构造顺序，所以不同的编译器

- 先父母再朋友再自己，析构顺序与构造顺序相反

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
    - this指针是某一个对象的地址（静态成员函数无this）
    - 构造函数也是成员函数有this指针

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

- 继承就是为了代码复用

- 返回值优化

  ```c++
  	> File Name: 0108.cpp
  	> Author: Zoe 
  	> Mail: 
  	> Created Time: 2019年01月08日 星期二 18时13分45秒
   ************************************************************************/
  
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

![](/home/zoe/截图/c++/继承中子类的访问权限.png)

```c++

```

- 默认调用方式：
  - 要求父类构造函数必是无参或者是带默认参数的构造函数
- 继承的构造顺序：
  - 先去自动/手动调用父类的构造函数（必须有匹配的）
  - 再调用子类构造函数（构造函数调用的口诀：先父亲 再朋友 最后自己（可以递归使用））

1.子类对象构造时，需要先初始化父类各属性（需要调用父类构造函数）

2.构造函数函数顺序为先父亲后朋友再自己

3.**父类构造函数显式调用时**，**必须在子类构造函数的初始化列表里**

4.子类对象销毁时，同样需要调用父类析构函数（自动调用）

5.**先构造的后析构**

- 所有的方法都是共有的（每个对象的？？？？）

父子间同名冲突：子类与父类定义了相同名字的属性和方法（认为你想优先使用新定义的方法或者属性，自动的把父类的同名属性和方法隐藏）



- 

- 子类和父类同名方法不构成重载关系（重写）
- 子类中定义父类中完全相反的函数
- 使用作用域分辨符区访问同名成员和方法



重写重载的区别：

```c++

```

父子兼容

-  子类是
- 父类对象指针可以指向子类对象
- 父类对象的引用可以引用子类对象

## 多态

编译期间编译器只能根据指针的类型去判断，调用父类的版本比较安全

#### 对象模型

- 对象的成员属性和成员方法是分着存的
- 一个对象是一种特殊的结构体，运行时退化成结构体
  - 成员属性是依次排列的
  - 成员属之间可能存在内存空隙
  - 通过内存地址直接去访问
  - 访问权限只存在比编译器期有效，运行期无效