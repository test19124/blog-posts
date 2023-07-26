---
title: '517最大余数题解'
date: 2021-08-10 21:39:55
tags: [517提高组]
categories: 
- [编程,题解]
---
# 最大余数-第一课: 枚举技巧-状压/折半/尺取法-2020最新版提高组初级课程

[题目链接](https://517coding.com/p/3980)

## 思路

折半 + 二进制枚举

注意b数组要排个序~

<!-- more -->

## 代码

```cpp
#include <bits/stdc++.h>
using namespace std;

int n,mod;
int a[1000010];
int b[1000010];
int tot;

int find(int x)
{
  int ans=-1;
  int l=0,r=tot-1;
  if(b[r]<=x) {
    return b[r];
  }
  while(l<=r) {
    int mid=(l+r)/2;
    if(b[mid]<=x) {
      ans=b[mid];
      l=mid+1;
    } else {
      r=mid-1;
    }
  }
  return ans;
}


int main() {
  scanf("%d%d",&n,&mod);
  for(int i=0;i<n;i++) {
    scanf("%d",&a[i]);
    a[i]%=mod;
  }
  int m=n/2;
  for(int i=0;i<(1<<m);i++) {
    int tmp=0;
    for(int j=0;j<m;j++) {
      if(i&(1<<j)) {
        tmp=(tmp+a[j])%mod;
      }
    }
    b[tot++]=tmp;
  }
  sort(b,b+tot);
  m=n-(n/2);
  int ans=0;
  for(int i=0;i<(1<<m);i++) {
    int tmp=0;
    for(int j=0;j<m;j++) {
      if(i&(1<<j)) {
        int jj=j+n/2;
        tmp=(tmp+a[jj])%mod;
      }
    }
    int x=find(mod-tmp-1);
    ans=max(ans,(x+tmp));
    if(ans==mod-1) {
      break;
    }
  }
  cout<<ans<<"\n";
  return 0;
}
```
