---
title: '517最短连续子序列题解'
date: 2021-08-10 21:18:16
tags: [517提高组]
categories: 
- [编程,题解]
---
# 最短连续子序列-第一课: 枚举技巧-状压/折半/尺取法-2020最新版提高组初级课程

[题目链接](https://517coding.com/p/3960)

## 思路

尺取法

<!-- more -->

## 代码

```cpp
#include <bits/stdc++.h>
using namespace std;

int n,s;
int sum[1200000];
int a[1200000];

int main()
{
  scanf("%d%d",&n,&s);
  for(int i=1;i<=n;i++) {
    scanf("%d", &a[i]);
    sum[i]=sum[i-1]+a[i];
  }
  int ans=998244353,i=1;
  for(int j=1;j<=n;j++) {
    if(sum[j]-sum[i-1]>=s) {
      while(sum[j]-sum[i]>=s) {
        i++;
      }
      ans=min(ans,j-i+1);
    }
  }
  if(ans==998244353)
    printf("0\n");
  else
    printf("%d\n", ans);
  return 0;
}
```
