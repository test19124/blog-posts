---
title: '517雷达题解'
date: 2021-08-10 21:43:33
tags: [517提高组]
categories: 
- [编程,题解]
---
# 雷达-第二课: 贪心算法-区间覆盖/字典序-2020最新版提高组初级课程

[题目链接](https://517coding.com/p/4000)

## 思路

用勾股定理求出区间

转化成区间覆盖问题

<!-- more -->

## 代码

```cpp
#include <bits/stdc++.h>
using namespace std;

struct jgt
{
  int x,y;
  double z;
} a[100010];

bool cmp(jgt a,jgt b) {
  return a.z<b.z;
}

int n,d,ans=1;
int main()
{
  cin>>n>>d;
  bool flag=false;
  for(int i=1;i<=n;i++) {
    cin>>a[i].x>>a[i].y;
    //cout<<a[i].x<<" "<<a[i].y<<endl;
    if(a[i].y>d||a[i].y<(-1*d)) {
      flag=true;
    }
    a[i].z=a[i].x+sqrt(d*d-a[i].y*a[i].y);
  }
  if(flag) {
    cout<<-1<<"\n";
    return 0;
  }
  sort(a+1,a+n+1,cmp);
  double tmp=a[1].z;
  for(int i=2;i<=n;i++) {
    if((a[i].x-tmp)*(a[i].x-tmp)+a[i].y*a[i].y>d*d) { 
      ans++;
      tmp=a[i].z;
    }
  }
  cout<<ans<<"\n";
  return 0;
}
```
