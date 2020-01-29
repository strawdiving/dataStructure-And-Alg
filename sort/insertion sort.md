## 插入排序（insertion sort）
```c++
void insertionSort(vector<int> &a)
{
    for(int i=1;i<a.size();++i)
    {
       int tmp=a[i];
       int j;
       for(j=i;j>0&&tmp<a[j-1];--j)
       {
          a[j]=a[j-1];
       }
       //将tmp插入到正确的位置
       a[j]=tmp;       
    }      
}    
```
**思路：**
  
  每一次将一个待排序的记录，按其大小插入到前面已排好序的子序列中（利用 **“已知位置0到位置 i-1上的元素已经处于排过序的状态”** 的事实）

**过程：**

 1）初始时，a[0]自成一个有序区，a[1,....,N-1]为无序区，令i=1

 2）将a[i]并入当前有序区a[0,...,i-1]，形成新的有序区a[0,....,i]
 
 选择无序区的第一个a[i]作为tmp，与有序区的各项比较，将（位置i之前）所有大于tmp的元素右移，找到 a[j]<tmp 时停下，将tmp插入到a[j+1]处

3）i加1，重复2），直到处理完a[N-1]，排序完成

**时间复杂度：**

　　1）内循环中，测试次数对每个 i 值最多是 i+1 次（当输入是反序时），内循环中的测试次数为(2+3+...+N)=Θ(N2)；

　　2）如果输入已排好序（正序），则内层循环都不执行，运行时间是O(N)；

　　平均运行时间为 **O(N2)**。

![insertion sort](https://github.com/strawdiving/dataStructure-And-Alg/blob/master/sort/imgs/insertion%20sort.png)


