# 排序
常见的排序算法如下：
1. 基于比较的低效算法：选择排序、插入排序、冒泡排序。时间复杂度为O(n^2^)。
2. 基于比较的高效算法：归并排序、快速排序、堆排序。时间复杂度为O(nlogn)。
3. 基于数值划分的高效算法：计数排序、基数排序、桶排序。时间复杂度O(n)。

第3种排序算法不是基于比较的，而是对数值按位划分，按照以空间换取时间的思路排序，虽然看起来复杂度更好，但实际上它们的应用环境比较苛刻，在很多情况下并不比前几种排序算法更好。
在算法竞赛中，一般不需要手动编写这些排序算法，而是直接使用库函数，例如C++和JAVA的sort()函数，Python的sort()和sorted()函数。
## C++的sort()函数
STL的排序函数sort()有以下两种定义：
```C++
void sort(RandomAccessIterator first,RandomAccessIterator last);
void sort(RandomAccessIterator first,RandomAccessIterator last,Compare comp);
```
返回值：无。
复杂度：O(nlogn)。
它排序的范围是[first,last)，包括first，不包括last。
默认情况下，sort()按从小到大进行排序。sort()自带4种排序：less,greater,less_equal,greater_equal。
也可以用自定义的比较函数进行排序：
```C++
bool my_less(int i,int j){return i<j;}//自定义小于函数
bool my_greater(int i,int j){return i>j;}//自定义大于函数
int main()
{
    int a[]={3,7,2,5,6,8,5,4};
    sort(a,a+4);//对前4个数排序
    sort(a,a+8,less<int>());//从小到大排序
    sort(a,a+8,my_less);//自定义排序
    sort(a,a+8,greater<int>());//从大到小排序
    sort(a,a+8,my_greater);//自定义排序
    return 0;
}
```
C++的sort()有两个优点：能在原数组上排序，不需要新的空间；能在数组的局部空间上排序。