# InsertSort

```c
#include "stdio.h"
#include "stdlib.h"
#include "string.h"
#include "windows.h"

void printArray02(int array[], int len)
{
	int i = 0;

	for(i=0; i<len; i++)
	{
		printf("%d ", array[i]);
	}

	printf("\n");
}

void swap01(int array[], int i, int j)
{
	int temp = array[i];
	array[i] = array[j];
	array[j] = temp;
}

void Insertsort1(int array[], int n)//O(n*n)
{
	int i = 0, j = 0, k = 0;
	for (i = 1; i < n; i++)
	{
		//为a[i]在前面的a[0...i-1]有序区间中找一个合适的位置
		for (j = i - 1; j >= 0; j--)
			if (array[j] <array[i])
				break;
		//如找到了一个合适的位置
		if (j != i - 1)///表示至少执行了for循环中的语句，已经j--(而且表示从0  到 j 处 均小于a[i])
		{
			//将比a[i]大的数据向后移
			int temp = array[i];
			for (k = i - 1; k > j  ; k--)//note : k > j (from break branch j to i - 1)
				array[k + 1] = array[k];
			//将a[i]放到正确位置上
			array[k + 1] = temp;// a[k+1]
		}
	}
}


void InertionSort(int array[], int len) // O(n*n)
{
	int i = 0;
	int j = 0;
	int k = -1;
	int temp = -1;

	//{12, 5, 433, 253, 216, 7};
	for(i=1; i<len; i++)
	{
		k = i; //待插入位置
		temp = array[k];

		for(j=i-1; (j>=0)   && (array[j]>temp) ; j--)
		{ 
			array[j+1] = array[j]; //元素后移
			k = j; //k需要插入的位置
            
		}

		array[k] = temp;//元素插入
	}
}

void Insertsort2(int array[], int n)//(O(n*n))
{
	int i, j;
	for (i = 1; i<n; i++)
		if (array[i] <array[i - 1])//加此判断在i=2时会减少下面的for循环执行2遍
		{
			int temp = array[i];
			for (j = i - 1; j>= 0   && array[j] >temp; j--)
				array[j + 1] = array[j];
			array[j + 1] = temp;
		}
}

void Insertsort3(int array[], int n)//O(n*n)
{
	int i, j;
	for (i = 1; i< n; i++)
		for (j = i - 1; j>= 0  && array[j] >array[j + 1]; j--)//从a[i]到a[0]逐一比较，若大于索引值大的则进行交换
			swap01(array, j, j + 1);
}

int main()
{
	int array[] = {12, 5, 433, 253, 216, 7};
	int len = sizeof(array) / sizeof(*array); 

	printArray02(array, len);
    DWORD start,end;
    // start= GetTickCount();
     //Insertsort1(array, len);
    // end= GetTickCount();
    //printf("time=%dms\n",end-start);
	//InertionSort(array, len);
    Insertsort2(array, len);
    //Insertsort3(array, len);
	printArray02(array, len);
	system("pause");
	return 0;
}

```

