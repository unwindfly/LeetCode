# BubbleSort

```c
#include "stdio.h"
#include "stdlib.h"
#include "string.h"
void printfArray03(int array[], int len)
{
	int i = 0;

	for(i=0; i<len; i++)
	{
		printf("%d ", array[i]);
	}
	printf("\n");
}

void swap03(int array[], int i, int j)
{
	int temp = array[i];
	array[i] = array[j];
	array[j] = temp;
}

void BubbleSort1(int a[], int n)//O(n*n)
{
	int i, j;
	for (i = 0; i<n; i++)
		for (j = 1; j<n - i; j++)//升序排列， 每趟外循环之后的最后一个元素肯定时最大的，不需要再判断（所以 j < n - i）
			if (a[j - 1] >a[j])
				swap03(a, j - 1, j);
}


void BubbleSort(int array[], int len) // O(n*n)
{
	int i = 0;
	int j = 0;
	int exchange = 1; //表明数组是否已经排好序 已经排好序为0   1表示没有排好序
	for(i=0; (i<len) && exchange; i++)
	{
		exchange = 0;//认为已经排序完毕
		for(j=len-1; j>i; j--)// 最小的元素放在最左边，所以 j > i(第i趟之后, 第i个元素是最小的， 而且从0到i递增)
		{
			if( array[j] < array[j-1] )
			{
				swap03(array, j, j-1);
				exchange = 1;//
			}
		}
	}
}

void BubbleSort2(int array[], int n)//o(n*n) 上面的BubbleSort while 循环方式（每次外循环后找到最大的放在最右边）
{
	int j, k;
	int flag;
	
	k = n;
	flag = 1;
	while (flag)
	{
		flag = 0;
		for (j = 1; j<k; j++)
    {
			if (array[j - 1] >array[j])
			{
				swap03(array, j - 1, j);
				flag = 1;
			}
		}
    k--;
	}
}

void BubbleSort3(int array[], int n)
{
	int j, k;
	int flag;
	
	flag = n;
	while (flag> 0)
	{
		k = flag;
		flag = 0;
		for (j = 1; j<k; j++)
        {
			if (array[j - 1] >array[j])
			{
				Swap(array, j - 1, j);
				flag = j;//记录最后一次交换的位置, 节省for执行的次数, 对if中的语句执行次数无影响
		    }
        }
	}
}


int main()
{
	int array[] ={8,3,6,1};
	int len = sizeof(array) / sizeof(*array); 
	printfArray03(array, len);
	BubbleSort(array, len);
	printfArray03(array, len);
	system("pause");
	return 0;
}
```

