# 栈
栈的特点是先进后出，只有唯一的一个出入口，元素既从这个口进入，又从这个口出来，这是栈与队列最大的区别，队列有两个口，一个入口，一个出口。
栈的常见操作如下：
* empty():返回栈是否为空；
* size():返回栈的长度；
* top():查看栈顶元素；
* push():向栈顶添加元素；
* pop():删除栈顶元素。
## C++的栈实现
### 手写栈
```C++
const int N=100100;//定义栈的大小
struct mystack
{
    int a[N];//存放栈元素
    int t=0;//栈顶位置
    void push(int x){a[t++]=x;}//入栈
    int top(){return a[t-1];}//读栈顶元素，不弹出
    void pop(){t--;}//弹出栈顶元素
    int empty(){return t==0;}
};
```
### STL stack
有关操作如下：
* stack< Type>s:定义栈，Type为数据类型；
* s.push(item):把item放入栈顶；
* s.top():返回栈顶元素，但不将其删除；
* s.pop():删除栈顶元素，但不会返回；
* s.size():返回栈中元素的个数；
* s.empty():检查栈是否为空。