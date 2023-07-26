---
title: '517有负环最短路径题解'
date: 2021-08-06 17:14:51
tags: [517普及组]
categories: 
- [编程,题解]
---
# 有负环最短路径-第十课：最短路径-【中级班】517编程普及组

## 描述

> 给定一个有向图，求1到n的最短路径。
> 可以判断图中是否有负环。

<!-- more -->

## 输入

> 第一行两个整数n和m，表示点数和边数。
> 接下来m行，每行3个整数，表示一条有向边。

## 输出

> 如果图中有负环，输出circle
> 如果没有负环，但是从1无法到达n，输出 can't arrive!
> 否则输出 1到n的最短距离

## 样例

### 输入#1

```txt
3 3
1 3 3
1 2 1
2 3 1
```

### 输出#1

```txt
2
```

### 输入#2

```txt
3 3
1 2 1
2 1 -2
2 3 1
```

### 输出#2

```txt
circle
```

### 输入#3

```txt
3 2
1 2 1
2 1 1
```

### 输出#3

```txt
can't arrive!
```

## 提示

> n≤200
> m≤2000

---

## 思路

这题就是标准负环最短路

## 易错点

1. 中转边必须有边才能转移：`if(g[u][i]!=998244353&&g[i][v]!=998244353)`
2. `g[u][v]` 可以等于 `998244353`

## 代码

```cpp
#include <bits/stdc++.h>
using namespace std;

int g[210][210];

int main() {
  int n,m;
  cin>>n>>m;
  for(int i=1; i<=n; i++) {
    for(int j=1; j<=n; j++) {
      if(i!=j) {
        g[i][j]=998244353;
      }
    }
  }
  int u,v,w;
  for(int i=1; i<=m; i++) {
    cin>>u>>v>>w;
    g[u][v]=min(w,g[u][v]);
  }
  for(int i=1; i<=n; i++) {
    for(int u=1; u<=n; u++) {
      for(int v=1; v<=n; v++) {
        if(g[u][i]!=998244353&&g[i][v]!=998244353) {
          if(g[u][i]+g[i][v]<g[u][v]) {
            g[u][v]=g[u][i]+g[i][v];
          }
        }
      }
      if(g[u][u]<0) {
        cout<<"circle"<<endl;
        return 0;
      }
    }
  }
  if(g[1][n]==998244353) {
    cout<<"can't arrive!\n";
  } else {
    cout<<g[1][n]<<"\n";
  }
  return 0;
}
```
