
# quilt 简介

想对openwrt做一点修改，把这些修改做成patch提交。于是遇到了quilt这个东西。

## quilt的安装

sudo apt-get install quilt

quilt本身是一个脚本，上面这一句把它安装于/usb/bin/quilt

quilt 的执行方式是：

> quilt command ...

command有如下选择:
```
add       fold    new       remove    top
annotate  fork    next      rename    unapplied
applied   graph   patches   revert    upgrade
delete    grep    pop       series
diff      header  previous  setup
edit      import  push      shell
files     mail    refresh   snapshot
```

其中每一个command都是/usr/share/quilt/目录下的一个以command命名的脚本。

## quilt基本使用

0. test目录下有两个文件file1.c file1.h

1. 创建一个新patch
> quilt new 0001-test.patch

2. 把文件加入到topmost patch
> quilt add file1.c

接下来对int.c的修改都会记录到topmost patch中去。

3. 编辑文件
使用编辑器修改源文件，也可以调用quilt的默认编译器来修改int.c。
> quilt edit file1.c

4. 更新topmost patch
> quilt refresh

使用了这条命令之后，修改才会写入到0001-test.patch中

5. 继续新建一个patch
> quilt new 0002-test.patch

此时topmost变成了0002-test.patch。
现在使用`quilt files`查看，此patch下没有跟踪文件

6. 添加两个文件file1.c file1.h
> quilt add file1.c file1.h

现在使用`quilt files`查看，此patch跟踪了两个文件。编辑它们。

7. pop/push

回退到某个patch
```
$ quilt pop 0001-test.patch 
Removing patch 0002-test.patch
Restoring file1.c
Restoring file1.h

Now at patch 0001-test.patch
```
这个命令之后，0001-test.patch将变为topmost patch。所有的修改退回到这个点上。

```
$ quilt push 0002-test.patch 
Applying patch 0002-test.patch
patching file file1.c
patching file file1.h

Now at patch 0002-test.patch
```
push命令使用0002-test.patch。

## 为openwrt制作patch



## 参考

* [quilt-doc](http://www.shakthimaan.com/downloads/glv/quilt-tutorial/quilt-doc.pdf)
* [Working with patches](http://wiki.openwrt.org/doc/devel/patches)

test1  
test2
