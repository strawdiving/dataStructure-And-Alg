## 冒泡排序
冒泡排序属于交换排序类。
```c++
void bubbleSort(vector<int> &a)
{
    for (int i = 0; i < a.size() - 1; i++)  //(N-1)趟操作
        for (int j = a.size() - 1; j > i; j--)
        {
                        /* 从小到大排序 */
            if (a[j] < a[j - 1])
                std::swap(a[j], a[j - 1]);
                       
            /** 
             * 从大到小排序 
            if (a[j] > a[j - 1])
                std::swap(a[j], a[j - 1]);
             */
        }
}    
```
**思路：**

　　重的沉底，轻的上浮（增序）。每次比较两个相邻的元素，如果它们顺序错误就交换过来。

**步骤：**

每一趟将一个数归位。

从第一位开始，进行相邻两数的比较，较小的放在后面；

比较完后向后挪一位继续比较下面两个相邻数大小，直到最后一个尚未归位的数。

已归位的数无需再比较。

如果有N个数需要排序，只需要将N-1个数归位，即进行N-1趟操作。

![bubble sort](https://github.com/strawdiving/dataStructure-And-Alg/blob/master/sort/imgs/bubble%20sort.png)

**时间复杂度：**

O(N2)