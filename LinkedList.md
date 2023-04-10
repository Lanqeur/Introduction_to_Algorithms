# 链表
链表可以看作是用指针串起来的数组，它用一串任意位置存储单元存放线性表的数据元素，这些存储单元可以看作是连续的，也可以是不连续的。
链表有两种：
* 单向链表。其指针是单向的，只能从左向右遍历数据，为了方便从任何一个位置出发都能遍历整个链表，所以让其首尾相接，尾巴tail的next指针指向头部head的data。由于首尾相接的链表是循环的，所以任意结点都可以成为头和尾。
* 双向链表。每个结点有两个指针，pre指针指向前一个结点，next指针指向后一个结点。双向链表也是首尾相连的，最后一个结点的next指针指向第一个结点，第一个结点的pre指针指向最后一个结点。

在需要频繁访问前后结点的场景，最好使用双向链表，例如删除一个结点now的操作。
链表的主要操作有：
* 初始化
* 添加
* 遍历
* 插入
* 删除
* 查找
* 释放

链表的缺点是查找慢，例如查找data等于某个值的结点时，需要遍历整个链表才能找到它。
## C++链表实现
链表的编程实现有动态链表、静态链表、STL lst等多种方法，算法竞赛中通常采用静态链表或STLlist加快编程速度。
### 单向静态链表
静态链表使用一个数组来模拟链表。
1. 链表结点的定义
用Struct node定义一个链表，data表示结点存储的数据，next指向下一个结点的编号。
2. 链表初始化
直接用i来赋值node[i]，并且注意最后一个结点的next指向第一个结点：```nodes[n].next=1;```
3. 遍历链表
沿着next指针访问所有结点。
4. 删除结点
若当前结点是now，要删除now必须先找到前一个结点pre，然后跳过now，即```nodes[pre].next=nodes[now].next```。如何找到pre是单向链表的难点。
5. 插入结点
由于是使用数组模拟链表的，因此插入一个结点只能把数组末尾还没用到的新nodes[]赋值给新结点。

用静态数组模拟链表的缺点是，若有频繁的删除和插入操作，会逐渐耗尽数组空间，因为删除的结点不方便回收利用。双向链表也有这样的缺点。
### 双向静态链表
双向静态链表相比单向静态链表只增加了一个指向前一个结点的指针pre，这样删除结点的操作就很容易实现。同时初始化要注意：
```C++
nodes[n].next=1;
nodes[1].pre=n;
```
### STL list
使用C++的STL list就不用自己管理链表了。
STL list是双向链表，通过指针访问结点数据，使用它可以高效的删除和插入结点。
```C++
list<int> node;
//定义一个存储int类型数据的链表
for(int i=0;i<n;i++)
node.push_back(i);
//为链表赋值
list<int>::iterator it=node.begin();
while(node.size()>0)
{
    it++;
    if(it==node.end())//循环链表，end()是list末端下一个位置，指向一个不存在的元素
    it=node.begin();
}
//用it遍历链表，例如从头遍历到尾
list<int>::iterator next=++it;
if(next==node.end())next=node.begin();//循环链表
node.erase(--it);
it=next;
//删除一个结点
```
### 实现 list 容器删除元素的成员函数
|成员函数|功能|
|-|-|
|pop_front()|删除位于 list 容器头部的一个元素|
|pop_back()|删除位于 list 容器尾部的一个元素|
erase()|该成员函数既可以删除 list 容器中指定位置处的元素，也可以删除容器中某个区域内的多个元素|
clear()|删除 list 容器存储的所有元素|
remove(val)|删除容器中所有等于 val 的元素|
unique()|删除容器中相邻的重复元素，只保留一份|
remove_if()|删除容器中满足条件的元素|
#### pop_front()、pop_back()、clear()
这三个函数不接受参数，返回值为void，执行固定的操作。
#### erase()
erase() 成员函数有以下 2 种语法格式：
```C++
iterator erase (iterator position);
iterator erase (iterator first, iterator last);
```
* 利用第一种语法格式，可实现删除 list 容器中 position 迭代器所指位置处的元素；
* 利用第二种语法格式，可实现删除 list 容器中 first 迭代器和 last 迭代器限定区域内的所有元素（包括 first 指向的元素，但不包括 last 指向的元素）。
#### remove(val)
erase() 成员函数是按照被删除元素所在的位置来执行删除操作，如果想根据元素的值来执行删除操作，可以使用 remove() 成员函数。
#### unique()
unique() 函数也有以下 2 种语法格式：
```C++
void unique()
void unique（BinaryPredicate）//传入一个二元谓词函数
```
以上 2 种格式都能实现去除 list 容器中相邻重复的元素，仅保留一份。但第 2 种格式的优势在于，我们能自定义去重的规则。
```C++
#include <iostream>
#include <list>
using namespace std;
//二元谓词函数
bool demo(double first, double second)
{
    return (int(first) == int(second));
}
int main()
{
    list<double> mylist{ 1,1.2,1.2,3,4,4.5,4.6 };
    //删除相邻重复的元素，仅保留一份
    mylist.unique();//{1, 1.2, 3, 4, 4.5, 4.6}
    for (auto it = mylist.begin(); it != mylist.end(); ++it)
        cout << *it << ' ';
    cout << endl;
    //demo 为二元谓词函数，是我们自定义的去重规则
    mylist.unique(demo);
    for (auto it = mylist.begin(); it != mylist.end(); ++it)
        std::cout << *it << ' ';
    return 0;
}
```
执行结果为：
```
1 1.2 3 4 4.5 4.6
1 3 4
```
注意，除了以上一定谓词函数的方式，还可以使用 lamba表达式以及函数对象的方式定义。

可以看到，通过调用无参的 unique()，仅能删除相邻重复（也就是相等）的元素，而通过我们自定义去重的规则，可以更好的满足在不同场景下去重的需求。
#### remove_if()
除此之外，通过将自定义的谓词函数（不限定参数个数）传给 remove_if() 成员函数，list 容器中能使谓词函数成立的元素都会被删除。
[STL list详解](http://c.biancheng.net/view/6892.html)
