## 快速排序（Quick Sort）　
快速排序是一种使用很广泛的排序算法，属于交换排序类。

**思路：使用“分治”的递归算法进行排序**

**步骤：**
1. 基准情形：N=0或1，无需排序，返回
2. N>1，从数组S中任意取一个元素ν，称之为枢纽元（pivot）
3. **分割：**

   将比ν大的元素全部放到v的右边，S1
   
   将比v小的元素全部放到v的左边，S2
  
4. 对左右两个区间递归地快速排序，直到序列中只有0或1个元素
   
   quicksort(S1)
   
   quicksort(S2)

注意：应避免创建新的数组，占据额外的内存空间

**分割方法：**
第 3）步分割的方法不是唯一的，因此成为了一种设计决策。

1. 常见的，**将第一个元素作为枢纽元**

　 如果输入是随机的，是可以的；
  
　 如果输入是预排序或反序的，则会产生一个劣质的分割，所有元素都在S1或S2中，且对所有递归情形都一样。
  
　 花费的时间是二次的，且枢纽元是无效的。
  
　 类似的，还有选取前2个互异的元素中的较大者作为枢纽元。
  
2. **随机选取基准数**

安全，不会总发生劣质的分割。
   
对绝大多数输入数据达到O(NlogN)的期望时间复杂度。
  
3. **三数中值分割法（Median-of-Three）**

  　最佳枢纽元：一个数组N个数的中值，即第N/2个最大的数。但很难算出，且明显减慢快排的速度
   
   一般做法：使用左端、右端、中心位置上的三个元素的中值作为基准数。
   
   消除了预排序输入的不好情形，且减少了大约14%的比较次数。避免“元素当初输入时不够随机”带来的恶化效应。　
    
```c++
/**
* 快速排序的驱动程序
*/
void quicksort(vector<int> &a)
{
    quicksort(a, 0, a.size() - 1);
}

void quicksort(vector<int> &a, int left, int right) 
```

```c++
void quicksort(vector<int> &a, int left, int right)
{
     if (left >= right) return;

     /* 找到枢纽元 */
     int base = division(a, left, right);
     int pivot = a[base];
        
     /* 开始分割 */
     int i = left;
     int j = right;
     while (i < j)
     {
         /* 先从右向左找到小于枢纽元的数 */
        while (a[j] >= pivot && i < j)  j--;
               
         /* 再从左向右找到大于枢纽元的数 */
        while (a[i] <= pivot && i < j)  i++;

         /*如果两者没有交会，则交换两数在数组中的位置 */  
        if (i < j)
           std::swap(a[i], a[j]);
     }

     /* 将枢纽元归位 */
     std::swap(a[base], a[i]);

      /* 递归地对左、右两半部分进行快速排序 */
     quicksort(a, left, i - 1);
     quicksort(a, i + 1, right);
}
```

```c++
/**
* 使用第一个元素或[left,right]内的随机数作为枢纽元 
*/
int division(vector<int> &a, int left, int right)
{
        /* 以下方案二选一 */

        /* 随机选取[left,right]范围内的数作为枢纽元 */
    int i = rand() % (right-left+1) + left; // [left,right]内的随机数
    std::swap(a[left], a[i]);
    return left;

     /* 使用第一个数作为枢纽元 */
     return left;
}    
```
![quick sort](https://github.com/strawdiving/dataStructure-And-Alg/blob/master/sort/imgs/quick%20sort.png)

- 使用三数中值分割法（Median-of-Three）
```c++
void quicksort(vector<int> &a, int left, int right)
{
    if (left >= right) return;
    int pivot = division(a, left, right);

    int i = left; // 开始位置，警戒标志
    int j = right - 1;

    while (i < j) {
        /* 从left+1和right-2开始 */
        while (a[++i] < pivot){}
        while (pivot < a[--j]){}
        if (i < j)
            std::swap(a[i], a[j]);
        else
            break;
    }
    std::swap(a[right - 1], a[i]);

    quicksort(a, left, i - 1);
    quicksort(a, i + 1, right);
}
```

```c++
int division(vector<int> &a, int left, int right)
{
    int center = (left + right) / 2;

    if (a[center] < a[left]) std::swap(a[left], a[center]);
    if (a[left] > a[right]) std::swap(a[left], a[right]);
    if (a[center] > a[right]) std::swap(a[right], a[center]);

    std::swap(a[center], a[right - 1]);
    return a[right - 1];
}
```

分析：选取a[left]，a[center]，a[right]的中值作为基准值。

　　先对三者进行排序，a[left]< a[center]<a[right]，a[center]为三者的中值，作为枢纽元pivot，而a[left]， a[right]都处于分割阶段应该在的区间。

　　可以把pivot放到a[right-1]，并在分割阶段将i和j初始化为left和right-1。a[left]<pivot，所以a[left]作为j的警戒标记，不必担心j跑过端点；由于i会停在pivot元素处，所以将pivot存储在a[right-1]处为i提供了一个警戒标记，不必担心i跑过端点。
  
 **时间复杂度：**
 
 N=0或1，时间为常数，记为1。
 
 N>1，用时为：T(N)=T(i)+T(N-i-1)+cN（分割花费的时间）
 
 1）最坏情形：枢纽元始终是最小元素，此时i=0，忽略无关紧要的T(0)=1 

        T(N)=T(N-1)+cN

        T(N-1)=T(N-2)+c(N-1)

         ......

        T(2)=T(1)+c(2)

        相加可得 T(N) =T(1)+c(2+3+4+...+N) =Θ (N2)
        
 2) 最好情形：枢纽元正好位于中间，为简化，假设两个子数组恰好是原数组的一半大小

        T(N)=2T(N/2)+cN ——> T(N)/N=T(N/2)/(N/2)+c

         T(N/2)/(N/2)=T(N/4)/(N/4)+c

         ......

        T(2)/2=T(1)/1+c

        相加可得 T(N) =cNlogN+N =Θ (NlogN)
        
 3) 平均情形：

　　**T(N)=O(NlogN)**
  
  
**适用情形:**

对于很小的数组(N<=20)，快速排序不如插入排序好。

通常的解决办法是，对于小的数组不递归地使用快速排序，而是使用插入排序这样的对小数组有效的排序算法。截止范围在N = 5~20之间都可以，相对只用快排的方式，实际上可以节省15%的运行时间。　　

```c++
if(left+10<=right)
{ 
    // 使用快速排序    
    quicksort(a,left,right);
}
else 
{  
    // 对小数组使用插入排序
    insertionSort(a,left,right);    
}
```
　STL的sort算法，数据量大时采用快排，分段递归排序，一旦分段后的数据量小于某个门槛，为避免快排的递归调用带来过大的额外负载，就改用插入排序。如果递归层次过深，还会改用堆排序。
