### vs code快捷键

Ctrl + B     隐藏侧边栏

Ctrl + ~     隐藏下面边栏

Ctrl + [     整行左移

Ctrl + ]     整行右移

F11          全屏         

















### 内存分区

#### 代码区

存放函数的二进制代码，由操作系统进行管理

- 存放CPU执行的机器指令
- 代码区是**共享**的，共享的目的是对于频繁被执行的程序，只需在内存中有一份
- 代码区是**只读**的，目的是防止程序以外的修改它的指令

#### 栈区

由编译器自动分配，自动释放存放函数的参数，局部变量等

#### 堆区

由程序员手动开辟，手动释放

#### 全局区

存放全局变量和静态变量以及常量

- `全局区`
- `静态变量，关键字static修饰`
- `字符串常量`
- `const修饰的全局变量`

注意：const修饰的局部变量不属于全局区，





#### 

















### 函数

#### 函数默认参数

注意事项：

1.如果某个参数有默认值，那么从左往右的参数都要有默认值

2.如果函数声明有默认值，那么函数实现就不能有默认值

  即声明和实现只能有一个有默认参数

```c++
int fun(int a ,int b =10 ,int c =20)
{
    return a+b+c;
}

int func(int a=10 , int b= 20);
int func(int a ,int b)
{
    return a + b ;
}
```







#### 占位参数

占位参数可以有默认参数







#### 函数重载

函数重载满足条件：

1.同一作用域下

2.函数名相同

3.函数的参数类型不同，或者个数不同，类型不同

注意：当函数重载碰到默认参数时会出现二义性

```c++
int func(int a ,int b =10)
{
    return a ;
}
int func(int a )
{
    return a ;
}
int main()
{
    func(10); //会出现二义性，func（）不知道要调用哪一个函数
}
```



















### 封装

#### 封装权限

public:成员 类内部可以访问，类的外部也可以访问

protected:成员 类的内部可以访问，类的外部不可以访问

private:成员 类的内部可以访问，类的外部不可以访问















### 对象的初始化和清理

#### 构造函数

按参数分类：无参构造（默认构造），有参构造

按照类型分类 普通构造，拷贝函数构造

```c++
//调用方法
//括号法
class person
{
    person()
    {
        cout << "默认构造函数" << endl ;
    }
    person(int a)
    {
        m_A = a;
        cout << "有参构造函数" << endl;
    }
    person(const person & p)
    {
        m_A = p.m_A ;
        cout << "拷贝构造函数" << endl ;
    }
}
person p1() //默认构造函数的调用
person p2(a)//有参构造函数
person p3(p2)//拷贝构造函数

    
//显示法
person p1();
person p2 = person(10);
person p3 = person(p2);

//隐式转换法
person p1 = 10 ;
person p1 = p2 ;
```



#### 调用规则

- 编译器会至少给我们提供三个函数
- 默认构造函数
- 有参构造函数拷贝构造函数

1.如写了有参构造函数，则编译器不在写默认构造函数，但会给我们写一个拷贝构造函数（浅拷贝）

2.若我们写了拷贝构造函数，则编译器不再给我们提供任何其它函数



#### 类对象作为类成员

有类对象作为类成员的构造函数与都是普通成员的构造函数稍有不同

```c++
class perosn()
{
    public:
    	string person_name ;
    person(string name ) //person的有参构造函数
    {
        person_name = name ;
    }
}

class subject 
{
    public :
    	string my_subject ;
    	person p ;
    subject(string name , string personname): p(personname)//subject的构造函数
    {
        my_subject = name ;
    }
}

int main()
{
    subject("Alace","English") ;
}
```





#### 静态成员变量

静态成员变量的特点：

- 在编译阶段分配内存
- 类内声明，类外初始化
- 所有对象共享同一份数据

静态成员的两种访问方式：

```c++
class person
{
    public:
    	ststic int m_A ;
    
};

int m_A = 100 ;

int main()
{
    person p ;
    cout << p1.m_A << endl ; //通过成员访问
    cout << preson :: m_A << endl ; // 通过类名访问
    
}
    
```



#### 静态成员函数

- 所有对象共享同一个函数
- 静态成员函数**只能访问**静态成员变量



#### 常函数与常对象

```c++
//常函数不允许修改成员的值
//成员后面加上 mutable 在常函数中依然可以修改
class person
{
    public :
    	int m_A ;
    	mutable int m_B ;
    void show() const // 常函数定义
    {
        m_A = 100 ; //不允许
        m_B = 200 ; //允许
    }
};

// 常对象
// 常对象只能调用常函数
class person
{
    public :
    	int m_A = 100 ;
    	mutable int m_B = 200 ;
    void show() const
    {
        cout << "Hello World " << endl ;
    }
};
int main()
{
    const person p ;
    p.m_A = 10 ; //不允许
    p.m_B = 10 ; // 允许
    p.show(); //允许
}
```













### 友元



#### 全局函数做友元

```c++
class person
{
    friend void show ; // 全局函数做友元
	private :
    	int m_A = 10;
};

void show()
{
    person p ;
    cout << p.m_A << endl ;
}
```



#### 类做友元

#### 成员函数做友元





































### 运算符重载

运算符重载的概念：对一种符号进行重新的定义，赋予其另一种功能以适应不同的数据类型

作用：实现两个自定义类型数据的运算

#### ++ 重载

```c++
class person
{
    public:
        int m_A;
        int m_B;
    person operator+(person & p)  //函数成员重载 本质 p3=p1.operator+(p2);
    {
        person temp;
        temp.m_A = this->m_A + p.m_A;
        temp.m_B = this->m_B + p.m_B;
        return temp;
    }
};
person operator+(person &p1,person &p2)  //全局函数重载 本质person p3= operator+(p1,p2)
{
    person temp;
    temp.m_A=p1.m_A+p2.m_A;
    temp.m_B=p1.m_B+p2.m_B;
    return temp;
}

//重载本身也能发生函数重载
person operator+(person &p,int num)  //发生了函数重载，只是传入的参数不同
{
    person temp;
    temp.m_A=p.m_A+num;
    return temp;
}

int main()
{
    int num;
    person p1,p2,p3,p4;
    p1.m_A=10,p1.m_B=5;
    p2.m_A=10,p2.m_B=5;
    
    p4=p1+num;
    p3=p1+p2; //简化
    
    cout << "p4.m_A =" << p4.m_A << endl;
    cout << "p3.m_A = " << p3.m_A << endl;
    cout << "p3.m_B = " << p3.m_B << endl;
    system("pause");
    return 0;
}
```







#### << 重载

```c++
class person
{
    public:
        int m_A;
        int m_B;
    
};

ostream & operator<<(ostream & cout , person &p) //全局函数重载，相当于cout << p1
    {
        cout << p.m_A << endl;
        cout << p.m_B << endl;
        return cout; // 返回cout 为链式编程继续使用cout
    }
int main()
{
    person p1;
    p1.m_A=1;
    p1.m_B=2;
    cout << p1 << endl;

    system("pause");
    return 0;
}
```





#### =重载

```c++
class person
{
public:

	int *m_Age;

	person(int Age) //构造函数
	{
		m_Age = new int(Age); //开辟堆区
	}

	person& operator=(person &p)
	{
		if (m_Age != NULL)
		{
			delete m_Age;
			m_Age = NULL;
		}
		m_Age = new int(*p.m_Age);//深拷贝，解决堆区重复释放的问题
		return *this; //返回自身类型的数据，链式编程
	}

	~person()  //析构函数，释放堆区，手动开辟堆区，手动释放
	{
		if (m_Age != NULL)
		{
			delete m_Age;
			m_Age = NULL;
		}
	}
};

int main()
{
	person p1(10);
	person p2(20);
	person p3(30);
	p3=p2 = p1;
	cout << "p1.m_Age ：" << *p1.m_Age << endl;
	cout << "p2.m_Age ：" << *p2.m_Age << endl;
	cout << "p3.m_Age : " << *p3.m_Age << endl;

	system("pause");
	return 0;
}
//普通赋值运算符对两个对象进行赋值时是没有问题的，但是赋值对象一旦开辟到堆区时，由于会两次释放同一块内存，则是不被
//允许的，所以要进行深拷贝
class person
{
    public:
        int m_a;
        int m_b;
    person(int a,int b)
    {
        m_a=a;
        m_b=b;
    }
};

int main()
{
    person p1(1,2);
    person p2(3,4);
    p1=p2;
    cout << p1.m_a << " " << p1.m_b << endl;
    system("pause");
    return 0;

}
```



#### ++重载

```c++
class person
{
    public:
        int m_A;
    person& operator++() //前置 ++a 返回的是引用，目的是可以对同个数据反复操作
    {
        m_A++ ;
        return *this;
    }

    person operator++(int) //后置 a++ 返回的是值，因为临时变量在函数调用后即被释放，需要返回值
    {
        person temp = *this ;
        m_A++;
        return temp;
    }
};

ostream& operator<<(ostream &cout, person p)
{
    cout << p.m_A << endl;
    return cout ;
}

int main()
{
    person p1(10);
    person p2(20);

    cout << p1++ << endl ;
    cout << ++p2 << endl ;

    system("pause");
    return 0;
}
```











### 引用

引用就是给变量起一个别名，能够使两个变量名操作同一块地址





#### 引用的注意事项

1.引用必须初始化

2.引用一旦初始化，就不能更改。就是一旦指向一块地址，它就不能再指向别处了

#### 引用做函数参数

作用：引用做函数的参数，可以用形参来说改变实参的值

```c++
void swap(int &a ,int &b) //交换 a , b 的值
{
    int temp;
    temp = a ;
    a = b ;
    b = temp ;
}
```



#### 引用做返回值

注意：

1.不要返回局部变量的引用

2.函数可以作为可修改的左值















### 继承

#### 继承方式

```c++
class pereson           //父类
{
    public :
    	int m_A ;
    protected :
    	int m_B ;
    private :
    	int m_C ;
};
```



公有继承：

```c++
class person1 : public person
{
    
    public :
    	int m_A ;
    protected :
    	int m_B ;
    private :
    	int m_C ; //不可访问
};
```



保护继承：

```c++
class person2 : protected person 
{
    protected :
    	int m_A ;
    	int m_B ;
    private :
    	int m_C ;  //不可访问
}
```



私有继承：

```c++
class person3 :private person 
{
    private :
    	int m_A ;
    	int m_B ;
    private :
    	int m_C ; //不可访问
}
```





#### 继承中同名成员的处理

访问子类同名成员，直接访问

访问父类成员，加上父类作用域



####  多继承

```c++
class son : public father1 ,public father2
{
    .........
};
```

 



#### 菱形继承

```c++
class father
{
    public :
        int m_A ;
};

class son1 : virtual public father   //虚继承
{

};

class son2 : virtual public father  //虚继承
{

};

class grandson : public son1 ,public son2
{
    
};

int main()
{
    grandson g1 ;
    g1.son1::m_A = 100 ;
    g1.son2::m_A = 200 ;
    cout << g1.son1::m_A << endl ;
    cout << g1.son2::m_A << endl ;
    cout << g1.m_A << endl ;      // 可以直接访问，并且只有一份数据
 
    system ("pause");
    return 0;
}

// cl /d1 reportSingleClassLayoutgrandson '文件所在地' 报告单个类布局
```















### 多态

#### 多态的基本概念

- 静态多态：函数重载 和 运算符重载 属于静态多态
- 动态多态：派生类 和 虚函数 实现运行时多态

静态和动态多态的区别：

- 静态多态的地址在编译阶段就已经绑定
- 动态多态的地址在运行时才分配内存

```c++
class father
{
    public:
        void speak()
        {
            cout <<"Father is speaking" << endl ;
        }
};

class son : public father
{
    public :
        void speak()                             // 静态，在编译阶段就已经确定函数地址
        {
            cout << "Son is speaking" << endl ;
        }
        virtual void speak()                             // 动态，在运行阶段才确定函数地址
        {
            cout << "Son is speaking" << endl ;
        }
};

void show(father & f)                           // 要有继承关系，子类重写父类的虚函数，父类指针或者引用指向子类
{
    f.speak();
}

int main()
{
    son s ;
    show(s);
    
    system("pause");
    return 0 ;
}
```



#### 多态的小列子

```c++
#include<iostream>
using namespace std ;

class F_calculator  // 父类
{
    public :
        
        virtual int getresult()
        {
            return 0 ;
        }
        int m_A ;
        int m_B ;

};

class Addcalcultor : public F_calculator  // 加法类
{
    public :
         int getresult()
        {
            return m_A + m_B ;
        }
};

class Subcalcultor : public F_calculator //  减法类
{
    public :
        int getresult()
        {
            return m_A - m_B ;
        }
};

void Add()
{
    F_calculator * add = new Addcalcultor ;   // 父类指针指向子类对象
    add ->m_A = 1 ;
    add ->m_B = 1 ;
    cout << add->m_A <<"+" << add->m_B << "="<<add->getresult()<< endl ;
    delete add ;
}

void Sub()
{
    F_calculator * sub =new Subcalcultor ;  // 父类指针指向子类对象
    sub->m_A =2 ;
    sub->m_B =3 ;
    cout << sub->m_A << "-" << sub->m_B << "=" << sub->getresult()<< endl ;
    delete sub ;

}
int main()
{
    Add();
    Sub();
    system ("pause");
    return 0 ;
}
```



#### 纯虚函数与抽象类

在多态中，通常父类中的虚函数的实现是毫无意义的，主要都是调用子类重写的内容

因此可以将虚函数改为纯虚函数

当类中有了纯虚函数，这给类也称为抽象类

抽象类的特点：

无法实例化对象

子类必须重写父类中的纯虚函数，否则也属于抽象类

```c++
#include<iostream>
using namespace std ;

class Father
{
    public :
        
        virtual int getresult() = 0 ;  //纯虚函数
        int m_A ;
        int m_B ;

};

class Addson : public Father
{
    public :
        int getresult()               //子类重写父类虚函数
        {
            return m_A + m_B ;
        }
};

class Subson : public Father 
{
    public :
        int getresult()               //子类重写父类虚函数
        {
            return m_A - m_B ;
        }
};

void Add()
{
    Father * add = new Addson ;   // 父类指针指向子类对象
    add ->m_A = 1 ;
    add ->m_B = 1 ;
    cout << add->m_A <<"+" << add->m_B << "="<<add->getresult()<< endl ;
    delete add ;
}

void Sub()
{
    Father * sub =new Subson ; // 父类指针指向子类对象
    sub->m_A =2 ;
    sub->m_B =3 ;
    cout << sub->m_A << "-" << sub->m_B << "=" << sub->getresult()<< endl ;
    delete sub ;

}
int main()
{
    Add();
    Sub();
    system ("pause");
    return 0 ;
}
```







#### 虚析构与纯虚析构

如果子类中有属性开辟到堆区中，那么在多态发生时，父类指针在释放时无法调用到子类的析构代码

解决方法：

将父类的析构函数改为虚析构或者纯虚析构



```c++
#include<iostream>
#include<string>
using namespace std ;

class Father
{
    public :
        Father()
        {
            cout << "Father" << endl ;
            
        }
        virtual ~Father()                   //虚析构
        {
            cout << "~Father" << endl ;
        }

        virtual void speak()
        {
            cout << "Father is speaking" << endl ;
        }

};

class Son : public Father
{
    public :
        string *m_name ;                //子类属性开辟到堆区

        Son(string name)
        {
            m_name = new string (name) ;
            cout << "Son" << endl ;
        }

        ~Son()
        {
            if (m_name != NULL)
            {
                delete m_name ;
                m_name = NULL ;
                cout << "~Son" << endl ;
            }
        }

        virtual void speak()
        {
            cout << "Son is speaking" << endl ;
        }

};

void dowork()
{
    Father * f = new Son("Tom") ;
    f->speak();
    delete f ;
}

int main()
{
    dowork();

    system("pause");
    return 0 ;
}
```

























### 文件

#### 写文件

1.头文件包含头文件 #include<fstream>

2.创建对象

- 写文件  ostream
- 读文件  istream
- 读写文件  fstream

3.路径及其打开方式

|   ios::in   | 为读文件而打开           |
| :---------: | ------------------------ |
|  ios::out   | 为写文件而打开           |
|  ios::ate   | 初始位置文件尾           |
|  ios::app   | 追加方式写文件           |
| ios::trunc  | 如果文件存在先删除在创建 |
| ios::binary | 二进制方式               |

4.操作完毕，关闭文件

```c++
#include<iostream>
using namespace std ;
#include<fstream>

int main()
{
    ofstream ofs ;
    ofs.open("test.txt",ios::out);
    ofs << "Hello,World " << endl ;
    ofs.close() ;
    system("pause");
    return 0 ;
}

```





#### 读文件

1.包含头文件 #include<fstream>

2.创建对象   ifstream ifs ;

3.路径及其打开方式

4.读文件

```c++
//第一种方法
char buffer [n] = {0} ; //初始化数组
while (ifs >> buffer)
{
    cout << buffer ;
}

//第二种方法
char buffer [n] = {0};
while (ifs.getline(buffer,sizeof(buffer)))
{
    cout << buffer ;
}

//第三种方法
string buffer ;
while(getline(ifs,buffer))
{
    cout << buffer ;
}

```

5.操作完毕，关闭文件





```c++
//合起来

#include<iostream>
#include<string>
using namespace std ;
#include<fstream>

void Write()
{
    ofstream ofs ;
    ofs.open("test.txt",ios :: trunc);
    ofs << "This is World !" << endl ;
    ofs << "Hello World ! " << endl ; 
    ofs.close() ;
}

void read()
{
    ifstream ifs ;
    ifs.open ("test.txt",ios :: in) ;
    if ( ! ifs.is_open())
    {
        cout << "File open failed" << endl ;
    }

    string buffer ;
    while(getline(ifs,buffer))
    {
        cout << buffer << endl ;
    }
    ifs.close () ;
}

int main()
{
    Write();
    read();
    system("pause");
    return 0 ;
}

```





















