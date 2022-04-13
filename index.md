内建的函数对象，逻辑仿函数

1，逻辑非logical_not

利用逻辑非，将容器搬运到容器v2中，并执行取反操作

利用resize对空间及逆行扩展

```
transform（v.begin(),v.end(),v2.begin(),v2.end(),logical_not<bool>）
```

```
#include<iostream>
#include<functional>
#include<algorithm>
#include<vector>
using namespace std;
void test01()
{
	vector <bool>v1;
	v1.push_back(true);
	v1.push_back(false);
	v1.push_back(true);
	v1.push_back(false);

	for (vector<bool>::iterator it = v1.begin(); it != v1.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;

	vector<bool>v2;
	v2.resize(v1.size());

	transform(v1.begin(),v1.end(),v2.begin(), logical_not<bool>());
	for (vector<bool>::iterator it = v2.begin(); it != v2.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}
int main()
{
	test01();
	system("pause");
	return 0;
}
```

## **STL**常见算法

算法主要有algorithm,functional,numeric等组成

algorirhm是所有	STL容器中最大的一个，它涉及到比较，交换，查找，遍历操作，赋值修改等

numeric体积很小，只包括几个序列上卖弄简单的数学运算模板

functional类定义了一些模板类用于声明函数对象



### 常用的遍历算法

#### for_each//遍历容器

```
for_each(v.begin(),v.end(),print01)//仿函数print02  普通函数print01
```

带不带括号取决于本体

```
#include<iostream>
#include<functional>
#include<algorithm>
#include<vector>
using namespace std;
void print01(int val) {//普通函数
	cout << val << " ";
}
class print02//仿函数
{
public:
	void operator()(int val)
	{
		cout << val << " ";
	}
};
void test01()
{
	vector<int>v;
	for (int i = 0; i < 10; i++)
	{
		v.push_back(i);
	}
	for_each(v.begin(), v.end(),print02());
}
int main()
{
	test01();
	system("pause");
	return 0;
}
```

#### transform 功能：搬运容器到另一个容器中

原容器开始迭代，原容器截至迭代，现容器开始迭代，函数

### 常用的查找算法

#### find 

查找指定元素，返回指定元素的迭代器，找不到返回结束迭代器end()

函数原型:

```
find(iterator beg,iterator end,value)
```

开始迭代器，结束迭代器，查找的元素

```
#include<iostream>
#include<functional>
#include<algorithm>
#include<vector>
#include<string>
using namespace std;
class Person
{
public:
	Person(string name, int age)
	{
		this->m_name=name;
		this->m_age=age;
	}
	bool operator==(const Person &p)
	{
		if (this->m_name == p.m_name && this->m_age ==p.m_age)
		{
			return true;
		}
		return false;
	}
	string m_name;
	int m_age;
};
void test02()
{
	vector<Person>v1;
	Person p1("aaa", 10);
	Person p2("bbb", 20);
	Person p3("ccc", 30);
	Person p4("ddd", 40);

	v1.push_back(p1);
	v1.push_back(p2);
	v1.push_back(p3);
	v1.push_back(p4);

	Person pp("bbb",20);

	vector<Person>::iterator it= find(v1.begin(), v1.end(), pp);
	if (it == v1.end())
	{
		cout << "没有找到！" << endl;
	}
	else
	{
		cout << "找到： " << it->m_name<<"年龄： "<<it->m_age << endl;
	}
}
void test01()
{
	vector<int>v;
	for (int i = 0; i < 10; i++)
	{
		v.push_back(i);
	}
	vector<int>::iterator it=find(v.begin(), v.end(), 5);
	if (it == v.end())
	{
		cout << "没有找到！" << endl;
	}
	else
	{
		cout << "找到： "<<*it << endl;
	}
}
int main()
{
	test02();
	system("pause");
	return 0;
}
```

#### find_if

按条件查找函数

按值查找元素，找到返回指定位置迭代器，找不到返回结束迭代器位置

三个位置的信息分别是：

开始迭代器，结束迭代器，函数或者谓词

### adjacent_find

#### binary_search
