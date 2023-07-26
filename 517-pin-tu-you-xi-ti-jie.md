---
title: '517拼图游戏题解'
date: 2021-08-01 10:55:04
tags: [517普及组]
categories: 
- [编程,题解]
---
# 拼图游戏-第四课：广搜-【中级班】517编程普及组

![拼图游戏-第四课：广搜-【中级班】517编程普及组](https://i.loli.net/2021/07/25/4xMjbA9NZi2sHVD.png)

<!-- more -->

```c++
#include <bits/stdc++.h>
using namespace std;

int mod=1000007;
int ji[1000010];
int top;
int me[1000010],to[1000010];

int X[4]={0,1};
int Y[4]={1,0};

struct zb {
  int a[5][5];
  int ans;
};
queue<zb>q;

void out(int a[5][5]) {
  for(int i=1;i<=3;i++) {
    for(int j=1;j<=3;j++) {
      cout<<a[i][j];
    }
    cout<<endl;
  }
}

void outji() {
  cout<<top<<endl;
  for(int i=0;i<mod;i++) {
    if(ji[i]) {
      for(int j=ji[i];;j=to[j]) {
        cout<<me[j]<<"-->";
        if(to[j]==0) {
          break;
        }
      }
      cout<<ji[i]<<endl;
    }
  }
}

int copy(int &a,int b[5][5]) {
  a=0;
  for(int i=1;i<=3;i++) {
    for(int j=1;j<=3;j++) {
      a=a*10+b[i][j];
    }
  }
  return a;
}

bool find(int x) {
  for(int i=ji[x%mod];to[i]!=0;i=to[i]) {
    if(me[i]==x) {
      return true;
    }
  }
  return false;
}

void in(int x) {
  if(ji[x%mod]==0) {
    top++;
    ji[x%mod]=top;
    me[top]=x;
    return;
  }
  for(int i=ji[x%mod];;i=to[i]) {
    if(to[i]==0) {
      top++;
      to[i]=top;
      me[top]=x;
      return;
    }
  }
}

zb push(int a[5][5],int ans) {
  zb x;
  for(int i=1;i<=3;i++) {
    for(int j=1;j<=3;j++) {
      x.a[i][j]=a[i][j];
    }
  }
  x.ans=ans;
  q.push(x);
  return x;
}

int bfs(int a[5][5]) {
  
  zb k;
  int h;
  
  push(a,0);
  in(copy(h,a));
  
  while(!q.empty()) {
  
    k=q.front();
    q.pop();
  
    copy(h,k.a);
    if(h==12345678) {
      return k.ans;
    }

    //cout<<k.ans<<endl;
    //out(k.a);
  
    for(int x=1;x<=3;x++) {
      for(int y=1;y<=3;y++) {
        for(int i=0;i<2;i++) {
          if(x+X[i]>3||y+Y[i]>3);
          else {
            swap(k.a[x][y],k.a[x+X[i]][y+Y[i]]);
            copy(h,k.a);
            if(!find(h)) {
              in(h);
              push(k.a,k.ans+1);
            }
            swap(k.a[x][y],k.a[x+X[i]][y+Y[i]]);
          }
        }
        /*
        if(find()) {
          return;
        }
        for(int i=0;i<4;i++) {
          if(x+X[i]<=0||y+Y[i]<=0||x+X[i]>3||y+Y[i]>3||vis[x+X[i]][y+Y[i]]);
          else {
            vis[x][y]=true;
            dfs(x+X[i],y+Y[i]);
            swap(a[x][y],a[x+X[i]][y+Y[i]]);
            //cout<<"swap "<<a[x][y]<<" and "<<a[x+X[i]][y+Y[i]]<<endl;
            dfs(x+X[i],y+Y[i],ansx+1);
            swap(a[x][y],a[x+X[i]][y+Y[i]]);
            vis[x][y]=false;
          }
        }
        if(l==k) {
          l=q.back();
          ans++;
        }
        */
      }
    }
    //outji();
  }
  return 0;
}

int main() {
  
  int x;
  int a[5][5];
  
  for(int i=1;i<=3;i++) {
    cin>>x;
    for(int j=3;j>=1;j--) {
      a[i][j]=x%10;
      x/=10;
    }
  }
  
  int ans;
  copy(ans,a);
  if(ans==12345678) {
    cout<<0<<endl;
  } else {
    cout<<bfs(a)<<endl;
  }
  
  return 0;
}
```
