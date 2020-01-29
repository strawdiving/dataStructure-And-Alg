## 选择排序（Selection Sort）
```c++
void selectionSort(vector<int> &a)
{
    for (int i = 0; i < a.size(); i++)
    {
        int min = i;
        for (int j = i + 1; j < a.size(); j++)
        {
            if (a[j] < a[min])
                min = j;
        }
        std::swap(a[i], a[min]);
    }
}
```
**思路：**

以无序区的第一个元素作为基准，从无序区选一个最小的元素放到有序区的最后（即和无序区第一个元素交换）

**步骤：**

1）数组a[0,...,N-1]，初始时全为无序，令i=0

2）在无序区a[i,...,N-1]中，选最小的元素，将其与a[i]交换，a[0,...,i]变为有序区

3）i++，重复2），直到i=N-1

数组a[0,...,N-1]中最小的，和a[0]交换，作为第1个元素

剩下的数组元素a[1,...,N-1]中，选最小的和a[1]交换，作为第2个元素

......

![selection sort]()

**时间复杂度：**

O(N2)