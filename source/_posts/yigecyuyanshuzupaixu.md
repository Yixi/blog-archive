title: 给一个C语言数组排序
tags:
  - C语言
  - 函数
id: 218
categories:
  - C/C++ Programming
date: 2009-06-30 19:31:53
---

这是上次帮226的人做专周的一个子函数，里面有个排序的函数，自认为对于入门还不错。

因为这是一个程序管理系统，这个排序是用来排名次的一个小功能，只是其中的一个子函数，故在这里先说下函数前提。

首先是数据，数据是写到一个文件中的，输出大概就是这么个形式。

 ![数据结构图](http://blog.liuyixi.com/wp-content/uploads/2009/06/12331.jpg "数据结构图")

然后将这个数据赋值到一个 float score[10][8] 的数组中。

在main() 函数中：

   首先赋值   int   n=10； //n为学生人数。

下面是排序函数的代码：
<pre lang="c" line="1" file="paixu.txt" colla="+">void fun3(float score[][8],int n)    //排序函数
{
	int i,j,k;
	float temp[10][3],x[3];        //定义了一个临时二维数组和一个一维数组
	for (i=0;i&lt;n;i++)
	{
		temp[i][0]=score[i][0];    //将学号赋给临时二维数组的0列
		temp[i][1]=score[i][6];    //将总分赋给临时二维数组的1列
	}
	for (i=0;i&lt;n;i++)              /*条件也可为：i&lt;n-1*/
	{
		k=i;
		for (j=i+1;j&lt;n;j++)
			if (temp[j][1]&gt;temp[k][1])
				k=j;
			if (i!=k)                /*此语句不要也可*/
			{
				x[0]=temp[k][0];     //以下就是交换学号和总分
				x[1]=temp[k][1];
				x[2]=temp[k][2];     /*些语句不要也可*/
				temp[k][0]=temp[i][0];
				temp[k][1]=temp[i][1];
				temp[k][2]=temp[i][2];
				temp[i][0]=x[0];
				temp[i][1]=x[1];
				temp[i][2]=x[2];    /*些语句不要也可*/
			}
	}
	j=1;
	temp[0][2]=j;
	for (i=1;i&lt;n;i++)
		if (temp[i][1]==temp[i-1][1])
			temp[i][2]=j;
		else
		{
			j++;temp[i][2]=j;
		}
	printf("按总分排列的名次\n");
	printf("原学号    总分    名次\n");
	for (i=0;i&lt;n;i++)
		printf("%4g%10g%7g\n",temp[i][0],temp[i][1],temp[i][2]);
}</pre>
嗯，排序函数就是这样，数组的排序，有很多种方式，这只是一种。