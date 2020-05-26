# ShellSort

```c
#include "stdio.h"
#include "stdlib.h"
#include "string.h"
#include<time.h>
#include <sys/time.h>
/*
struct timeval {
               time_t      tv_sec;   秒 
               suseconds_t tv_usec;  微秒 
           }; 

struct timespec {
    time_t tv_sec; //seconds
    long   tv_nsec; //nonoseconds 纳秒
}
*/

/****************************blog****************************************/
void println(int array[], int len)
{
	int i = 0;

	for(i=0; i<len; i++)
	{
		printf("%d ", array[i]);
	}

	printf("\n");
}
void swap(int array[], int i, int j)
{
	int temp = array[i];
	array[i] = array[j];
	array[j] = temp;
}

void shellsort1(int a[], int n)
{
	int i, j, gap;
	for(gap = n / 2; gap> 0; gap /= 2)
    {
		for (i = 0; i<gap; i++) //按组排序
		{
			for (j = i + gap; j<n; j += gap) 
			{
				if (a[j] <a[j - gap])//同组比较
				{
					int temp = a[j];//缓存后面小的元素
					int k = j - gap;//缓存同组中较大元素的索引
					while (k >= 0 && a[k] >temp)//较大的元素的索引值有效且大于较小的元素
					{
						a[k + gap] = a[k];
						k -= gap;
					}
					a[k + gap] = temp;println(a, n);
				}
			}
        }
    }    
}

void shellsort2(int a[], int n)
{
	int j, gap;
	
	for(gap = n / 2; gap> 0; gap /= 2)
		for (j = gap; j<n; j++) //从数组第gap个元素开始
			if (a[j] <a[j - gap]) //每个元素与自己组内的数据进行直接插入排序
			{
				int temp = a[j];
				int k = j - gap;
				while (k>= 0 &&a[k] >temp)
				{
					a[k + gap] = a[k];
					k -= gap;
				}
				a[k + gap] = temp;
			}
}

void shellsort3(int a[], int n)
{
	int i, j, gap;
	for (gap = n / 2; gap> 0; gap /= 2)
    {
		for (i = gap; i<n; i++)
        {
			for (j = i - gap; j>= 0 &&a[j] >a[j + gap]; j -= gap)
            {
                swap(a, j, j + gap);
                printf("i = %d gap=%d ",i, gap);
                println(a, n);
                printf("    a[%d]=%d <---> a[%d]=%d\n",  j,a[j],j+gap, a[j+gap]);//每交换一个元素后都要从0开始再比较
            }
        }
	}			
}

void shellsort3_while(int a[], int n)
{
	int i, j, gap = n;
    do
    {
      gap = gap/2;
	  for (i = gap; i<n; i++)
		for (j = i - gap; j>= 0 &&a[j] >a[j + gap]; j -= gap){
            swap(a, j, j + gap);
        }
    }while(gap>1);		
}
/****************************blog****************************************/



/*****************************itcast**************************************/
//nlogn
void ShellSort(int array[], int len) //
{
	int i = 0;
	int j = 0;
	int k = -1;
	int temp = -1;
	int gap = len;
	do
	{
		 //业界统一实验的 平均最好情况 经过若干次后，收敛为1
		//gap = gap / 3 + 1; //gap /2345 2000 都行  //O（n 1.3）
        gap = gap / 2;// 此例使用gap = gap / 2; 优于使用 gap = gap / 3 + 1;
	
		for(i=gap; i<len; i+=gap)
		{
			k = i;
			temp = array[k];

			for(j=i-gap; (j>=0) && (array[j]>temp); j-=gap)
			{
				array[j+gap] = array[j];
				k = j;
			}

			array[k] = temp;
		}

	}while( gap > 1 );
}
/*****************************itcast**************************************/

int main()
{
	int array[] = {49, 38, 65, 97, 26, 13, 27, 49, 55, 4};
	int len = sizeof(array) / sizeof(*array); 

    struct timespec tStart,tEnd;
    long timeElapse; //变量保存程序耗费时间

	println(array, len);
    printf("\n");
    clock_gettime(CLOCK_MONOTONIC   , &tStart);

    //shellsort1(array, len); //600ns
    //shellsort2(array, len); //400ns
    //shellsort3(array, len); //400ns
    //shellsort3_while(array, len);
	ShellSort(array, len); //800ns
    
    clock_gettime(CLOCK_MONOTONIC   , &tEnd);
    timeElapse = tEnd.tv_nsec - tStart.tv_nsec;//?以纳秒来计数

    printf(" Start_ns :  %ldns\n End_ns   :  %ldns\n Elapse_ns:  %ldns\n",tEnd.tv_nsec, tStart.tv_nsec, timeElapse);//
    printf("\n");
	println(array, len); 
	system("pause");
	return 0;
}

```

