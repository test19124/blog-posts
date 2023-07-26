---
title: '517迷宫题解'
date: 2021-07-24 17:15:46
tags: [517普及组]
categories: 
- [编程,题解]
---
# 迷宫-第四课：广搜-【中级班】517编程普及组

[迷宫-第四课：广搜-【中级班】517编程普及组 ](https://517coding.com/contest/problem?id=498&pid=1#problem-anchor)

## 做法1 - 在队列中记录层的分界线

### 思路

$ru$记录当前层的最后一个节点，如果被访问到的节点==$ru$ 说明这一层的所有节点都被访问到

也就说明了这一层的所有节点的子节点（$k+1$层的所有节点）都已入队列，此时$ru$应更新为队尾元素

### 易错点

如果$ru$出现多次应该在最后一次出现时更新$ru$

即，在入栈的同时就标记被访问过（$a_{i,j}=1$），不是访问到再标记！

<!-- more -->

### 代码

```c++
#include <bits/stdc++.h>
using namespace std;

int n,m;
int a[1010][1010];
int ans;
int tx,ty;

int X[4]={1,-1,0,0};
int Y[4]={0,0,1,-1};

struct zb {
  int x;
  int y;
};
queue<zb>b;

bool operator==(const zb &a,const zb &b) {
  if(a.x==b.x&&a.y==b.y) {
    return true;
  }
  return false;
}

void outzb(zb b) {
  cout<<"x="<<b.x<<" y="<<b.y<<endl;
  return;
}

void out(/*zb x*/) {
  for(int i=1;i<=n;i++) {
    for(int j=1;j<=m;j++) {
      cout<<int(a[i][j]);
    }
    cout<<endl;
  }
  //cout<<"x="<<x.x<<" y="<<x.y;
  cout<<"ans="<<ans<<endl;
  cout<<endl;
}

bool bfs(int x,int y) {
  zb l,k,h;
  int xx,yy;
  l.x=x;l.y=y;
  b.push(l);
  zb ru=l;
  while(!b.empty()) {
    k=b.front();
    b.pop();
    if(k.x==tx&&k.y==ty) {
      return true;
    }
    //out(k);
    for(int i=0;i<4;i++) {
      h.x=xx=k.x+X[i];
      h.y=yy=k.y+Y[i];
      if(xx<=0||xx>n||yy<=0||yy>m||a[xx][yy]==1);
      else {
        b.push(h);
        a[xx][yy]=1;
      }
    }
    if(k==ru) {
      ru=b.back();
      ans++;
    }
    //out();
  }
  return false;
}

int main() {
  char c;
  int x,y;
  cin>>n>>m;
  for(int i=1;i<=n;i++) {
    for(int j=1;j<=m;j++) {
      cin>>c;
      if(c=='S') {
        x=i;
        y=j;
        a[i][j]=1;
      } else if(c=='T') {
        tx=i;
        ty=j;
      } else if(c=='#') {
        a[i][j]=1;
      }
    }
  }
  if(bfs(x,y)) {
    cout<<ans<<endl;
  } else {
    cout<<"-1"<<endl;
  }
  return 0;
}
```

## 做法2 - 数组记录每个节点的层数

### 思路

直接开数组 $a_{i,j}$ 来判断此时层数（墙记录 $a_{i,j}=-1$ )

### 代码

```c++
#include <bits/stdc++.h>
using namespace std;

int n,m;
int a[1010][1010];
int tx,ty;

int X[4]={1,-1,0,0};
int Y[4]={0,0,1,-1};

struct zb {
  int x;
  int y;
};
queue<zb>b;

bool operator==(const zb &a,const zb &b) {
  if(a.x==b.x&&a.y==b.y) {
    return true;
  }
  return false;
}
void outzb(zb b) {
  cout<<"x="<<b.x<<" y="<<b.y<<endl;
  return;
}

void out(zb x) {
  for(int i=1;i<=n;i++) {
    for(int j=1;j<=m;j++) {
      cout<<int(a[i][j]);
    }
    cout<<endl;
  }
  cout<<"x="<<x.x<<" y="<<x.y<<endl;
  cout<<endl;
}

bool bfs(int x,int y) {
  zb l,k,h;
  int xx,yy;
  l.x=x;l.y=y;
  b.push(l);
  while(!b.empty()) {
    k=b.front(); b.pop(); // 取出队首
    if(k.x==tx&&k.y==ty) { // 找到终点
      return true; //返回
    }
    //out(k);
    for(int i=0;i<4;i++) { // 枚举上下左右
      h.x=xx=k.x+X[i];
      h.y=yy=k.y+Y[i];
      if(xx<=0||xx>n||yy<=0||yy>m||a[xx][yy]!=0);
      else {
        b.push(h);
        a[h.x][h.y]=a[k.x][k.y]+1;
      }
    }
    //outzb(ru);
    //cout<<endl;
  }
  return false;
}

int main() {
  cin>>n>>m;
  char c;
  int x,y;
  for(int i=1;i<=n;i++) {
    for(int j=1;j<=m;j++) {
      cin>>c;
      if(c=='S') {
        x=i;
        y=j;
      } else if(c=='T') {
        tx=i;
        ty=j;
      } else if(c=='#') {
        a[i][j]=-1;
      }
    }
  }
  if(bfs(x,y)) {
    cout<<a[tx][ty]<<endl;
  } else {
    cout<<"-1"<<endl;
  }
  return 0;
}
```
