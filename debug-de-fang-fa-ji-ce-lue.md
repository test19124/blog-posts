---
title: 'debug的方法及策略'
date: 2021-08-09 20:02:42
tags: [DEBUG]
categories: [编程]
---
C++以及普及组选手多使用静态查错法与输出调试法

提高组选手可以适当使用对拍调试法

[https://www.bilibili.com/video/BV1sQ4y1K7T4/ 初级调试指南视频版]

[https://www.bilibili.com/video/BV1he411p74Y/ 高级调试指南视频版]

= 调试指南 =

1：在草稿纸上模拟程序的运行，写下一些关键变量的中间结果

2：利用打印调试法打印出这些中间变量的值

3：对比观察

<!-- more -->

下面介绍利用数据去查错的几种查错方法

== 静态查错法 ==

静态查错法的意思是说，写完程序，先整体浏览一遍代码，把一些肉眼可见的，明显发现是错的地方修改掉

根据以往的经验，我们发现，一个选手功力越深，静态查错的时候能发现的问题越多，往往大多数错误不需要下面的方法就已经查出来了。

== 输出调试法 ==

首先，我们运行了一组数据，发现结果不对，然后静态查错也没看出什么来，这个时候我们采用输出调试法。

1：先 分段  打印一些变量，观察变量的值跟预想的对不对，找到最先不对的地方，然后检查，这个时候下面的代码就不用看了

2：不停的重复1的行为，不断的缩小定位错误区域，直到所有的错误修复完毕

举个例子

比如下面这个程序, 题库链接：https://517coding.com/p/1100

```c++
#include<bits/stdc++.h>
using namespace std;
int a[10010];
int b[10010];
int main(void){
	int n,m;
	int k=-1e9;
	scanf("%d%d",&n,&m);
	for(int i=1;i<=n;i++) scanf("%d",&a[i]);
	for(int i=1;i<=m;i++) scanf("%d",&b[i]);
	for(int i=1;i<=n;i++) {
		for(int j=1;j<=n;j++) {
		    
			if(a[i]+b[j]>k) { 
		//下面这行代码是用来打印调试的语句
			     printf("i=%d j=%d sum=%d\n", i, j, a[i]+b[j]);
			     k=a[i]+b[j];
			}
		}
       }
	printf("%d",k);
	return 0;
}

/*
错误数据：

2 3
1 2
1 2 3
*/
```

我们可以在循环里面加一句printf语句打印关键信息，然后运行代码下方的错误数据，我们发现会输出如下信息

```c++
2 3
1 2
1 2 3
i=1 j=1 sum=2
i=1 j=2 sum=3
i=2 j=2 sum=4
4
```

可以发现，答案明明是5，但是却输出了4，而且中间过程也并没有产生5，而答案5是来自于第一个数组中的2与第二个数组中的3相加得到的，此时我们通过调试信息的输出并没有发现这两个数被同时枚举到，于是我们检查两个for循环，这个时候发现了两个for循环枚举的都是1到n，而实际上，第二个循环应该枚举1到m，修改之后，这个程序就可以正常通过了

== 对拍调试法 ==

=== duipai.sh ===

```sh
#!/bin/bash
t=0;
while true; do
    let "t = $t + 1"
    printf $t
    printf ":\n"
    ./rand > rand.txt
    ./AC < rand.txt > AC.out
    ./WA < rand.txt > WA.out
   
    if diff AC.out WA.out; then
        printf "\n"
    else
        printf "WA\n"
        cat rand.txt
        break
    fi
done
```

=== run.bat ===

```bat
:loop 
    @echo off   
    gen.exe > in.txt                     
    my.exe < in.txt  > myout.txt     
    std.exe < in.txt  > stdout.txt
    fc myout.txt stdout.txt              
if not errorlevel 1   goto loop         
pause
```

=== std.cpp ===

```c++
#include <bits/stdc++.h>
using namespace std;

int main() {
  int a, b;
  cin >> a >> b;
  cout << a + b << endl;
  return 0;
}
```

=== my.cpp ===

```c++
#include <bits/stdc++.h>
using namespace std;

//这是一个错误程序
int main() {
  int a, b;
  cin >> a >>b;
  if (a > 130 && b > 130) {
    cout << a - b << endl;
  } else {
    cout << a + b << endl;
  }
  return 0;
}
```

=== gen.cpp ===

```c++
#include <bits/stdc++.h>
using namespace std;

// 返回0到x-1之间的随机数
// rand()函数返回 0-32767之间的一个随机数
int get_rand(int x) {
  return rand() * rand() % x + 1;
}

//返回L 到 R之间的整数
int get_rand(int L, int R) {
  return rand() * rand() % (R-L+1) + L;
}

int main() {
  //初始化随机种子
  srand(time(0));
  int a, b;

  //生成一组随机数据
  a = get_rand(1, 200);
  b = get_rand(1, 200);
  cout << a << " " << b <<endl;
  return 0;
}

```
