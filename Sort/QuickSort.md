# QuickSort

```c
#include "stdio.h"
#include "stdlib.h"
#include "string.h"
#include<time.h>
#include <sys/time.h>

void printArray05(int array[], int len)
{
    int i = 0;

    for (i = 0; i < len; i++)
    {
        printf("%d ", array[i]);
    }

    printf("\n");
}

void swap5(int array[], int i, int j)
{
    int temp = array[i];
    array[i] = array[j];
    array[j] = temp;
}

/*************************itcast***********************************/
int partition(int array[], int low, int high)
{
    int pv = array[low]; //最左边元素作为基准值

    while (low < high)
    {
        while ((low < high) && (array[high] >= pv))//里面要再加一层 low< high 判断
        {
            high--; //比基准大，本来就在右边，所以high前移动
        }
        swap5(array, low, high);//从右找到第一个小于基准值的位置，并与基准值位置的值互换
        while ((low < high) && (array[low] <= pv))
        {
            low++;
        }
        swap5(array, low, high);//从左找到第一个大于基准值的位置，并于前面小于基准的位置交换值
    }

    return low;
}

void QSort(int array[], int low, int high)
{
    if (low < high)
    {
        int pivot = partition(array, low, high);

        QSort(array, low, pivot - 1);
        QSort(array, pivot + 1, high);
    }
}

void QuickSort(int array[], int len) // O(n*logn)
{
    QSort(array, 0, len - 1);
}
/*****************************itcast**************************************/

/****************************blog****************************************/

// 挖坑填数进行总结
// 1．i =L; j = R; 将基准数挖出形成第一个坑a[i]。
// 2．j--由后向前找比它小的数，找到后挖出此数填前一个坑a[i]中。
// 3．i++由前向后找比它大的数，找到后也挖出此数填到前一个坑a[j]中。
// 4．再重复执行2，3二步，直到i==j，将基准数填入a[i]中
// 5. 递归i==j左边的数列，递归i==j右边的数列

int AdjustArray(int s[], int left, int right) //返回调整后基准数的位置
{
    int i = left, j = right;
    int x = s[left]; //s[l]即s[i]就是第一个坑
    while (i < j)
    {
        // 从右向左找小于x的数来填s[i]
        while (i < j && s[j] >= x)
            j--;
        if (i < j)
        {
            s[i] = s[j]; //将s[j]填到s[i]中，s[j]就形成了一个新的坑
            i++;
        }
        // 从左向右找大于或等于x的数来填s[j]
        while (i < j && s[i] < x)
            i++;
        if (i < j)
        {
            s[j] = s[i]; //将s[i]填到s[j]中，s[i]就形成了一个新的坑
            j--;
        }
    }
    //退出时，i等于j。将x填到这个坑中。
    s[i] = x;
    return i;
}

//再写分治法的代码：
void quick_sort1(int s[], int l, int r)
{
    if (l < r)
    {
        int i = AdjustArray(s, l, r); //先成挖坑填数法调整s[]
        quick_sort1(s, l, i - 1);     // 递归调用
        quick_sort1(s, i + 1, r);
    }
}

//这样的代码显然不够简洁，对其组合整理下：
void quick_sort(int s[], int left, int right)
{
    if (left < right)
    {
        //Swap(s[l], s[(l + r) / 2]); //将中间的这个数和第一个数交换参见注1
        int i = left, j = right, x = s[left];
        while (i < j)
        {
            while (i < j && s[j] >= x) // 从右向左找第一个小于x的数
                j--;
            if (i < j)
                s[i++] = s[j];

            while (i < j && s[i] < x) // 从左向右找第一个大于等于x的数
                i++;
            if (i < j)
                s[j--] = s[i];
        }
        s[i] = x;//i左边均小于s[i]的值,i的右边均大于s[i]的值
        quick_sort(s, left, i - 1); // 递归调用
        quick_sort(s, i + 1, right);
    }
}
/****************************blog****************************************/

int main()
{
    int array[] = {72, 6, 57, 88, 60, 42, 83, 73, 48, 85};
    int len = sizeof(array) / sizeof(*array);
    printArray05(array, len);
    struct timespec tStart, tEnd;
    clock_gettime(CLOCK_MONOTONIC, &tStart);
    //QuickSort(array, len);//800ns
    //quick_sort1(array, 0, len -1);//700ns
    quick_sort(array, 0, len -1);//600ns
    clock_gettime(CLOCK_MONOTONIC, &tEnd);
    printf("\nelasped time = %d\n\n", tEnd.tv_nsec - tStart.tv_nsec);
    printArray05(array, len);
    system("pause");
    return 0;
}

```

