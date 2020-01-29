

```c++
int leftChild(int i)
{
    return 2 * i + 1;
}

void percDown(vector<int> &a, int j, int n)
{
    int left;
    int tmp = a[j];
    for (; leftChild(j)<n; j = left)
    {
        left = leftChild(j);
        if (left<n-1 && a[left] < a[left + 1])
            ++left;
        if (a[left] > tmp)
            a[j] = a[left];
        else
            break;
    }
    a[j] = tmp;
}

// heap sort 堆排序
void heapSort(vector<int> &a)
{
    //heapBuild
    for (int i=a.size() / 2-1; i >= 0; --i)
    {
        percDown(a, i, a.size());
    }

    for (int j = a.size() - 1; j > 0; j--)
    {
        std::swap(a[0], a[j]);
        percDown(a, 0, j);
    }
}
```