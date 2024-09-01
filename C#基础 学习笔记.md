# C#基础 学习笔记

## 1.隐式转换与显示转换

### 1.1 隐式转换

总的概述：用大范围去装小范围

### 1.2 显示转换

#### 1.2.1 括号强转

**重点注意精度问题和范围问题**

加()，例如：

```c#
int i=40000;
long l=(long)i;
```

但是，在转换过程中，应当注意大小区间，例如：

```c#
int i=40000;
short s=(short)i;
//溢出
```

特别的，面对有符号与无符号的数据类型转换需更加谨慎，整数与浮点数之间的转换会舍弃小数点后的所有位数，bool类型，string类型不支持括号强制转换

#### 1.2.2 Parse法

作用：将字符串转化为其他类型

语法：变量类型.Parse("string")

注意：字符串必须是可以转换对应类型的字符串，否则将报错，值的范围也应该是合法合规的

```c#
int i=int.Parse("123");
Console.WriteLine(i);
>>123

int i=int.Parse("123.45");
Console.WriteLine(i);
>>异常

short i=short.Parse("40000");
Console.WriteLine(i);
>>异常
```

#### 1.2.3 Convert法

作用：将各个类型之间相互转换

语法：Convert.To目标类型(常量或变量)

注意：填写的变量必须正确

```c#
Console.WriteLine(Convent.ToInt32("123"));
>>123
Console.WriteLine(Convent.ToInt32(114.514f));
>>115//会四舍五入
```

## 2.枚举

### 2.1 枚举的概念

#### 2.1.1 枚举是什么

被命名的整形常量集合，一般用于表示状态，类型等。

注意：申明枚举与申明枚举变量是不一样的。申明枚举不能在任何函数与方法中，应当在类，结构体，命名空间中。而申明枚举变量是使用申明的枚举类型创造一个枚举变量。

#### 2.1.2 申明枚举语法

```c#
enum E_NAME
{
	selfname1,
	selfname2,
	selfname3,
}
```

### 2.2 枚举的应用

#### 2.2.1 枚举的使用

```c#
using System;
namespace enumerate
{
	class Program
	{
		enum Etype
		{
			boss,
			normal,
		}
		static void main(string[] args)
		{
			Console.Writeline("enumerate");
			Etype type=Etype boss;
			switch(type)
			{
				case Etype.boss:
					Console.WriteLine("boss");
					break;
				case Etype.normal:
					Console.WriteLine("normal");
					break;
				default:
					Console.WriteLine("none");
					break;
			}
		}
	}
}
```

#### 2.2.2 枚举的转换

##### 2.2.2.1 枚举与int互换

```c#
//枚举转int
int i=(int)type;
Console.WriteLine(i);
//int转枚举
type=0
```

##### 2.2.2.2 枚举与string互换

```c#
//枚举转string
string str=type.Tostring();
Console.WriteLine(str);
//string转枚举
//Parse后的第一个参数是想要转换的枚举类型，第二个参数是
type=(Etype)Enum.Parse(typeof(Etype),"normal");
Console.WriteLine(type);
```

#### 2.2.3 枚举的作用

最主要的作用是清晰状态含义。

## 3.一维数组

#### 3.1 数组的形式

一般形式为 

变量类型 [ ] 数组名;

变量类型 [ ] 数组名 = new 变量类型[n];

变量类型 [ ] 数组名 = new 变量类型[n]{};

变量类型 [ ] 数组名 = new 变量类型[ ]{ , , , , };

变量类型 [ ] 数组名 = { , , , , , };

```c#
int [] arr1;
int [] arr2=new int[n];
int [] arr3=new int[n]{1,3,4,5,6};
int [] arr4=new int[]{1,3,4,5};
int [] arr5={1,2,3,4,5,6};
```

#### 3.2 数组的使用

```c#
int [] array = {1,2,3,4,5};
```

##### 3.2.1 数组的长度

```c#
Console.WriteLine(array.length);
```

##### 3.2.2 获取数组中的元素

```c#
Console.WriteLine(array[n]);//注意不要越界
```

##### 3.2.3 修改数组中的元素

```c#
array [n]=a;
```

##### 3.1.2.4 遍历数组

```c#
for(int i=0;i<array.length;i++)
{
	Console.WriteLine(array[i]);
}
```

## 4.二维数组

#### 4.1 二维数组的形式

```c#
int [,] array = new int [a,b];
int [,] array = {{1,2,3}},
				{4,5,6}};
```

#### 4.2 二维数组的使用

##### 4.2.1  二维数组的长度

行，列

```c#
Console.WriteLine(array.GetLength(0));
Console.WriteLine(array.GetLength(1));
```

## 5.交错数组

#### 5.1 交错数组的形式

```
int [][] array=new int [(行数)][];
int [][] array=new int [][]{new int[]{1,2,3},
					      new int[]{4,5},
					      new int[]{6}};
```

### 5.2 交错数组的使用

#### 5.2.1 交错数组的长度

行/列

```
Console.WriteLine(array.GetLength(0));
Console.WriteLine(array[0].length);
```

## 6.值类型与引用类型

### 6.1 值类型与引用类型的分类

引用类型：string，类，数组

值类型：结构体，其他

### 6.2 值类型与引用类型的区别

```c#
int a= 10;
int [] arr= new int []{1,2,3,4,5};
int b=a;
int [] arr2=arr;
Console.WriteLine("a={0},b={1}",a,b);
Console.WriteLine("arr[0]={0},arr2[0]={1}",arr[0],arr2[0]);

>>a=10,b=10
>>arr[0]=1,arr2[0]=1

b=20,arr2[0]=5;
Console.WriteLine("a={0},b={1}",a,b);
Console.WriteLine("arr[0]={0},arr2[0]={1}",arr[0],arr2[0]);

>>a=10,b=20
>>arr[0]=5,arr2[0]=5
```

值类型在相互赋值时，将内容拷贝给了对方，它变我不变。

引用类型在相互赋值时，让两者指向同一个值，它变我也变。

原因在于，值类型与引用类型在储存区域和储存方式都有不同。

值类型存储于栈里面，栈是一种由系统分配，自动回收的数据结构，而引用类型存储于堆里面，堆是一种手动申请，手动回收的数据结构。

### 6.3 特殊的引用类型——string

```c#
string str1="123";
string str2=str1;
str2="321";
```

string作为一种特殊的引用类型，它有值类型的特征。这代表着频繁改变string的值会产生内存垃圾。

## 7.函数

### 7.1 函数的作用

1.封装代码

2.提高代码利用率

3.抽象行为

### 7.2 函数的位置

1.class语句块中

2.struct语句块中

### 7.3 函数的形式

```c#
static int(类型) name(函数名)(参数类型 参数名,参数类型 参数名,......)
{
	//语句块
	return ...;
}
```

函数形式里static不是必须的，函数命名须讲究帕斯卡命名法。

带参数函数有多返回值

```c#
static int[] calc(int a,int b)
{
	int sum=a+b;
	int avg=sum/2;
	int []arr={sum,avg};
	return new int[] {sum,avg};
}
```

## 8.ref与out

### 8.1 为什么要学习ref和out

可以解决在函数内部改变外部传入的内容，里面变了外面也要变。

### 8.2 ref和out的使用

```c#
ststic void ChangeValue(int value)
{
	value=3;
}
static void Main(String [] args)
{
	int a=1;
	ChangeValue(a);
	Console.WriteLine("a={0}",a);
}

>>a=1

static void ChangeValue(ref int value)
{
	......
}
static void Main(String [] args)
{
	......
	ChangeValue(ref a);
	......
}

static void ChangeValue(out int value)
{
	......
}
static void Main(String [] args)
{
	......
	ChangeValue(out a);
	......
}
```

### 8.3 ref和out的区别

ref传入的变量必须初始化，out不用。

```
int a=1;
ChangeValue(ref a)

int a;
ChangeValue(out a)
```

out传入的变量必须在内部赋值，ref不用。

```
ststic void ChangeValue(int value)
{
	value=3;
}
.......
ChangeValue(out a)

ststic void ChangeValue(int value)
{
	value;
}
.......
ChangeValue(ref a)
```

## 9.变长参数与参数默认值

### 9.1 变长参数关键字

关键字：params

```
static int Sum(params int [] arr)
{
	......
}
```

注意：

1.params后面必为数组

2.数组类型为任意类型

3.函数参数可以有别的参数和params修饰的参数

4.函数中最多只能出现一个params关键字，并且一定是在最后一个参数，前面可以有无数个其他参数

### 9.2 参数默认值

有默认值的参数一般称为可选参数。

作用：调用函数可以不传参数，不传参数时用默认值传入参数。

```
static void Speak(string str="Hikari")
{
	Console.writeLine(str);
}
......
Speak();
```

注意：

1.可选参数支持多参数。

2.在混用时，普通参数要放在可选参数之前。

## 10.函数重载

### 10.1 基本概念

在同一语块中(struct,class)，函数/方法名相同，参数的数量不同或者是参数的数量相同但类型或顺序不同。

注意：

1.重载只与参数类型，顺序，个数有关，与其他无关

2.调用时，程序会根据参入的参数类型调用对应的函数

```c#
//参数数量不同
static int Sum(int a,int b)
{
	return a+b;
}
static int Sum(int a,int b,int c)
{
	return a+b+c;
}
static void Main(string[] args)
{
	Sum(1,2,3);
	sum(1,2)
}

//数量相同，类型不同
static float Sum(float a,float b)
{
	return a+b;
}
static int Sum(int a,int b)
{
	return a+b;
}
static float Sum(int a,float b)
{
	return a+b;
}
static void Main(string[] args)
{
	Sum(1,1.1f);
}

//数量相同，顺序不同
static float Sum(int a,float b)
{
	return a+b;
}
static float Sum(float a,int b)
{
	return a+b;
}
static float Sum(int a,float b)
{
	return a+b;
}
static void Main(string[] args)
{
	Sum(1,1.1f);
	Sum(i.1f,1);
}

//ref和out
static float Sum(ref int a,float b)
{
    return a+b;
}
static float Sum(int a,int b,params int []arr)
{
    return ......;
}
//可选参数不能认为函数重载
```

作用：处理同一类型不同参数的逻辑处理。

## 11. 递归函数

### 递归函数的概念

递归就是函数自己调用自己。

一个正规的递归函数

1.必须有结束递归的条件

2.用于条件判断的条件必须能够达到停止的目的

```c#
static int Func()
{
	if(false)
	{
		return;
	}
	Func();
}
```

## 12. 结构体

### 12.1 结构体的概念

一种自定义变量类型，是函数与数据的结合，在结构体中可以申请各种变量和方法。作用是表现存在关系的数据集合，比如用结构体表现学生成绩等等。

### 12.2 基础语法

1.结构体一般写在namespace语句中，

2.关键字：struct

```c#
struct SelfStruct
{
	//变量/构造函数/函数
}
```

### 12.3 实例

```c#
struct Student
{
    //变量
    //结构体申明的变量不能直接被初始化
    //变量类型可以写任意类型，除了自身的结构体
	int age;
	bool sex;
	int number;
	string name;
    S s;
    //函数方法
    //在结构体的函数方法不需要加static
    void Speak
    {
        Console.WriteLine("My name is {0},I'm {1} years old.",name,age);
    }
}
struct S
{
    ......;
}
```

### 12.4 结构体的使用

```c#
struct Student
{
	int age;
	bool sex;
	int number;
	string name;
    void Speak
    {
        Console.WriteLine("My name is {0},I'm {1} years old.",name,age);
    }
}
static void Main(string [] args)
{
	Student s1;
    s1.age=10;
}

```

### 12.5 访问修饰符

修饰结构体中变量的方法，是否能被外界使用。主要有public/private，默认为private。

### 12.6 构造函数

基本概念：

1.没有返回值

2.函数名和结构体名相同

3.必须有参数

4.如果申明了构造函数，那么必须在其中对所有变量初始化。

```c#
public Student(int age,bool sex,int number,string name)
{
	//this关键字
	this.age=age;
	this.sex=sex;
	this.number=number;
	this.name=name;
}
......
static void Main(string[] args)
{
    ......
    Student s2 =new Student(18,true,2023000,"Hikari");
    ......
}
```

## 13.冒泡排序

###  13.1 基本原理

两两相邻，不停比较，不停交换，比较n轮

### 13.2 代码实现

```
static void Main(string [] args) 
{
	int [] arr;
	
	for(int i=0;i<arr.Length;i++)
	{
		bool isSort=false;
		for(int j=0;j<arr.Length-1-i;j++)
		{
			isSort=true;
			int temp=arr[j];
			arr[j]=arr[j+1];
			arr[j+1]=temp;
		}
		if(!isSort)
		{
			break;
		}
	}
}
```

## 14. 选择排序

### 14.1 基本原理

新建中间商，依次比较，找出极值，放入目标位置，比较n轮

### 14.2 代码实现

```
static void Main(string [] args)
{
	int [] arr;
	for(int i=0;i<arr.Length;i++)
	{
		int m=0;
		for(int j=1;j<arr.Length-i;j++)
		{
			if(arr[m]<arr[j])
			{
				m=j;
			}
		}
		if(m!=arr.Length-1-i)
		{
			int temp=arr[m];
			arr[m]=arr[Length-1-i];
			arr[Length-1-i]=temp;
		}
	}
}
```

## 15. 类与对象

### 15.1 什么是类

具有相同事物特征，具有相同行为，一类事物的抽象，通过类创建对象，申明在namespace中。

### 15.2 申明类的语法

```
class ClassName
{
	......;(成员变量，成员方法，成员属性，构造函数，析构函数，索引器，运算符重载，静态成员)
}
```

### 15.3 申明实例

```
class Person
{
	......;
}
```

同一语句块的不同类不能重名。

### 15.4 什么是类对象

对象是由类创建出来的，一般称为实例化对象。

### 15.5 实例化对象基本语法

```
ClassName variable;
ClassName variable=null;
ClassName variable=new ClassName();

Person p3 =new Person();
```

## 16. 成员变量与访问修饰符

### 16.1 成员变量

1.申明在语句块中

2.用来描述对象特征

3.可以是任意变量类型

4.数量不做限制

5.是否赋值根据需求来确定

```
enum E_SexType
{
	man,
	woman,
}
class Person
{
	string name;
	int age;
	E_SexType sex;
}
//如果要在类中申明一个同类的成员变量，则不能将其初始化。
```



### 16.2 访问修饰符

```
public(公有) private(私有) protect(保护)
```

### 16.3 成员变量的使用和初始值

```
static void Main(string[] args)
{
	Person p=new Person();
	p.age=10;
	Console.WriteLine(p.age);
}
//观察默认值：default
Console.WriteLine(default(Person));
```

## 17. 成员方法

### 17.1 成员方法的基本概念

1.申明在类语句块中

2.用来描述对象行为

3.规则和函数申明规则相同

4.受到访问修饰符的限制

5.返回值参数不做限制

6.方法数量不做限制

注意：

1.成员方法不要加static关键字

2.成员方法必须实例化出对象，再通过对象来使用，相当于该对象执行了某个行为

3.成员方法受到访问修饰符的限制

```
class Person
{
	public void Speak(string str)
	{
		Console.WriteLine("{0}说{1}",name,str);
	}
	public bool IsAdult()
	{
		return age>=18;
	}
	public string name;
	public int age;
}
```

### 17.2 成员方法的使用

```
static void Main(string[] args)
{
	......;
	string str1="";
	Console.ReadLine(str1);
	Person p=new Person();
	p.Speak(str1);
	......;
}
```

## 18. 构造函数，析构函数，垃圾回收

### 18.1 构造函数

```
class Person
{
	public string name;
	public int age;
	public Person(string name,int age)
	{
		this.name=name;
		this.age=age;
	}
}
static void Main(string[] args)
{
	Person p= new Person("Hikari",18);
}
//如果不自己实现无参构造构造函数而实现了有参构造函数，会失去默认的无参构造
```

### 18.2 析构函数

在引用类型的堆内存回收时，会调用该函数。

```
~Person
{
	
}
```

### 18.3  垃圾回收

将数据分为0代，1代，2代内存，新分配的内存都会被分配在第0代内存中，83kb以上被称为大对象。GC会标记对象，可标记的是可达对象，反之则为不可达对象。不可达对象就被认为是垃圾。然后搬迁对象压缩堆，释放未标记的对象，搬迁可达对象，修改应用地址。

大对象一般认为储存在2代内存中，目的是减少损耗，提高性能。

```
GC.Collect()//手动触发GC,通常在loading条调动
```

## 19. 成员属性

### 19.1 成员属性的基本概念

1.保护成员变量

2.为成员属性的获取和赋值添加逻辑处理。

3.解决3P的局限性

4.属性可以让成员变量在外部只能获取，不能修改或者只能修改，不能获取。

### 19.2 成员属性的基本语法

```
访问修饰符 属性类型 属性名
{
	get{};
	set{};
}
class Person
{
	private string name;
	private int age;
	
	public string Name;
	{
		get
		{
			return name;
		}
		set
		{
			//value 关键字用来表示外部传入的值 
			name=value;
		}
	}
}

```

### 19.3 成员属性的使用

```
Person p=new Person()
{
	p.Name=Console.ReadLine();
	Console.WriteLine(p.Name);
}

```

### 19.4 get和set前面可以加修饰符

注意：

1.默认不加，会使用属性申明的访问权限

2.加的访问修饰符要低于属性的访问权限

3.不能让get和set的访问权限都低于属性的权限

```
class Person
{
	private string name;
	private int age;
	
	public string Name;
	{
		private get
		{
			return name;
		}
		set
		{
			//value 关键字用来表示外部传入的值 
			name=value;
		}
	}
}
```

### 19.5 get和set可以只有 一个

在只有一个的时候，就不用加修饰符

### 19.6 自动属性

外部能得不能改的属性

```
public float Height
{
	get;
	set;
}
```

## 20. 索引器 

### 20.1 索引器基本概念

让对象可以像数组一样通过索引访问其中元素，使程序看起来更直观，更容易编写

### 20.2 索引器语法及使用

```
class Person
{
	private string name;
	private int age;
	private Person[] friends;
	
	public Person this[int index]
	{
	//索引器中可以写逻辑
		
		get
		{
             if(friends == null)
                return null;
            else if(friend.Length-1<index)
                return null;
			return friends[index];
		}
		set
		{
		if(friends == null)
			friends=new Person[]
			{
				friends=new Person[]{value};
			}
		else if(friend.Length-1<index)
			return null;
			friends[index]=value;
		}
	}
}
......
static void Main(string [] args)
{
	......
	Person p =new Person();
	p[0]=new Person();
	Console.WriteLine(p[0]);
	......
}
```

### 20.3 索引器可以重载

```
class Person
{
	private int[,]array;
	public int this[int i,int j]
	{
		get
		{
			return array[i,j];
		}
		set
		{
			array[i,j]=value;
		}
	}
	public string this[string str]
	{
		get
		{
			switch(str)
			{
				case "name":
					return this.name;
				case "age":
					return age.ToString();
			}
			return "";
		}
	}
}
```

## 21. 静态成员

### 23.1 静态成员的概念

静态关键字 static

用static修饰的成员变量，方法，属性等称为静态成员，静态成员的特点是直接用类名点出使用

### 23.2 自定义静态成员

```
class Test
{
	static public float PI=3.14f;
	public int TestInt=1;
	public static float CalCircle(float r)
	{
		return PI*r*r;
	}
}
```

### 23.4 静态成员的使用

```
class Program
{
	static void Main(string[] args)
	{
		Console.WriteLine(Test.PI);
		Console.writeLine(Test.CalCircle(2));
		
		Test t=new Test();
		Console.WriteLine(t.TestInt);
	}
}
```

### 23.5 为什么可以直接引用静态成员

程序是不能无中生有的，我们要使用的对象，变量，函数都是要在内存中分配变量空间的，之所以要实例化对象,目的是为了分配内存空间，在程序中产生一个抽象的对象。

而静态成员会在程序开始运行时，就会分配内存空间所以能直接使用。静态成员与程序同生共死，只要使用了它，直到程序结束了才会释放。同时具备了唯一性和全局性。

### 23.6 静态函数不能直接使用非静态成员

普通成员变量需要将对象实例化后才能使用，而静态成员不用。在静态函数中使用非静态成员会报错。

### 23.7 非静态函数可以直接使用非静态成员

### 23.8 静态成员的的作用

静态变量：

1.常用唯一变量的申明

2.方便别人获取的对象申明

静态方法：

常用唯一的方法申明，例如相同规则的数学计算相关函数

### 23.9 常量与静态变量

const可以理解为特殊的static

它们都可以用类名点出

但是

1.const必须初始化，不能修改，static没有这个规则

2.const只能修饰变量，static可以修饰很多

3.const一定是写在访问修饰符后的，static没有这个要求

```
public const int G=1;
```

## 24. 静态类与静态构造函数

### 24.1 静态类

概念：用static修饰的类

特点：只能包含静态成员，不能被实例化

作用：

1.将常用的静态成员写在静态类里，方便使用

2.静态类不能被实例化，更能体现工具类的唯一性（console）

```
static class TestStatic
{
	public static int a;
	public static void Testfun()
	{
		......
	}
	public static int TestIndex
	{
		get;
		set;
	}
}
```

### 24.2 静态构造函数

概念：在构造函数前加上static修饰

特点：

1.静态类和普通类都可以有

2.不能使用访问修饰符

3.不能有参数

4.只会自动调用一次

作用：

在静态构造函数中初始化静态变量

使用：

1.静态类中静态构造函数

```
static class StaticClass
{
	public static int testInt=100;
	public static int testInt2=100;
	
	static StaticClass()
	{
		Console.WriteLine("静态构造函数");
	}
}
class Program
{
	Console.WriteLine(StaticClass.testInt);
	Console.WriteLine(StaticClass.testInt2);
}
>>静态构造函数
  100
  100
```

2.普通类中静态构造函数

```
class Test
{
	public static int testInt=200;
	static Test()
	{
		Console.WriteLine("静态构造");
	}
	public Test()
	{
		Console.WriteLine("普通构造");
	}
}
>>静态构造
  200
  普通构造
  普通构造
```

## 25. 扩展方法

### 25.1 基本概念

为现有非静态的变量类型添加新方法

作用：

1.提升程序扩展性

2.不需要再对象中重写方法

3.不需要继承来添加方法

4.为别人封装的类型提供额外的方法

特点：

1.一定是写在静态类中

2.一定是个静态函数

3.第一个参数拓展目标

4.第一个参数用this修饰

### 25.2 基本语法及实例

```
//访问修饰符 static 返回值 函数名(this 拓展类名 参数名，参数类型，参数名，参数类型，参数名...)
static class Tools
{
	//为int拓展了一个成员方法
	//成员方法是需要实例化后才能使用的
	public static void SpeakValue(this int value)//这个value就是i
	{
		//拓展方法逻辑
		Console.WriteLine("拓展方法"+value);
	}
}
class Program
{
	static void Main(string[] args)
	{
		int i=10;
		i.SpeakValue()
	}
}
>>拓展方法10
```

### 25.3 自定义类型拓展方法

```
class Test
{
	public int i=10;
	public void Fun1()
	{
		Console.WriteLine("123");
	}
	public void Fun2()
	{
		Console.WriteLine("456");
	}
}
static class Tools
{
	public static void Fun2(this Test t)
	{
		Console.WriteLine("为test拓展的方法");
	}
}
class Program
{
	static void Main(string[] args)
	{
		Test t=new Test();
		t.Fun2();
	}
}
//当拓展方法与实例方法冲突，会调用实例方法
```

## 26. 运算符重载 

### 26.1 概念

让自定义类和结构体能够使用运算符，关键字operator

特点：

1.是一个公共的静态方法

2.返回值写在operator前

3.返回处理自定义

作用：

让自定义和结构体对象可以进行运算

注意：

1.条件运算需要成对实现

2.一个符号可以多个重载

3.不能使用ref和out

### 26.2 基本语法

```
public static 返回类型 operator 运算符
```

### 26.3 实例

```
class Point
{
	public int x;
	public int y;
	
	public static Point operator +(Point p1,Point p2)
	{
		Point p=new Point();
		p.x=p1.x+p2.x;
		p.y=p1.y+p2.y;
	}
}
class Program
{
	static void Main(string[] args)
	{
		Point p1=new Point();
		p1.x=1,p1.y=1;
		Point p2=new Point();
		p2.x=2,p2.y=2;
	}
}
```

## 27. 内部类与外部类

### 27.1 内部类

概念：在一个类中再申明一个类

特点：使用时要用包裹者点出自己

作用：亲密关系的变现

注意：访问修饰符的作用很大

```
class Person
{
	public class Body
	{
		public class Arm
		{
			
		}
		Arm leftArm;
		Arm rightArm;
	}
}
class Program
{
	static void Main(string[] args)
	{
		Person p=new Person;
		Person.Body body=new Person.Body;
		Person.Body.Arm;
	}
}
```

### 27.2 分部类

概念：把一个类分为几部分申明

关键字：partial

作用：分布描述一个类，增加程序的拓展性

注意：分布类可以写在多个脚本文件中，分布类访问修饰符要一致，分布类中不能有重复成员

```
partial class Student
{
	public bool sex;
	public string name;
}
partial class Student
{
	public int number;
}
class Program
{
	static void Main(string[] args)
	{
		Student s=new Student;
		s.number;
	}
}
```

### 27.3 分布方法

概念：将方法的申明和实现分离

特点：

1.不添加访问修饰符，默认私有

2.只能在分布类中申明

3.返回值只能是void

4.可以有参数但不用out关键字

## 28. 继承基础

### 28.1  基本概念

一个类A继承一个类B，类A会继承类B的所有成员和所有特征与行为。被继承的类被称为父类，继承的类被称为子类，子类可以有自己的特征和行为。

特点：

1.单根性：子类只能有一个父类

2.传递性：子类可以间接继承父类的父类

### 28.2 基本语法与实例

```
class Teacher
{
	public string name;
	public int number;
	public void SpeakName
	{
		Cosole.WriteLine(name);
	}
}
class TeachTeacher:Teacher
{
	public string subject;
	public void SpeakSubject()
	{
		Console.WriteLine(subject);
	}
}
class ChineseTeacher:TeachTeacher
{
	public void Skill()
	{
		Consile.WriteLine("aaa");
	}
}
class Program
{
	static void Main(string[] args)
	{
		TeachTeacher t=new TeachTeacher()
		{
			t.name="Hikari";
			t.number=114514;
			......
         }
	}
}
```

### 28.3 访问类型的影响

private无法直接在外部与子类直接使用

protected无法在外部访问

### 28.4 子类与父类的同名成员

可以存在但不建议使用

## 29. 里氏替换原则

### 29.1 基本概念

概念：任何父类出现的地方，子类都可以替代

重点：语法表现：父类容器装子类对象，因为子类对象包含了父类的所有内容

作用：方便对象存储和管理

### 29.2 基本实现

```
class GameObject
{

}
class Player:GameObject
{
	public void PlayerAtk()
	{
		Console.WriteLine("玩家攻击");
	}
}
class Monster:GameObject
{
	public void MonsterAtk()
	{
		Console.WriteLine("怪物攻击");
	}
}
class Boss:GameObject
{
	public void BossAtk()
	{
		Console.WriteLine("Boss攻击");
	}
}
class Program
{
	static void Main(string[] args)
	{
		Console.WriteLine("");
		//里氏替换原则：用父类容器装载子类对象
		GameObject player=new Player();
		GameObject monster=new Monster();
		GameObject boss=new Boss();
		
		GameObject[] objects=new GameObject[]{new Player(),new Monster(),new Boss()};
	}
}
```

### 29.3 is和as

基本概念：

is：判断一个对象是否为指定类对象，返回值为bool类型

```
if(player is Player)
{
	
}
else if(player is Monster)
{

}
```

as：将一个对象转换成指定类对象，返回值为指定类型对象或者null

```
Player p=player as Player
```

基本语法：

```
if(player is Player)
{
	Player p =player as Player;
	p.PlayerAtk();
	
	//(player as Player).PlayerAtk();
}
```

## 30. 继承中的构造函数

### 30.1  基本概念

语法：

```
访问修饰符 类名()
{
	
}
```

不写返回值，返回值与类名相同，访问修饰符根据需求来定，一般是public，构造函数可以重载，可以用this语法重用代码。

注意：

1.有参构造会顶掉默认的无参构造

2.如想保留无参构造须重载出来

特点：

当申明一个子类对象时，先执行父类的构造函数，再执行子类的构造函数

注意：

1.父类的无参构造很重要

2.子类可以通过base关键字代表父类调用父类构造

### 30.2 继承中构造函数的执行顺序

父类的父类构造->父类构造->子类构造

```
class GameObject
{
	public GameObject()
	{
		Console.WriteLine("GO的构造函数");
	}
}
class Player:GameObject
{
	public Player()
	{
		Console.WriteLine("P的构造函数");
	}
}
class MainPlayer:Player
{
	public MainPlayer()
	{
		Console.WriteLine("MP的构造函数");
	}
}
class Program
{
	static void Main(string[] args)
	{
		MainPlayer mp=new MainPlayer();
	}
}
```

### 30.3  父类无参构造函数重要

始终保持无参或调用base

```
class Father
{	//子类实例化时，默认自动调用的是父类的无参构造，所以如果父类无参构造被顶掉，会报错
	//public Father()
	//{
	
	//}
	public Father(int i)
    {
    	Console.WriteLine("Father");
    }
}
class Son:Father//会报错
```

### 30.4 通过base调用指定的父类构造

```
class Father
{	//子类实例化时，默认自动调用的是父类的无参构造，所以如果父类无参构造被顶掉，会报错
	//public Father()
	//{
	
	//}
	public Father(int i)
    {
    	Console.WriteLine("Father");
    }
}
class Son:Father
{
	public Son(int i):base(i)
	{
	
	}
	public Son(int i,string str):this(i)//调用public Son(int i):base(i)
	{
	
	}
}
```

## 31.万物之父与装箱拆箱

### 31.1  万物之父

关键字：object

概念：object是所有类型的父类，它是一个类（引用类型）

作用：

1.可以利用里氏替换原则，用object容器装所有对象

2.可以用来表示不确定的类型，作为函数参数类型

### 31.2  万物之父的使用

```
static void Main(string[] args)
{
	Father f=new Son();
	if(f is son)
	{
		(f as son).Speak;
	}
	//引用类型
	Object o=new Son();
	if(o is Son)
	{
		(o as Son).Speak;
	}
	//值类型
	object o2=1f;
	//强转
	float fl=(float)o2;
	//string类型
	object str="123123";
	string str2=str.ToString();
	string str3=str as string;
}
```

### 31.3 装箱拆箱

object存值类型（装箱）

object转值类型（拆箱）

装箱

把值类型用引用类型存储，代码会迁移到堆内存中

拆箱

把引用类型储存的值类型取出来，堆内存会迁移到栈内存里

好处：不确定类型可以进行参数的储存和传递

坏处：存在内存迁移，增加内存消耗

## 32. 密封类

### 32.1 基本概念

密封类使用sealed密封关键字修饰的类

作用：让类无法被继承

### 32.2 实例

```
sealed class Father
{

}
class Son:Father//报错
{
	
}
```

### 32.3 作用

在面向对象程序设计中，目的是为了子类不再被继承。

## 33. 多态Vob

### 33.1 多态的概念

让继承同一父类的子类们在执行相同方法是有不同的表现，主要目的是为了同一父类的对象执行相同方法有不同的表现，解决让同一个对象有唯一行为的特征

### 33.2 多态的实现

事实上，函数的重载是一种编译上的多态

运行上的多态：vob，抽象函数，接口

vob:

virtual(虚函数)

override(重写)

base(父类)

```
class GameObject
{
	public string name;
    public GameObject(string name)
    {
    	this.name=name;
    }
    public virtual void Atk()
    {
    	Console.WriteLine("攻击1");
    }
}
class Player:GameObject
{
	public Player(string name):base(name)
	{
		
	}
	public override void Atk()
	{
		//代表父类，可以通过base保留父类的行为
         //base.Atk();
         Console.WriteLine("攻击2");
	}
}
class Program
{
	static void Main(string[] args)
	{
		GameObject p=new Player("t");
		p.Atk()
	}
}
```

## 34. 抽象类与抽象函数

### 34.1 抽象类

被abstract修饰的类

特点：

1.不能被实例化

2.可以包含抽象方法

3.继承抽象类必须重写其抽象方法

```
abstract class Thing
{	//抽象类中限制较少
	public string name;
}
class Water:Thing
{
	
}
class Program
{
	static void Main(String[] args)
	{
		//里氏替换原则
		Thing t=new Water();
	}
}
```

### 34.2 抽象方法

用abstract修饰的方法

特点：

1.只能在抽象类中使用

2.没有方法体

3.不能是私有的

4.继承后必须用override重写实现

```
abstract class Fruits
{
	public string name;
	public abstract void Bad();
	//虚方法
	public virtual void Test()
	{
		//虚方法可以写
	}
}
class Apple:Fruits
{
	public ovverride void Bad()
	{
		......;
	}
	//虚方法可以不继承
}
```

## 35. 接口

### 35.1 接口的概念

一种自定义类型，关键字interface

接口申明的规范：

1.不包含成员变量

2.只包含方法，属性，索引器，事件

3.成员不能被实现

4.成员可以不用写访问修饰符，不能是私有的

5.接口不能继承类但是可以继承另一个接口

接口的使用规范：

1.类可以继承多个接口

2.类继承接口后要实现接口中的所有成员

特点：

它和类的申明类似，用来继承，不能被实例化但是可以作为容器储存对象

### 35.2 接口的申明

```
Interface 接口名
{
	//接口是整个抽象行为的基类	
}
Interface IFly
{
	public void Fly();
	string Name
	{
		get;
		set;
	}
	int this[int index]
	{
		get;
		set;
	}
	event Action doSomeThing; 
}
```

### 35.3 接口的使用

接口用于继承

1.类可以继承1个类，n个接口

2.继承接口后必须实现其中的内容，并且为public

3.实现的接口函数可以加virtual再在子类重写

4.接口遵循里氏替换原则

```
class Animal
{

}
class Human:Animal,IFly
{
	......
}
```

```
class Program
{
	IFly f=new Person();
}
```

### 35.4 接口与接口的关系

接口继承接口时不需要实现

待类继承接口类自己

```
Interface Iwalk
{
	void Walk();
}
Interface IMove:IWalk
{
......;
}
```

### 35.5 显示实现接口

当一个类继承了两个接口，但是接口中出现了同名方法

```
Interface IAtk()
{
	void Atk();
}
Interface ISuperAtk()
{
	void Atk();
}
class Player:IAtk,ISuperAtk
{
	void IAtk.Atk()
	{
		......;
	}
	void  ISuperAtk.Atk()
	{
		......;
	}
}
//使用时可以用里氏替换原则，as
```

## 36.面向对象七大原则

### 36.1 基本概念

面向对象编程（OOP）的七大原则是一组指导性的原则，旨在帮助开发者编写出更加灵活、可维护、可扩展的代码。这些原则并不是强制性的规则，但遵循它们可以显著提高软件的质量。以下是面向对象编程的七大原则：

1. 单一职责原则（Single Responsibility Principle, SRP）
   - 一个类应该仅有一个引起它变化的原因。这意味着一个类应该负责一组相对独立的功能。如果类承担的职责过多，就应该将其拆分成多个类。
2. 开闭原则（Open-Closed Principle, OCP）
   - 软件实体（类、模块、函数等）应该对扩展开放，对修改关闭。这意味着当需要添加新功能时，应该通过扩展已有代码（如添加子类）来实现，而不是修改现有代码。
3. 里氏替换原则（Liskov Substitution Principle, LSP）
   - 子类型必须能够替换掉它们的基类型。这要求子类型必须能够完全替代其父类型，而不会影响程序的正确性。
4. 接口隔离原则（Interface Segregation Principle, ISP）
   - 不应该强迫客户依赖于它们不使用的方法。这意味着接口应该尽量小，职责应该被细分，客户端应该只依赖它们需要的接口。
5. 依赖倒置原则（Dependency Inversion Principle, DIP）
   - 高层次的模块不应该依赖低层次的模块，它们都应该依赖其抽象；抽象不应该依赖细节；细节应该依赖抽象。这通常通过接口和抽象类来实现，以减少模块间的耦合。
6. 迪米特法则（Law of Demeter, LoD）
   - 也称为最少知识原则，一个对象应该对其他对象有尽可能少的了解。这要求一个类应该只与它的直接朋友（即其成员变量、方法参数、方法返回类型中的类）通信。
7. 组合/聚合复用原则（Composite/Aggregate Reuse Principle, CARP）
   - 尽量使用组合/聚合的方式，而不是使用继承来达到复用的目的。组合/聚合可以使系统更加灵活，因为组合关系具有比继承关系更弱的耦合性。

## 37. 密封方法

### 37.1 密封方法基本概念

用sealed 修饰的重写函数，让该抽象方法无法被继承重写，和override一起出现

### 37.2 实例

```
abstract class Animal
{
	public string name;
	public abstract void Eat();
	public virtual void Speak()
	{
		Console.WriteLine("a");
	}
}
class Person:Animal
{
	public sealed override void Eat()//不允许再继承
	{
	
	}
	public override void Speak()
	{
		
	}
	
}
class WhitePerson:Person
	{
	
	}
```

## 38.命名空间

### 38.1 命名空间的基本概念

命名空间是用来组织和重用代码，集合了在该命名空间的类

### 38.2 命名空间的使用

```
namespace 命名空间名
{
	类
}
namespace MyGame
{
	class GameObject
	{
		
	}
}
namespace MyGame
{
	class Player:GameObject
	{
		
	}
}
```

### 38.3 命名空间的相互引用使用

```
//@1 using MyGame;
namespace Lesson
{
	class Program
	{
		static void Main(string [] args)
		{
			//@2 MyGame.GameObject g =new MyGame.GameObject();
		}
	}
}
```

### 38.4 不同命名空间允许同名类

在不同命名空间中可以有同名类，

```
using MyGame1;
using MyGame2;
namespace MyGame1
{
	class GameObject
    {
    
    }
}
namespace MyGame2
{
	class GameObject
	{
	
	}
}
namespace Lesson
{
	class Program
	{
		static void Main(string [] args)
		{
			MyGame1.GameObject g =new MyGame1.GameObject();
			MyGame2.GameObject g =new MyGame2.GameObject();
		}
	}
}
```

### 38.5 命名空间可以包裹命名空间

```
using MyGame.UI
namespace MyGame
{
	namespace UI
	{
		class Image
		{
		
		}
	}
	namespace Game
	{
		class Image
		{
		
		}
	}
}
namespace Lesson
{
	class Program
	{
		static void Main(string [] args)
		{
			Image ima0=new Image();
			MyGame.UI.Image img=new MyGame.UI.image();
		}
	}
}
```

### 38.6 关于修饰类的访问修饰符

public:公有

internal:程序集/命名空间默认

abstract:抽象类

sealed:密封类

partial:分布类

## 39. 万物之父的方法

### 39.1 object静态方法

静态方法 Equals 判断两个对象是否相等 

最终的裁判权交由左侧对象的Equals方法

不管值类型引用类型都会按照左侧对象Equals方法的规则进行比较

```
Console.WriteLine(object.Equals(1,1));
>>True
Test t=new Test();
Test t2=new Test();
Console.WriteLine(object.Equals(t,t2));//判断内存地址
>>False
```

静态方法 ReferenceEquals 比较两个对象是否是相同的引用，主要是用来比较引用类型的对象

值类型对象返回值始终是false

```
Console.WriteLine(object.ReferenceEquals(t,t2));
```

### 39.2 object成员方法

普通方法GetType

该方法在反射有作用，主要作用时获取对象运行时的类型Type，结合反射的知识能够做一些操作

```
Test t=new Test();
Type type =t.GetType();
```

普通方法MemberwiseClone

该方法用于浅拷贝对象，意思是会返回一个新对象但是新对象的引用变量和老对象一致(只拷贝栈的)

```
class Test
{
	public int i=1;
	pubilc Test t2=new Test2();
	public test Clone
	{
		return MemberwiseClone() as Test;
	}
}
class Test2
{

}
class Program
{
	....
	Test t=new Test();
	Test t2 =t.Clone;
	
	Console.WriteLine(t.i);
	Console.WriteLine(t.t2.i);
	Console.WriteLine(t2.i);
	Console.WriteLine(t2.r2.i);
	
	t2.i=20;
	t2.t2.i=21;
	Console.WriteLine(t.i);
	Console.WriteLine(t.t2.i);
	Console.WriteLine(t2.i);
	Console.WriteLine(t2.r2.i);
}
>>
1
2
1
2

1
21
20
21
```

### 39.3 虚方法

1.虚方法Equals

相当于ReferenceEquals比较两个对象是否是相同的引用，主要是用来比较引用类型的对象，但在System.ValueType重写后可以比较值相等

2.虚方法GetHashCode

该方法是获取对象的哈希码（一种通过算法算出的，表示对象的唯一编码，不同对象的哈希码可能一样，具体情况具体分析），我们也可以重写该方法，定义自己的比较相等的规则

3.虚方法ToString

该方法用于返回当前对象代表的字符串，我们可以重写定义自己的对象转字符串规则

调用打印方法时，默认使用的是对象的ToString方法打印出来的内容

## 40. 结构体和类的区别

### 40.1 区别概述

最大的区别在于存储空间，结构体是值，类是引用。一个在栈上，一个在堆上。因此在调用和赋值上面有区别。

结构体和类在使用上类似，都可以来形容一类对象。但结构体具备封装特性，不具备继承和多态特性，因此使用次数会比类少很多，同时由于不具备继承特性，所以不能使用protected保护访问修饰符。

### 40.2 细节区别  

1.结构体不能指定初始值

2.结构体不能申明无参的构造函数

3.结构体申明有参构造函数后，无参不会被顶掉

4.结构体不能申明析构函数

5.结构体不能被static修饰

6.结构体要在构造函数初始化所有成员变量

7.结构体不能在自己内部申明跟自己一样的结构体变量

### 40.3 结构体特殊点

结构体可以继承接口，因为接口是行为抽象

### 40.4 选择

运用继承，多态用类：玩家，怪物

对象数据集合可以用结构体：坐标，位置

从值类型和引用类型上考虑

## 41 抽象类与接口的区别

### 41.1 相同点

1.都可以被继承

2.都不能直接实例化

3.都可以包含方法申明

4.子类必须是未实现的方法

5.都遵循里氏替换原则

### 41.2 区别

1.抽象类中可以有构造函数，接口中不能

2.抽象类只能被单一继承，接口可以被继承多个

3.抽象类中可以有成员变量，接口中不能

4.抽象类可以申明成员方法，虚方法，抽象方法，静态方法，接口只能申明没有实现的抽象方法

5.抽象类方法可以使用访问修饰符，接口建议不写，默认public

### 41.3 选择

表示对象用接口，表示行为拓展的用接口

## 42.string

### 42.1  字符串指定位置

字符串的本质是char数组

```
string str="aa";
Console.WriteLine(str[0]);
char[] chars=str.ToCharArray();
Console.WriteLine(chars[1]);
for(int i=0;i<str.Length;i++)
{
	Console.WriteLine(str[i]);
}
```

### 42.2 字符串拼接

```
str=string.Format("{0}{1}",1,333);
Console.WriteLine(str);
>>
1333
```

### 42.3 正向查找字符位置

```
str="Hikari";
int index=str.IndexOf("H");
Console.WriteLine(index);
int index2=str.IndexOf("O");
Console.WriteLine(index2);
>>
0
-1
```

### 42.4 反向查找字符串位置

```
str="HikariHikari";
index=str.LastIndexOf("Hikari");
Console.WriteLine(index);
>>
5
```

### 42.5 移除指定位置的字符

```
str="Hikari";
str=str.Remove(4);//要用字符串接收,因为返回新字符串
Console.WriteLine(str);
>>
Hika

str="Hikari";
str=str.Remove(1,1);
Console.WriteLine(str);
>>
Hkari
```

### 42.6 替换指定字符串

```
str="Hikari";
str=str.Replace("H","h");
Console.WriteLine(str);
>>
hikari
```

### 42.7 大小写转换

```
str="Hikari";
str=str.ToUpper();
Console.WriteLine(str);
>>
HIKARI
str=str.ToLower();
>>
hikari
```

### 42.8 字符串截取

```
str="Hiakri";
str=str.Substring(2);
Console.WriteLine(str);
>>
akri

str="Hiakri";
str=str.Substring(2,3);
Console.WriteLine(str);
>>
akr
```

### 42.9 字符串切割

```
str="1,2,3,4,5,6,7,8"
string[] strs=str.Split(',');
for(int i=0;i<str.Length;i++)
{
	Console.WriteLine(strs[i]);
}
>>
1
2
3
4
5
6
7
8
```

## 43. stringbuilder

### 43.1 概念

用于处理字符串的公共类。修改字符串而不创建新的对象，用于提升性能（不过早GC）。引用System.Text

```
初始化 直接指明内容
StringBuilder str=new StringBuilder("123123");
Console.WriteLine(str);
>>
123123
```

### 43.2 扩容

StringBuilder会自动扩容

提升性能的原理类似于预处理

```
Console.WriteLine(str.Capacity);
>>
16
```

```
StringBuilder str=new StringBuilder("123123",100);//一百个房间
```

### 43.3 增删改查

```
//增
str.Append("4444");
Console.WriteLine(str);
Console.WriteLine(str.Length);
Console.WriteLine(str.Capacity);

str.AppendFormat("{0}{1}",100,999);
Console.WriteLine(str);
Console.WriteLine(str.Length);
Console.WriteLine(str.Capacity);
//插
str.Insert(0,"Hikari");
Console.WriteLine(str);
//删
str.Remove(0,10);
Console.WriteLine(str);
//清
str.Clear();
Console.WriteLine(str);
//查
Console.WriteLine(str[0]);
//改
str[0]='A';
Console.WriteLine(str);
//换
str.Replace("i","H");//i->H

```

## 44. ArrayList

### 44.1  ArrayList本质

ArrayList是一个C#封装好的类，本质是object类型的数组，ArrayList类帮助实现了很多方法比如数组的增删查改

### 44.2 申明

```
using System.Collecttions;
ArrayList array=new ArrayList();
```

### 44.3 增删查改

```
增
array.Add(1);
array.Add("string");
array.Add(true);
array(new object());

//批量增加
ArrayList array2=new ArrayList();
array2.Add(123);
array.Addrange(array2);

删
//指定元素从头找
array.Remove(1);
//移除指定位置元素
array.ReoveAt(0);
//清空
array.Clear();

查
//得到指定元素
Console.WriteLine(array[0]);
//判断元素是否存在
if(array.Contains("123"))
{
	.......
}
//正向查找元素位置(如果-1代表不存在)
int index=array.IndexOf(true);
Console.WriteLine(index);
//反向查找元素位置
index=array.LastIndexOf(true);

改
array[0]="999";
Console.WriteLine(array[0]);
```

### 44.4 遍历

```
//长度
Console.WriteLine(array.Count);
//容量
Console.WriteLine(array.Capacity);
//遍历
for(int i=0;i<array.Count;i++)
{
	Console.WriteLine(array[i]);
}
//迭代器
foreach (object item in array)
{
	Console.WriteLine(item);
}
```

### 44.5 装箱拆箱

值类型储存是在装箱，值类型对象转换使用就是在拆箱

```
int i=1;
array[0]=i;//装箱
i=(int)array[0];//拆箱
```

## 45. Stack

### 45.1 Stack本质

一种封装好的类，本质是object数组，遵循先进后出的规则

### 45.2 申明

```
using System.Collection;
Stack s=new Stack();
```

### 45.3 增取查改

```
增
//压栈
stack.push(1);
stack.push("123");
stack.push(true);

取
//弹栈
object v=stack.Pop();
Console.WriteLine(v);

v=stack.Pop();
Console.WriteLine(v);

查
//只能查看栈顶
v=stack.Peek();
Console.WriteLine(v);

v=stack.Peek();
Console.WriteLine(v);
//查看元素是否存在于栈中
if(stack.Contain(1.2f))
{
	Console.WriteLine("a");
}

改
//清空
stack.Clear();
```

### 45.4 遍历

```
//长度
Console.WriteLine(stack.Count);


//foreach
foreach(object item in stack)
{
	......;
}

//转换成object
object [] array=stack.ToArray();
for(int i=0;i<array.Length;i++)
{
	......;
}

//循环弹栈
while(stack.Count>0)
{
	object o=stack.Pop();
	Console.WriteLine(o);
}
```

### 45.5 装箱拆箱

值类型储存是在装箱，值类型对象转换使用就是在拆箱

## 46 Queue

### 46.1 Queue本质

一种封装好的类，本质是object数组，遵循先进先出的规则

### 46.2 申明

```
using System.Collection;
Queue queue=new Queue();
```

### 46.3 增取查改

```
增
queue.Enqueue();
取
object v=queue.Dequeue();
查
v=queue.Peek();

if(queue.Contain(1.2f))
{
	Console.WriteLine("a");
}
改
//清空
queue.Clear();
```

### 46.4 遍历

```
//长度
Console.WriteLine(queue.Count);
//foreach
foreach(object item in queue)
{
	Console.WriteLine(item);
}
//转数组
object [] array=queue.ToArray();
for(int i=0;i<array.Length;i++)
{
	......;
}

//循环出列
while(stack.Count>0)
{
	object o=queue.Dequeue();
	Console.WriteLine(o);
}
```

### 46.5 装箱拆箱

值类型储存是在装箱，值类型对象转换使用就是在拆箱

## 47. Hashtable

### 47.1 Hashtable的本质

基于键的哈希代码组织起来的 键/值对

主要作用是提高数据查询效率

使用键来访问集合中的元素

### 47.2 申明

```
using System.Collection;
Hashtable hashtable=new Hashtable();
```

### 47.3 增删查改

```
增
hashtable.Add(1,"2333");
//不能出现相同的键

删
//通过键来删除
hashtable.Remove(1);
//删除不存在的键，不反应
hashtable.Remove(2);
//清除
hashtable.Clear();

查
//通过建查看值，找不到会返回空
Console.WriteLine(hashtable[1]);
//根据键看是否存在
if(hashtable.Contains("2"))
{
	......;
}
if(hashtable.ContainsKey("2"))
{
	......;
}
//根据值去检测
if(hashtable.ContainsValue(12))
{
	......;
}

改
//只能修改值对应的内容
hashtable[1]=100;
```

### 47.4 遍历

```
//得到键值对数
Console.WriteLine(hashtable.Count);

//遍历所有键
foreach(object item in hashtable.Keys)
{
	Console.WriteLine(item);//键
	Console.WriteLine(hashtable[item]);//值
}
//遍历所有值
foreach(object item in hashtable.Values)
{
	Console.WriteLine(item);//值
}
//键值对一起遍历
foreach(DictionaryEntry item in hashtable)
{
	Console.WriteLine(item.Key+item.Value);
}
//迭代器遍历
IDictionaryEnumerator myEnumerator=hashtable.GetEunmerator();
bool flag=myEnumerator.MoveNext();
while(flag)
{
	Console.WriteLine(myEnumerator.Key+myEnumerator.Value);
	flag=myEnumerator.MoveNext();
}
```

## 48. 泛型

### 48.1 泛型的概念

实现类型参数化，达到代码重用的目的，通过类型参数化实现同一份代码上操作多种类型

泛型相当于类型占位符

定义类或方法时再具体指定类型

### 48.2 泛型分类

泛型类：

```
class 类名<泛型占位字母>
```

泛型接口：

```
interface 接口名<泛型占位字母>
```

泛型函数：

```
函数名<泛型占位字母>(参数列表)
```

### 48.3 泛型类和接口

```
class TestClass<T>
{
	public T value;
}
class Program
{
	static void Main(string[] args)
	{
		TestClass<int> t=new TestClass<int>();
		t.value=10;
		
		TestClass<string> t2=new TestClass<string>();
		t2.value="123123";
	}
}


interface TestInterface<T>
{
	T Value
	{
		get;
		set;
	}
	class Test:TestInterface<int>
	{
		.......
	}
}
```

### 48.5 泛型方法

```
//普通类的泛型方法
class Test2
{
	public void TestFun<T>(T value)
	{
		Console.WriteLine(value);
	}
	public void TestFun<T>()
	{
		T t=default(T);//默认值
	}
	public T TestFun<T>(string v)
	{
		return default(T);
	}
}

//泛型类的泛型方法
class Test2<T>
{
	public T value;
	
	//不是泛型方法，仅仅是使用这个泛型，不能动态变化
	public void TestFun(T t)
	{
		......;
	}
	//泛型函数
	public void TestFun<K>(K k)
	{
		......;
	}
}

class Program
{
	static void Main(string[] args)
	{
		Test2 t2=new Test2();
		t2.TestFun<string>("1234");
		
		Test2<int> tt2 =new Test2<int>();
		tt2.TestFun<string>("123");
	}
}


```

## 49. 泛型约束

### 49.1 概念

 让泛型的类型有一定的限制：where

|      值类型      |     where 泛型字母:struct     |
| :--------------: | :---------------------------: |
|     引用类型     |     where 泛型字母:class      |
| 无参公共构造函数 |      where 泛型字母:new       |
|   类或者派生类   |      where 泛型字母:类名      |
| 接口及其派生类型 |     where 泛型字母:接口名     |
| 泛型及其派生类型 | where 泛型字母:另一个泛型字母 |

### 49.2 各泛型约束的讲解

```
值类型约束
class Test1<T> where T:struct
{
	public T value;
	public void TestFun<K>(K k)where K:struct
	{
		
	}
}
class Program
{
	static void Main(string[] args)
	{
		Test1<int> t1=new Test1<int>();
	}
}

引用类型约束
class Test2<T> where T:class
{
	public T value;
	public void TestFun<K>(K k)where K:class
	{
		
	}
}
class Program
{
	static void Main(string[] args)
	{
		Test2<Random> t2=new Test2<Random>();
	}
}

无参公共构造函数约束
class Test3<T> where T:new()
{
	public T value;
	public void TestFun<K>(K k)where K:new
	{
		
	}
	class Test1
	{
	
	}
	class Test2
	{
		public Test2(int a)
		{
			
		}
	}
}
class Program
{
	static void Main(string[] args)
	{
		Test3<Test1> t3=new Test3<Test1>();
	}
}

类或派生类
class Test4<T> where T:Test1
{
	public T value;
	public void TestFun(K k)where K:Test1
	{
		class Test1
		{
	
		}
		class Test2:Test1
		{
		
		}
	}
}
class Program
{
	static void Main(string[] args)
	{
		Test4<Test1> t4=new Test4<Test1>();
		Test4<Test2> t4=new Test4<Test2>();
	}
}

接口及派生类型
Interface IFly
{

}
class Test5<T> where T:Ifly
{
	public T value;
	public void TestFun<K>(K k)where K:IFly
	{
		
	}
}
class Program
{
	static void Main(string[] args)
	{
		Test5<IFly> t5=new Test5<IFly>();
		t5.value=new Test5();
	}
}

另一个泛型类及派生类型
class Test6<T,U> where T:U
{
	public T value;
	public void TestFun<K,V>(K k)where K:V
	{
		
	}
}
class Program
{
	static void Main(string[] args)
	{
		Test5<Test4,IFly> t5=new Test5<Test4,IFly>();
	}
}
```

### 49.3 组合使用

```
class Test7<T> Where T:class,new()
{
	
}
```

### 49.4 多个泛型约束

```
class Test8<T,K> where T:class,new() where K:struct
{

}
```

## 50. List

### 50.1 List本质

可变类型的泛型数组

### 50.2 申明

```
using System.Collections.Generic
class Program
{
	static void Main(string[] args)
	{
		List<int> list=new List<int>
	}
}
```

### 50.3 增删查改

```
增
list.Add(1);
........
List<string> listStr=new List<string>();
list.AddRange(listStr);

删
list.Remove(1);
list.RemoveAt(0);
list.Clear();

查
Console.WriteLine(list[1]);
是否存在
if(list.Contains(1))
{
	.......
}
正向查找
int index=list.IndexOf(2);
Console.WriteLine(index);
反向查找
int index=list.LastIndexOf(2);
Console.WriteLine(index);

改
Console.WriteLine(list[0]);
list[0]=99;
Console.WriteLine(list[0]);
```

### 50.4 遍历

```
//长度
Console.WriteLine(list.Count);
//容量
Console.WriteLine(list.Capacity);

for(int i=0;i<list.Count;i++)
{
	.......;
}

foreach(int item in list)
{
	......;
}
```

## 51. Dictionary

### 51.1 本质

拥有泛型的Hashtable

### 51.2 申明

```
using System.Collections.Generic
Dictionary<int,string> dic=new Dictionary<int,string>();
```

### 51.3 增删查改

```
增
dic.Add(1,"233");

删
//键删除
dic.Remove(1);
dic.Remove(5);//未反应
//清除
dic.Clear();

查
//键查
找不到直接报错
Console.WriteLine(dic[1]);
//存在
键检测
if(dic.ContainKey(1))
{
	......;
}
值检测
if(dic.ComntainValue("223"))
{
	......;
}

改
dic[1]="555";
```

### 51.4 遍历

```
Console.WriteLine(dic.Count);
```

1.遍历所有键

```
foreach(int item in dic.Key)
{
	Console.WriteLine(item);
	Console.WriteLine(dic[item]);
}
```

2.遍历所有值

```
foreach(string item in dic.Values)
{
	Console.WriteLine(item);
}
```

3.遍历键值对

```
foreach(KeyValuePair<int,string> item in dic)
{
	Console.WriteLine(item.Key+item.Value);
}
```

## 52. 顺序存储与链式存储

### 52.1 数据结构

指存在一种或多种特定关系的数据元素的集合

常用数据结构：数组，栈，队列，链表，树，图，堆，散列表

### 52.2 线性表

线性表是一种数据结构，比如数组,ArrayList,Stack,Queue

### 52.3 顺序存储

用一组地址连续的储存单元依次存储线性表的各个数据元素

数组,ArrayList,Stack,Queue都是顺序存储，但组织规则不一样

### 52.4 链式存储

用一组任意的储存单元存储线性表的各个数据元素

单向链表，双向链表，循环链表都是链式存储

### 52.5 单向链表的实现

```
class LinkedNode<T>
{
	public T value;
	public LinkedNode<T> nextNode; 
	public LinkedNode(T value)
	{
		this.value=value;
	}
}
class Program
{
	static void Main(string[] args)
	{
		LinkedNode<int> node=new LinkedNode<int>();
	}
}
class LindedList<T>
{
	public LinkedNode<T> head;
	public LinkedNode<T> last;
	
	public void Add(T value)
	{
		LinkedNode<T> node =new LinkedNode<T>(Value)
		{
			if(head==null)
			{
				head=node;
				last=node;
			}
			else
			{
				last.nextNode=node;
				last=node;
			}
		}
	}
	
	public void Remove(T value)
	{
		if(head==null)
		{
			return;
		}
		if(head.value.Equals(value))
		{
			head=head.nextNode;
			if(head==null)
			{
				last==null;
			}
			return;
		}
		linkedNode<T> node=head;
		while(node.nextNode!=null)
		{
			if(node.nextNode.value.Equals(value))
			{
				node=node.nextNode;
				node.nextNode=node.nextNode.nextNode;
				break;
			}
		}
	}
}
```

### 52.6 顺序存储与链式存储的优缺点

增删：链式优于顺序

查改：顺序优于链式

## 53. 委托

### 53.1 委托是什么

委托是函数的容器，用于存储和传递函数，其本质是一个类，用来定义函数的类型，不同的函数必须对应各自格式一致的委托

### 53.2 基本语法

关键字：delegate

语法：访问修饰符 delegate 返回值 委托名（参数列表）

可以申明在namespace和class语句块中，更多的写在namespace里

### 53.3 定义自定义委托

访问修饰符不写，为public 在别的命名空间也能使用

private 其他命名空间不能使用

一般使用public

```
申明规则：
delegate void MyFun();
delegate void MyFun2()；
委托申明在同一语句块中不能重名
```

### 53.4 使用委托

```
class Program
{
	static void Main(string[] args)
	{
		MyFun f =new MyFun(Fun);
		//专门用来装载函数的容器
		f.Invoke();
		
		MyFun f2=Fun;
		f2();
		
		MyFun2=Fun3;
		f3(10);
		
		Test t=new Test();
		t.TestFun(Fun,Fun2)
	}
	static void Fun()
	{
		Console.WriteLine("123");
		Console.WriteLine("456");
	}
	static void Fun2(int value)
	{
		Console.WriteLine(value);
	}
}




class Test
{
	public MyFun fun;
	public MyFun2 fun2;
	
	public void TestFun(MyFun fun,MyFun2 fun2)
	{
		//先处理一些逻辑，再执行传入的函数
		fun();
		fun2(2);
	}
}
```

### 53.5 多播委托

委托变量可以存储多个函数

```
//批量处理函数
MyFun ff=Fun;
ff+=Fun;
ff();

增
public void AddFun(MyFun fun,MyFun2 fun2)
{
	this.fun+=fun;
	this.fun2+=fun2;
}
.....
t.AddFun(Fun,Fun2);
t.fun();
t.fun2(1);

删
public void RemoveFun(MyFun fun,MyFun fun2)
{
	this.fun-=fun;
	this.fun2-=fun2;
}
```

### 53.6 系统定义好的委托

```
using System;
public Action action;
Action action=Fun;
action+=Fun3;


Func<string> funcString=Fun4;//有返回值
Func<int> funcint =Fun5;
public string Fun4()
{
	return"";
}
public int Fun5()
{
	......;
}
//委托支持泛型，可以是返回值和参数可变
delegate T MyFun3<T,K>(T t,K k);

//系统提供1到16个参数委托
Action<int,string> action=Fun6;//无返回值
public void Fun6(int 1,string s)
{
	
}

Func<int(传入) int(输出)>func2=Fun2 (一个参数);
```

## 54. 事件

### 54.1 事件是什么

事件基于委托存在，是委托的安全包裹，让委托使用更有安全性

### 54.2  事件怎么使用

申明语法：

访问修饰符 event 委托类型 事件名;

使用：

作为成员变量存在于类中

委托怎么用，事件就怎么用

注意：

只能作为参与成员存在于类、接口和结构体中

事件与委托的区别：

不能在类外部赋值和调用

```
class Test
{
	//委托成员变量 用于存储函数的
	public Action myFun;
	//事件成员变量 用于存储函数的
	public event Action myEvent;
	
	public Test()
	{
		myFun=TestFun;
		myFun+=TestFun();
		
		myEvent=TestFun();
		myEvent+=TestFun();
	}
	public void TestFun()
	{
		Console.WriteLine("123");
		Test t=new Test();
	}
}
```

### 54.3 为什么有事件

1.防止外部随意置空委托

2.防止外部随意调用委托

3.事件相当于给委托做封装

```
class Program
{
	static void Main(string[] args)
	{
		Console.WriteLine("extend");
		Test t =new Test();
		//委托可以在外部赋值
		t.myFun=null;
		t.myFun=TestFun;
		//事件不可以在外部赋值，虽然不能直接赋值，但是可以添加移除记录的函数
		t.myEvent+=TestFun;
		
		//委托可以在外部调用
		t.myFun();
		t.myFun.Invoke();
		//事件不能在外边调用，只能在类的内部封装调用
		t.DoEvent();
		
		Action a =TestFun;
		//事件不能作为历史变量在函数中使用
	}
	public void DoEvent
	{
		if(myEvent!=null)
		{
			myEvent();
		}
	}
}
```

## 55. 协变逆变

### 55.1 什么是协变逆变

协变：和谐自然的变化，由小范围变成大范围、高级变低级，如：string变为object，父类变子类

逆变：不和谐自然的变化，由大范围变成小范围、低级变高级，如：object变为string，子类变父类

协变和逆变主要用于修饰泛型，用于修饰泛型字母，只有泛型接口和泛型委托能使用

协变：out

逆变：in

### 55.2 作用

1.返回值和参数

用out申明的泛型，只能修饰返回值

```
delegate T TestOut<out t>();
```

用in修饰的泛型，只能用作参数

```
delegate void TestIn<in T>(T t);
```

2.里氏替换原则

```
class Father
{
	
}
class Son:Father
{
	
}
class Program
{
	static void Main()
	{
		//协变：
		TestOut<Son> os=()=>
		{
			return new Son();
		};
		TestOut<Father> of=os;
		Father f=of();//返回Son
		
		
		//逆变
		TestIn<Father> iF=(value)=>
		{
			
		};
		TestIN<Son> is=iF();
		is (new Son())//调用Father
	}
}
```

## 56.多线程

### 56.1 进程

进程是计算机程序关于某数据集合上的一次运行活动，是系统进行资源分配和调度的基本单位，是操作系统的基础

进程之间可以相互独立运行，互不干扰，同时也能相互访问操作

### 56.2 线程

线程是操作系统能够调动运算的最小单位，它被包含于进程中，是进程的实际运作单位

一条线程是指进程中的单一顺序控制流，一个进程中可以并发多个线程

可以理解为一条从上到下运行的管道

### 56.3 多线程

通过代码开启新的线程，同时运行多个线程就叫多线程

### 56.4 多线程语法

线程类 Thread

命名空间 using System.Threading;

```

class Program
{
	static bool isRuning=true;
	static void Main(string[] args)
	{
		//申明线程
		Thread t =new Thread(NewThreadLogic);
		//开启线程
		t.Start();
		//后台线程
		t.IsBackground=true;
		//关闭一个线程
			//bool标识
			Console.ReadKey();//检测
			isRuning=false;
			Console.ReadKey();//检测
			//线程提供方法(.Net core不能使用)
			t.Abort();
			t=null;
	}
	static void NewThreadLogic()
	{
		while(isRuning)
		{
			//线程休眠
			Thread.Sleep();//休眠多少毫秒，在哪个线程就休眠哪个
        	 Console.WriteLine("aaa");
		}
	}
}
		
```

### 56.5 线程之间共享程序

多个线程使用的内存是共享的，都属于应用程序

所以，当多线程同时操作同一片区域时可能会出现问题

可以通过加锁来避免问题

```
lock(引用类型对象)
当多个线程想访问同样的东西进行逻辑处理时，为避免不必要的逻辑执行的查错

static Object obj=new Object()
lock(obj)
{	
	......
}
```

### 56.6 多线程意义

专门处理复杂逻辑
