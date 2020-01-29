## 桶排序（Bucket Sort）
要使桶排序正常运行，需要额外的信息：

输入A1，A2，...，AN必须只由小于M的正整数构成，即Ai<M。使用一个大小为M的数组result，初始化为全0。数组有M个单元，即M个桶（bucket）。 
```c++
void bucketSort(vector<int> &a, const int maxVal)

/* 初始化桶 */
for (int i = 0; i < maxVal; i++)
{
    result[i] = 0;
}
/* 读入数据装桶 */
for (int i = 0; i < a.size(); i++)
{
    result[a[i]]++;
}
/* 将桶中的每个数打印出来，出现几次就打印几次 */
for (int i = 0; i < maxVal; i++)
 　　for (int j = 0; j < result[i]; j++)
    {
       cout << i << endl;
    }
}
```
**步骤：**

result[Ai]中存放的是Ai出现的次数；

读入Ai时，result[Ai]增1；　　

所有输入数据读入后，扫描数组result，打印出排序后的数据，result[Ai]值是n，Ai就打印n次.

eg.  输入数组{1,4,5,3,7,8,4,9,6,5,0}，最大为9，另建一个大小为10的数组，初始化为全0。

![bucket](https://github.com/strawdiving/dataStructure-And-Alg/blob/master/sort/imgs/bucket.png)

读入数组：

　　遇到1，将result[1]加1

　　遇到4，将result[4]加1

　　......

　　遇到5，将result[5]加1

　　遇到0，将result[0]加1

得到结果：

![bucket1](https://github.com/strawdiving/dataStructure-And-Alg/blob/master/sort/imgs/bucket1.png)

打印结果：

　　0 1 3 4 4 5 5 6 7 8 9

**时间复杂度：**

　　算法用时O(M+N)，M为桶的个数，N为待排序数组的大小。

**空间复杂度：**

　　O(M+N)

如果输入数据非常庞大，桶的数量会非常多，空间代价将会非常大。　
