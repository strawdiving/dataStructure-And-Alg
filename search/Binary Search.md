## 二分查找
```c++
template <typename Comparable>

int binarySearch(const vector<Comparable>& a, const COmparable& x)
{
    int low = 0,high = a.size()-1;
    // 范围没有缩小到只包含一个元素
    while(low < high) {
        int mid = (low + high)/2;
        if(a[mid] < x) 
          low = mid + 1;
        else if(a[mid] > x)
          high = mid - 1;
        else 
          return mid;
    }
    return -1;
}
```
### 分析：
- 每次迭代在循环内全部工作的花费是O(1)

- 循环次数：从 high-low = N-1开始，在 high-low <= -1结束；每次循环后，（high-low）的值至少将该次循环前的值折半。

若 high-low = 128，则各次迭代后（high-low)的最大值为 64,32,16,8,4,2,1,0,-1

**循环的次数最多为 log(N-1)+2 ==> O(LogN)**

**注：二分查找的输入必须是一个有序的元素列表**
