---
title: '517覆盖数轴题解'
date: 2021-08-07 14:37:42
tags: [517普及组]
categories: 
- [编程,题解]
---
# 覆盖数轴-第二课：贪心算法-【中级班】517编程普及组

## 描述

> 有一个长度为m的数轴，现在有n个区间，每个区间有一个左右端点，现在需要选择最少的区间，覆盖整个数轴。

<!-- more -->

## 输入

> 第一行两个整数n和m
> 接下来n行，每行两个整数，表示区间。

## 输出

> 输出最少的区间个数，覆盖整个数轴。如果无法覆盖，输出-1

## 样例

### 输入#1

```txt
5 6
1 3
2 4
3 5
5 6
1 4
```

### 输出#1

```txt
2
```

## 思路

贪心，先按右侧端点排序
之后再取 左侧端点<=右侧端点+1 的所有线段中右侧端点最远的点
达到 m 结束

## 易错点

1. 左侧端点<=右侧端点 **+1**
2. 取所有线段中右侧端点最远的点

## 代码

```cpp
#include <bits/stdc++.h>
using namespace std;
int n,m;
struct qj {
  int s,t;
} a[100010];
bool cmp(qj a,qj b) {
  if(a.s==b.s) {
    return a.t<b.t;
  }
  return a.s<b.s;
}
int main() {
  cin>>n>>m;
  for(int i=1;i<=n;i++) {
    cin>>a[i].s>>a[i].t;
  }
  sort(a+1,a+n+1,cmp);
  int t=0,ans=0,Max,x=1,flag=0;
  for(int i=2;i<=n;i++) {
    Max=0;
    while(a[x].s<=(t+1)&&x<=n) {
      Max=max(Max,a[x].t);
      x++;
    }
    t=Max;
    ans++;
    if(t>=m) {
      flag=1;
      break;
    }
  }
  if(flag) {
    cout<<ans<<endl;
  } else {
    cout<<-1<<endl;
  }
  return 0;
}
```
