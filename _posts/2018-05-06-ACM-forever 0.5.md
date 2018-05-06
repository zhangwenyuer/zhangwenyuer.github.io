---
layout: post
title: 第四届福建省大学生程序设计竞赛--A题
date: 2018-05-05
categories: 算法
tags: 算法 ACM
cover: '/assets/img/hero.jpg'
---
# 来自今天下午的比赛

*一道找规律的题*

* 题目

## 描述
Given an integer N, your task is to judge whether there exist N points in the plane such that satisfy the following conditions:

1. The distance between any two points is no greater than 1.0.

2. The distance between any point and the origin (0,0) is no greater than 1.0.

3. There are exactly N pairs of the points that their distance is exactly 1.0.

4. The area of the convex hull constituted by these N points is no less than 0.5.

5. The area of the convex hull constituted by these N points is no greater than 0.75.

## Input


The first line of the date is an integer T, which is the number of the text cases.

Then T cases follow, each contains an integer N described above.

1 <= T <= 100, 1 <= N <= 100

## Output

For each case, output “Yes” if this kind of set of points exists, then output N lines described these N points with its coordinate. Make true that each coordinate of your output should be a real number with AT MOST 6 digits after decimal point.

Your answer will be accepted if your absolute error for each number is no more than 10-4.

Otherwise just output “No”.

See the sample input and output for more details.

## Sample Input
3

2

3

5

## Sample Output
No

No

Yes

0.000000 0.525731

-0.500000 0.162460

-0.309017 -0.425325

0.309017 -0.425325

0.500000 0.162460
* 题目解析

一共有T个测试样例，每个样例输入一个n代表有几个点，这几点要满足以下几个条件：

1.每两个点之间的距离不超过1.0

2.每个点到原点的距离不超过1.0

3.存在n对点，他们之间的距离为1.0

4.这些点构成的凸多边形的面积不小于0.5

5.这些点构成的凸多边形的面积不大于0.75


首先我拿到这个题呢，看了一下样例，就觉得是应该要构成正多边形，然后利用三角函数去计算每个点的坐标。然后z发现这样很复杂，无法实现，所以放弃这个思路。

然后发现一个以原点为其中一个顶点的边长为1的正三角形，另外两个点正好在以原点为圆心1为半径的圆的圆弧上，在这两个点之间的圆弧上加任意个数的点都满足以上的前三个条件。

最后就是要解决后面两个面积的问题，1个点和2个点无法构成多边形，3个点的时候计算了面积为√3/4(小于0.5)，不满足条件。4个点的时候将第4个点的位置放在（0，-1）上面积刚好为0.5，满足条件，所以我们把第4个点以及之后的点都放在这个位置上就解决了。

* 代码展示

``` clike
#include <iostream>
#include <string.h>
#include <stdlib.h>
#include <algorithm>
#include <math.h>
#include <stdio.h>
using namespace std;
int main()
{
	int T,n;
    cin>>T;
    while(T--){
        cin>>n;
        if(n<=3)
            cout<<"No"<<endl;
        else{
            cout<<"Yes"<<endl;

            cout<<"0.000000 0.000000"<<endl;
            printf("0.500000 %.6f\n",-1.0*sqrt(3.0)/2);
            printf("-0.500000 %.6f\n",-1.0*sqrt(3.0)/2);
            for(int i=1;i<=n-3;i++)
                cout<<"-0.000000 -1.000000"<<endl;
        }
    }
    return 0;
}

```