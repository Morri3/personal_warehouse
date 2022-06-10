### Git操作

我们直接开门见山：

步骤：

1、进入到 **把那些要上传到远程仓库的文件** 所在的文件夹

2、删除本地的那些要上传到远程仓库的文件

3、打开git bash

4、执行git clone https://github.com/XXXXX/XXXXX【clone后面的是自己的远程仓库地址】

5、等待clone完成，此时会发现本地出现了远程仓库中的文件夹。

6、进入到步骤5中提到的这个文件夹**里**。

7、打开git bash【注意这里你所进入的文件夹的位置！】

8、执行git pull，待出现“Already up to date.”后表示该步骤成功。

9、这一步你可以对你的本地项目进行修改

⭐注意：若有提交空文件夹，请在每个空文件夹中创建一个xx.gitignore文件【创建一个xx.txt文本文件，另存为xx.gitignore即可】，输入的内容为：

```
# Ignore everything in this directory
*
# Except this file
!.gitignore
```

10、修改完后，**可以**执行git pull，待出现“Already up to date.”后表示该步骤成功。【要注意：**推到一个分支上不能同时间编辑同一个文件**】

11、这一步开始提交操作。

11-1、git add -A【添加所有变化】

11-2、git commit -m "20220504修改"【这是添加提交的注释的操作】

11-3、git push【执行git push是直接push到源程的主分支，不需要执行git push origin master】

12、至此，大功告成！