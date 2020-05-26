# SelectionSort

```c
#include "stdio.h"
#include "stdlib.h"
#include "string.h"

void printArray01(int array[], int len)
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

void SelectionSort(int array[], int len) // O(n*n)
{
	int i = 0;
	int j = 0;
	int k = -1;

	for(i=0; i<len; i++)
	{
		k = i; //寻找最小元素的下标
		for(j=i+1; j<len; j++)
		{
			if( array[j] < array[k] ) //开始寻找最小元素的下标
			{
				k = j;	
			}
		}
		swap01(array, i, k);
	}
}


/****************************blog****************************************/
void SelectionSort2(int array[], int len) // O(n*n)
{
	int i = 0;
	int j = 0;
	int k = -1;

	for(i=0; i<len; i++)
	{
		//k = i; //寻找最小元素的下标
		for(j=i+1; j<len; j++)
		{
			if( array[j] < array[i] ) //开始寻找最小元素的下标
			{
				swap01(array, i, j);
			}
		}
		
	}
}
/****************************blog****************************************/
int main()
{
	int array[] = {12, 5, 433, 253, 216, 7};
	//int array[] = {12, 5, 433, 253};
	int len = sizeof(array) / sizeof(*array); 

	printArray01(array, len);
	SelectionSort2(array, len);
	printArray01(array, len);
	system("pause");
	return 0;
}

```

