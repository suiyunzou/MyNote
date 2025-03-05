# Bug：github邮箱private，导致本地上传失败

## 报错信息

>**$ git push -u origin main**
>Enumerating objects: 8, done.
>Counting objects: 100% (8/8), done.
>Delta compression using up to 12 threads
>Compressing objects: 100% (8/8), done.
>Writing objects: 100% (8/8), 2.50 KiB | 1.25 MiB/s, done.
>Total 8 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
>remote: Resolving deltas: 100% (2/2), done.
>remote: error: GH007: Your push would publish a private email address.
>remote: You can make your email public or disable this protection by visiting:
>remote: https://github.com/settings/emails
>To https://github.com/suiyunzou/MyNote.git
> ! [remote rejected] main -> main (push declined due to email privacy restrictio
>ns)
>error: failed to push some refs to 'https://github.com/suiyunzou/MyNote.git'

由于我之前将自己的github邮箱修改为私人化，导致我本地使用私人邮箱无法正常上传git代码；

## 解决方案

>方案一：在GitHub设置中公开邮箱
>
>1. 访问 https://github.com/settings/emails
>
>2. 取消勾选 "Keep my email addresses private"
>
>---
>
>方案二：修改本地Git配置使用GitHub提供的no-reply邮箱
>
>1. git config --global user.email "你的ID+username@users.noreply.github.com"
>
>2. git commit --amend --reset-author
>
>3. git push -u origin main --force

这里使用方案2：因为我是想保护个人邮箱信息，所有才private，显然方案1不合理；

解释方案2：

1. git config --global user.email "你的ID+username@users.noreply.github.com"

   修改本地配置邮箱信息，从github设置中获取；路径：右上角头像->Settings->Emails

2. git commit --amend --reset-author

   git commit --amend：修改最近一次的提交信息；

   ​					--reset-author：重置一下用户信息；

3. git push -u origin main --force

   告诉本地，强制提交代码到远程仓库。

## 疑问解答

**Q：使用amend修改本地用户信息后，推向远端必须要使用--force吗？**

不是的，如果你远端没有你本地最新提交的原始版本，则不用使用--force；

比如：

本地commit：A->B->C ；    远程commit：A->B；

- 当你本地尝试提交C时，出现你所提交的email是私人邮箱；
- 这个时候拟将其改为了ID+username@users.noreply.github.com；
- 并使用 --amend 修改最后一次提交为C，此时最新你提交变为C'；
- 此时本地：A->B->C' ;远程：A->B；由于远程没有第三次提交任何信息
- 此时直接git push -u origin main  即可；

