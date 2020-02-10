# dataStructure-And-Alg
data structure and algorithm collections

## Sort
1.  [insertion sort 插入排序](https://github.com/strawdiving/dataStructure-And-Alg/blob/master/sort/insertion%20sort.md)
2.  [quick sort 快速排序](https://github.com/strawdiving/dataStructure-And-Alg/blob/master/sort/quick%20sort.md)
3.  [bubble sort 冒泡排序](https://github.com/strawdiving/dataStructure-And-Alg/blob/master/sort/bubble%20sort.md)
4.  [selection sort 选择排序](https://github.com/strawdiving/dataStructure-And-Alg/blob/master/sort/selection%20sort.md)
5.  [bucket sort 桶排序](https://github.com/strawdiving/dataStructure-And-Alg/blob/master/sort/bucket%20sort.md)
6.  [radix sort 基数排序](https://github.com/strawdiving/dataStructure-And-Alg/blob/master/sort/Radix%20Sort.md)
7.  [heap sort 堆排序](https://github.com/strawdiving/dataStructure-And-Alg/blob/master/sort/heap%20sort.md)
8.  [merge sort 归并排序](https://github.com/strawdiving/dataStructure-And-Alg/blob/master/sort/merge%20sort.md)
9.  [shell sort shell排序](https://github.com/strawdiving/dataStructure-And-Alg/blob/master/sort/shell%20sort.md)

### 排序总结
对一般的内部排序应用，**插入排序，shell排序，归并排序，快速排序**是常用的，选择哪一种依赖于输入的大小和底层环境。
- 插入排序适用于非常少量的输入
- shell排序适用于适量输入（上佳），对适当的增量排序，性能极好，代码少
- 归并排序有O(NlogN)最坏情形性能，但需要额外的空间。其所使用的比较次数几乎是最优的
- 快速排序具有几乎是必然的O(NlogN)性能

其他排序算法：
- 基数排序，可对字符串以线性时间完成排序
- 对输入的数去重，可以用桶排序，a[t]=1,即对出现的数字记为1,不累加；或排完序后输出，若a[i]=a[i-1]，则a[i]不输出

注：快排比归并排序快的原因——大O表示法中的常量有时候也事关重大


## Search
1. [Binary Search 二分查找](https://github.com/strawdiving/dataStructure-And-Alg/blob/master/search/Binary%20Search.md)
2. [DFS 深度优先搜索](https://github.com/strawdiving/dataStructure-And-Alg/blob/master/search/DFS.md)
3. [BFS 广度优先搜索](https://github.com/strawdiving/dataStructure-And-Alg/blob/master/search/BFS.md)
