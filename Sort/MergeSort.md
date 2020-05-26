# MergeSort

```cpp
#include <stdio.h>
#include <stdlib.h>
#include <malloc.h>
#include <time.h>
#include <sys/time.h>

void printArray06(int array[], int len)
{
	int i = 0;
	for(i=0; i<len; i++)
	{
		printf("%d ", array[i]);
	}
	printf("\n");
}

void swap6(int array[], int i, int j)
{
	int temp = array[i];
	array[i] = array[j];
	array[j] = temp;
}

/*****************************itcast**************************************/
void Merge(int src[], int des[], int low, int mid, int high)
{
	int i = low;
	int j = mid + 1;
	int k = low;

	while( (i <= mid) && (j <= high) ) //将小的放到目的地中
	{
		if( src[i] < src[j] )
		{
			des[k++] = src[i++];
		}
		else
		{
			des[k++] = src[j++];
		}
	}

	while( i <= mid )  //若还剩几个尾部元素
	{
		des[k++] = src[i++];
	}

	while( j <= high ) //若还剩几个尾部元素
	{
		des[k++] = src[j++];
	}
}

//每次分为两路 当只剩下一个元素时，就不需要在划分
void MSort(int src[], int des[], int low, int high, int max)
{
	if( low == high ) //只有一个元素，不需要归并，结果赋给des[low]
	{
		des[low] = src[low]; 
	}
	else //如果多个元素，进行两路划分
	{
		int mid = (low + high) / 2;
		int* space = (int*)malloc(sizeof(int) * max);

		//递归进行两路，两路的划分 
		//当剩下一个元素的时，递归划分结束，然后开始merge归并操作
		if( space != NULL )
		{
			MSort(src, space, low, mid, max); 
			MSort(src, space, mid+1, high, max);
			Merge(space, des, low, mid, high); //调用归并函数进行归并
		}

		free(space);
	}
}

void MergeSort(int array[], int len) // O(n*logn)
{
	MSort(array, array, 0, len-1, len);
}
/*****************************itcast**************************************/

/****************************blog****************************************/
//将有二个有序数列a[first...mid]和a[mid...last]合并。
void mergearray(int a[], int first, int mid, int last, int temp[])
{
	int i = first, j = mid + 1;
	int m = mid, n = last;
	int k = 0;
	
	while (i <= m && j<= n)
	{
		if (a[i] < a[j])
			temp[k++] = a[i++];
		else
			temp[k++] = a[j++];
	}
	
	while (i <= m)
		temp[k++] = a[i++];
	
	while (j <= n)
		temp[k++] = a[j++];
	
	for (i = 0; i<k; i++)
		a[first + i] = temp[i];

}

void mergesort_itcast(int a[], int first, int last, int temp[])
{
	if (first<last)
	{
		int mid = (first + last) / 2;
		mergesort_itcast(a, first, mid, temp); //左边有序
		mergesort_itcast(a, mid + 1, last, temp); //右边有序
		mergearray(a, first, mid, last, temp); //再将二个有序数列合并
	}
}

int MergeSort_itcast(int a[], int n)
{
	int *pTempArray = (int*)malloc(sizeof(int)*n);
	if (pTempArray == NULL)
		return 0;
	mergesort_itcast(a, 0, n - 1, pTempArray);
    free(pTempArray);
	return 1;
}

/****************************blog****************************************/
int main()
{
	int array[] = {21, 25, 49, 25, 16, 8};
	int len = sizeof(array) / sizeof(*array); 
	printArray06(array, len);
	struct timespec tStart, tEnd;
    clock_gettime(CLOCK_MONOTONIC, &tStart);
    //MergeSort(array, len);
    MergeSort_itcast(array, len);
    clock_gettime(CLOCK_MONOTONIC, &tEnd);
    printf("\nelaseped time = %d\n\n", tEnd.tv_nsec - tStart.tv_nsec);
	printArray06(array, len);
	system("pause");
	return 0;
}

```

