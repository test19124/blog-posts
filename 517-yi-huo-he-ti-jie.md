---
title: '517异或和题解'
date: 2021-08-10 21:22:46
tags: [517提高组]
categories: 
- [编程,题解]
---
# 按钮变色-第一课: 枚举技巧-状压/折半/尺取法-2020最新版提高组初级课程

[题目链接](https://517coding.com/p/3970)

## 思路

尺取法加强，记得开long long

<!-- more -->

## 代码

```cpp
#include <bits/stdc++.h>
using namespace std;

int n,s;
int a[1200000];
long long suma[1200000];
long long sumb[1200000];

int main()
{
  scanf("%d",&n);
  for(int i=1;i<=n;i++) {
    scanf("%d", &a[i]);
    suma[i]=suma[i-1]+a[i];
    sumb[i]=sumb[i-1]^a[i];
  }
  long long ans=0;
  int i=1;
  for(int j=1;j<=n;j++) {
    while(suma[j]-suma[i-1]!=(sumb[j]^sumb[i-1])) {
      i++;
    }
    ans+=j-i+1;
  }
  printf("%lld\n", ans);
  return 0;
}
```
