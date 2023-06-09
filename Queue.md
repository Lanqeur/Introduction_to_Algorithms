# 队列
队列的存取方式是先进先出，元素只能从队首离开队列，从队尾进入队列。队列有两种实现方式：链队列和循环队列。
链队列和单向链表类似，都是用指针把各个结点连接起来。
循环队列使用一组连续的存储单元依次存放队列元素，用指针head指向队首元素，用指针rear指向队尾元素，当head和rear走到底时，下一步回到开始的位置，从而在这组连续空间内循环。
和链表一样，队列的查找速度较慢，需要从头到尾一个一个查找，为解决这一问题，有一种优先队列，它让优先级最高的元素先出，复杂度为O(logn)，优先队列并不是正常的队列，实际上是**堆**。
## STL queue
队列的部分操作如下：
* queue< Type>q:定义队列，Type是数据类型；
* q.push(item):把item放进队列；
* q.pop():删除队首元素；
* q.front():返回队首元素，但不进行删除；
* q.back():返回队尾元素；
* q.size():返回元素个数；
* q.empty():检查队列是否为空。
## C++优先队列
很多算法需要用到一种特殊的队列：优先队列。它的特点是最优数据始终位于队首。
优先队列效率很高：新数据插入队列生成新的最优队首元素，计算复杂度是O(logn)，弹出最优的队首元素后在队列中计算出新的最优队首元素，计算复杂度也是O(logn)。
C++STL优先队列priority_queue用堆来实现，堆是用二叉树实现的一种数据结构。
定义：priority_queue<Type,Container,Functional>。
Type是数据类型，Container是容器类型（用数组实现的容器，默认是vector），Functional是比较的方式。当需要使用自定义的数据类型时才需要传入这3个参数，使用基本数据类型时，只需要传入数据类型，默认是大顶堆，堆顶是最大值。
priority_queue部分操作如下：
* pq.push():入队；
* pq.pop():出队；
* pq.size():返回当前队列元素个数；
* pq.top():返回队首元素；
* pq.empty():判断是否为空。
## prority_queue理解
优先队列是一种容器适配器，使用堆的数据结构，保证了第一个元素总是优先队列中最大的或最小的元素。
优先队列默认使用vector作为底层存储数据的结构，在vector上使用堆算法将vector中的元素构造成堆的结构。
priority_queue有3个参数：
* Type是优先队列中存储的数据类型；
* Container=vector< Type>：Container是优先队列底层采用使用的存储结构，默认采用vector；
* Functinal=less< Type>:Functinal是定义优先队列中元素比较方式的类，默认按小于的方式(less)比较，这种比较方式创建出来的就是大堆。如果需要创建小堆，就需要将less改为greater。
less类和greater类是模板类，需要模板参数即优先队列存储的数据类型Type，它们在内部重载()，返回“<”和“>”运算符的bool值。如果想要比较自定义类型的数据，也可以自己定义一个比较类，并且重载()。

priority_queue容器不能使用迭代器，操作与堆类似，只能从堆顶删除元素，只能常量访问堆顶元素。