---
title: '517最小字典序题解'
date: 2021-08-10 21:31:51
tags: [517提高组]
categories: 
- [编程,题解]
---
# 最大余数-第二课: 贪心算法-区间覆盖/字典序-2020最新版提高组初级课程

[题目链接](https://517coding.com/p/3980)

## 思路

两边取小的往内贪心

如果相同则比较下一层大小

<!-- more -->

## 代码

```cpp
#include <bits/stdc++.h>
using namespace std;

int n,tot;
char a[2010];

int main() {
  scanf("%d%s",&n,&a);
  int l=0,r=n-1;
  while(l<=r) {
    bool flag;
    for(int i=0;i<=r-l;i++) {
      if(a[l+i]!=a[r-i]) {
        flag=a[l+i]<a[r-i];
        break;
      }
    }
    if(flag) {
      printf("%c",a[l]);
      l++;
    } else {
      printf("%c",a[r]);
      r--;
    }
    tot++;
    if(tot%80==0) {
      printf("\n");
    }
  }
  return 0;
}
```
