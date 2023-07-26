---
title: '517倒酒题解'
date: 2021-08-01 10:50:11
tags: [517普及组]
categories: 
- [编程,题解]
---
# 倒酒-第四课：广搜-【中级班】517编程普及组

![倒酒-第四课：广搜-【中级班】517编程普及组](https://i.loli.net/2021/07/26/XIlbcxZomf79Bve.png)

思路：广搜

<!-- more -->

```c++
#include <bits/stdc++.h>
using namespace std; 

int a[3];
int vis[160][160][160]; 

struct jgt {
  int a[3];
  int ans;
}; 
queue<jgt>q;

bool find(jgt f) { // 均分
  if(f.a[0]==f.a[1]&&f.a[2]==0)
    return true;
  if(f.a[0]==f.a[2]&&f.a[1]==0)
    return true;
  if(f.a[1]==f.a[2]&&f.a[0]==0)
    return true;
  return false;
} 

jgt push(int a,int b,int c,int ans) { // 入队
  jgt x;
  vis[a][b][c]=true;
  x.a[0]=a;
  x.a[1]=b;
  x.a[2]=c;
  x.ans=ans;
  q.push(x);
  return x;
}

void copy(jgt &a,jgt b) { // 拷贝
  for(int i=0;i<3;i++) {
    a.a[i]=b.a[i];
  }
  a.ans=b.ans;
}

void bfs() {
  jgt k,l;  // 定义
  push(a[0],0,0,0); // 初始数据入队
  while(!q.empty()) { // 队列不为空
    k=q.front(); // 取出队首
    q.pop(); // 删除队首
    for(int i=0; i<3; i++) { // 枚举准备倒的杯
      for(int j=0; j<3; j++) { // 枚举被倒的杯
        if(i!=j) { // 不能倒给自己
          if(find(k)) { // 如果当前已均分
            cout<<k.ans<<endl; // 输出
            return;// 结束函数
          }
          copy(l,k); // 拷贝k到l
          int x=a[j]-l.a[j]; // x=原先被倒的杯里的酒-现在这个杯里的酒
          if(l.a[i]>=x) { // 如果溢出
            l.a[j]=a[j]; // 灌满被倒的杯
            l.a[i]-=x; // 剩余的酒留在杯中
          } else { // 否则
            l.a[j]+=l.a[i]; // 全倒过去
            l.a[i]=0; // 原来的杯清零
          }
          l.ans++; // 倒的次数++
          if(vis[l.a[0]][l.a[1]][l.a[2]]==false) { // 当前状态没有被记录
            vis[l.a[0]][l.a[1]][l.a[2]]=true; // 记录当前状态
            q.push(l); // 记录入队
          }
        }
      }
    }
  }
  //没办法平均分
  cout<<"NO"<<endl;
}

int main() {
  for(int i=0;i<3;i++) {
    cin>>a[i];
  }
  bfs();
  return 0;
}
```
