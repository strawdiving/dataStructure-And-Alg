```c-plus-plus
#include <stdio.h>
#include <iostream>
#include <vector>
using namespace std;



int division(vector<int> &a, int left, int right)
{
       //int i = rand() % (right-left+1) + left;
       //int i = left;

       int center = (left + right) / 2;

       if (a[center] < a[left]) std::swap(a[left], a[center]);
       if (a[left] > a[right]) std::swap(a[left], a[right]);
       if (a[center] > a[right]) std::swap(a[right], a[center]);

       std::swap(a[center], a[right - 1]);
       return a[right - 1];

       //return i;
}

// insertion sort 插入排序
void insertionSort(vector<int>&a, int left, int right)
{
       for (int i = left + 1; i <= right; i++)
       {
              int tmp = a[i];
              int j;
              for (j = i; j > 0 && tmp < a[j - 1]; --j)
                     {
                           a[j] = a[j - 1];
                     }
              a[j] = tmp;
       }
}


void quicksort(vector<int> &a, int left, int right)
{
       if (left < right)
       {
              int base = division(a, left, right);

              int i = left;
int j = right - 1;

while (i < j) {
       while (a[++i] < base){}
       while (base < a[--j]){}
       if (i < j) {
              std::swap(a[i], a[j]);
       }
       //else

       //break;
}
std::swap(a[right - 1], a[i]);

quicksort(a, left, i - 1);
quicksort(a, i + 1, right);
       }
       else
              insertionSort(a, left, right);
}

// quick sort 快速排序
void quicksort(vector<int> &a)
{
       quicksort(a, 0, a.size() - 1);
}

// bubble sort 冒泡排序
void bubbleSort(vector<int> &a)
{
       for (int i = 0; i < a.size() - 1; i++)
              for (int j = a.size() - 1; j > i; j--)
              {
                     if (a[j] > a[j - 1])
                           std::swap(a[j], a[j - 1]);
              }
}

// selection sort 选择排序
void selectionSort(vector<int> &a)
{
       for (int i = 0; i < a.size(); i++)
       {
              int tmp = i;
              for (int j = i + 1; j < a.size(); j++)
              {
                     if (a[j] < a[tmp])
                           tmp = j;
              }
              std::swap(a[i], a[tmp]);
       }
}

// bucket sort 桶排序
void bucketSort(vector<int> &a)
{
       int result[10] = { 0 };
       for (int i = 0; i < a.size(); i++)
       {
              result[a[i]]++;
       }
       for (int i = 0; i < 10; i++)
       {
              for (int j = 0; j < result[i]; j++)
              {
                     cout << i << endl;
              }
       }
}

int maxBit(vector<int> &a)
{
       int bit = 0;
       for (int i = 0; i < a.size(); i++)
       {
              int p = a[i];
              int c = 1;
              while (p / 10)
              {
                     p = p / 10;
                     c++;
              }
              if (c > bit)
                     bit = c;
       }
       return bit;
}

// radix sort, radix排序
void radix_sort(vector<int> &a)
{
       int buckets[10] = { 0 };
       int tmp[12];
       int bit = maxBit(a);
       int c = 1;

       cout << bit << endl;
       for (int i = 0; i < bit; i++)
       {
              for (int i = 0; i < 10; i++)//装桶之前要清零
                     buckets[i] = 0;

              for (int j = 0; j < a.size(); j++) //将数据出现的次数存储在buckets[]中
              {
                     int k = a[j] / c;
                     int q = k % 10;
                     buckets[q]++;
              }

              for (int i = 1; i < 10;i++)
       {
              buckets[i] += buckets[i - 1];
                     cout << "buckets " << i << ":" << buckets[i]<<"\n"<<endl;
        }

              for (int j = a.size() - 1; j >= 0; j--)
              {
                     int p = a[j] / c;
                     int k = p % 10;
                     tmp[buckets[k] - 1] = a[j];
                     buckets[k]--;
              }
                           
              for (int i = 0; i < a.size(); i++)
              {
                     a[i] = tmp[i];
              }

              c = c * 10;
       }
}

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

int main(void)
{
       //int aa[10] = { 1, 4, 5, 3, 7, 8, 4, 9, 6, 0 };
       //int aa[12] = { 65, 24, 47, 13, 50, 92, 88, 66, 33, 22445, 10001, 624159 };
       int aa[7] = { 31,41,59,26,53,58,97 };
       vector<int>a(aa, aa + 7);
       heapSort(a);

       //quicksort(a);
       //bubbleSort(a);
       //selectionSort(a);

       //bucketSort(a);
       //radix_sort(a);
       for (vector<int>::iterator i = a.begin(); i < a.end(); i++)
       {
              cout << *i << endl;
       }
       
       system("pause");
       return 0;
}
```
