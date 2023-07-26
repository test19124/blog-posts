---
title: '517按钮变色题解'
date: 2021-08-07 19:59:11
tags: [517提高组]
categories: 
- [编程,题解]
---
# 按钮变色-第一课: 枚举技巧-状压/折半/尺取法-2020最新版提高组初级课程

[题目链接](https://517coding.com/p/3951)

## 思路

暴力dfs

易证：每个点最多会被翻转一次（2次不就翻回来了吗qwq）

dfs枚举每个点是否会被翻，查看当前是否全部同色

<!-- more -->

## 代码

```cpp
#include <bits/stdc++.h>
using namespace std;

char a[10][10];
int X[5]={0,0,0,1,-1};
int Y[5]={0,1,-1,0,0};
map<char,char>b;

void change(int x,int y) {
  int xx,yy;
  for(int i=0;i<5;i++) {
    xx=x+X[i];
    yy=y+Y[i];
    if(xx>=0&&xx<4&&yy>=0&&yy<4) {
      a[xx][yy]=b[a[xx][yy]];
    }
  }
}

bool find() {
  int x=0;
  for(int i=0;i<4;i++) {
    for(int j=0;j<4;j++) {
      x+=(a[i][j]=='w');
    }
  }
  return (x==0||x==16);
}

int ans=998244353;

void dfs(int x,int ansx) {
  if(x==16) {
    if(find()) {
      if(ansx < ans) {
        ans=ansx;
      }
    }
    return;
  }
  dfs(x+1,ansx);
  change(x/4,x%4);
  dfs(x+1,ansx+1);
  change(x/4,x%4);
}

int main() {
  b['w']='b';
  b['b']='w';
  for(int i=0;i<4;i++) {
    scanf("%s",a[i]);
  }
  dfs(0,0);
  if(ans==998244353) {
    printf("Impossible");
  } else {
    printf("%d",ans);
  }
  return 0;
}
```
