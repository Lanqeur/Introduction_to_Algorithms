# 尺取法
尺取法又称为双指针，是算法竞赛中常用的一个优化技巧，用来解决序列的区间问题，其操作简单，编程容易。
尺取法就是在区间操作时，用两个指针同时遍历区间，从而实现高效率操作。
尺取法的优化原理是，可以把两重循环转换为一重循环，从而把复杂度由O(n^2^)变成O(n)：
```C++
for(int i=0;i<n;i++)//i从头扫描到尾
for(int j=n-1;j>=0;j--)//j从尾扫描到头
{...}
```
用尺取法优化这个两重循环，把两重循环变成一重循环，在这个循环中一起处理i和j，复杂度就变为O(n)了：
```C++
for(int i=0,j=n-1;i<j;i++,j--)
{...}
```
虽然尺取法很简单，但是它的应用有极大的限制：要求i < j，也就是说，i从头到尾扫描，j从尾到头扫描，两者在中间位置相会。由于这种应用场合并不多，因此尺取法只能用于处理和区间有关的一些问题。也可以把for循环改为while循环来实现尺取法：
```C++
int i=0,j=n-1;
while(i<j)
{
    ...
    i++;
    j--;
    ...
}
```
以上例子使用的是“反向扫描”尺取法，另外还有一种“同向扫描”尺取法，即i、j指针是同向前进或后退的。
## 总结
循环指针i、j称为“扫描指针”，在尺取法中，这两个“扫描指针”有以下两种扫描方法：
### “反向扫描”尺取法
指针i、j扫描方向相反，i从头扫描到尾，j从尾扫描到头，两者在中间相会。反向扫描的i、j指针称为“左右指针”。
### “同向扫描”尺取法
指针i、j的扫描方向相同，都从头扫描到尾，但是速度不一样，例如可以让j跑在i前面。同向扫描的i、j指针称为“快慢指针”，此时由于i和j的速度不同，i和j之间将在序列上产生一个大小可变的“滑动窗口”，这是“同向扫描”尺取法的优势。