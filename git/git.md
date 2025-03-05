# git常用指令

## 查看本地账户配置信息：

>git config user.name
>
>git config  user.email

## 创建分支；

>git branch <name>  //创建分支
>
>git branch -b <name> // 创建并切换分支
>
>

## 修改当前分支名称

>```git
>git branch -M main # 修改分支名为Main
>```



## 提交代码：



>```javascript
>## 1. 本地提交
>git commit -m "提交信息" 
>## 2.1 远程提交，先确定远程提交的地址
>git remote add origin https://github.com/suiyunzou/MyNote.git
>## 2.2 提交代码到远程,确定提交分支名称
>git push -u origin main
>
>```