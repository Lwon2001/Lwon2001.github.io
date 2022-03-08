---
title: Welcome
tags: TeXt
---

## scanf的正则用法的常见问题
```c
    scanf("%d %d",&m,&n);
    char a[256];
    scanf("%[^\n]%*c",a);
    //输入为
    //2 6
	//ABCDEFGH 12345
```
如上，再scanf正则用法前,如果已经有输入,并且输入结尾会包含一个回车(换行符)，那么这个回车会作为后面一个scanf的输入，即将后面scanf的正则用法给取消了
    解决该问题的办法就是再上一个读入结束后加一个getchar();将最后的回车吃掉；如下

```c
    scanf("%d %d",&m,&n);
    getchar();
    char a[256];
    scanf("%[^\n]%*c",a);
```



