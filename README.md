## # git的使用方法

## git是什么

[Git - is what?](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control)

What is “version control”, and why should you care? 

Version control is a system that r**ecords changes to a file or set of files over time** 记录历史更改

 so that you can **recall specific versions later.**   恢复某个版本

# 不断简化

```
1 看日志
2 克隆远程
3 提交更改
4 recall 版本
5 
```



```
# 1. 关联远程仓库
git remote add origin https://github.com/luo57wuqi/git_using_report.git  # 添加远程仓库地址

# 2. 重命名分支并推送
git branch -M main                      # 确保分支名为main（与远程匹配）
git push -u origin main                 # 推送代码并建立分支追踪
```

```
# 1. 创建并初始化新仓库
echo "# git_using_report" >> README.md   # 创建README文件并写入标题
git init                                 # 初始化本地Git仓库
git add README.md                       # 将README文件添加到暂存区
git commit -m "first commit"            # 提交更改，添加提交信息
git branch -M main                      # 将默认分支重命名为main（适配GitHub新规范）

# 2. 关联远程仓库并推送
git remote add origin https://github.com/luo57wuqi/git_using_report.git  # 添加远程仓库地址
git push -u origin main                 # 首次推送并设置上游分支关联
```



## 需求1 ：上传远程仓库

我有一个git配置代理的.md文件再xx目录下，

我有一个gihub账号3206178825@qq.com 名字是 luo57wuqi

**2 如何第一次发送呢？**

```
1 新建仓库 不用新建README.me文件，也会导致没有分支
2 初始化本地文件所在的文件夹 git init
3 关联远程仓库 git remote add origin https://github.com/luo57wuqi/仓库名.git
4 文件 提交到缓存 git add README.md
5 提交到本地仓库 git commit -m "新建README.md文件"
6 推送到远程仓库 
	1 首次推送
   		git push -u origin main  # 首次推送并设置上游分支关联
  2 非首次推送
  		git push origin main
```

**3 提交更新**

```
1  git add README.md
2  git commit -m "更新第一次上传成功" # 提交到本地仓库和更新信息
         返回出 提交了几个文件 增加了几个更改 删除几个更改  
         1 file changed, 50 insertions(+), 6 deletions(-)
3  git push -u origin main # 提交到分支main
        Enumerating objects: 5, done.
        Counting objects: 100% (5/5), done.
        Delta compression using up to 4 threads
        Compressing objects: 100% (2/2), done.
        Writing objects: 100% (3/3), 1.18 KiB | 401.00 KiB/s, done.
        Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
        remote: Resolving deltas: 100% (1/1), completed with 1 local object.
        To https://github.com/luo57wuqi/git_using_report.git
           1c93158..1675ce2  main -> main
        branch 'main' set up to track 'origin/main'
```

**4 远程仓库没有文件怎么办？**

```
1 若不存在 main，需在 GitHub 设置中将默认分支改为 main 

2 重新初始化远程仓库 若远程仓库为空，可删除并重新创建（勾选初始化 README），再执行以下命令：
      git remote remove origin # 删除远程文件
      git remote add origin https://github.com/luo57wuqi/git_using_report.git # 本地仓库加入远程
      git push -u origin main # 上传更改
```



###  教程

1. github官网新建一个仓库  git_using_report 不用添加一个README.md文件

2. 初始git仓库

   1. 打开要上传的md所在的文件夹--打开gitbash 右键就出现了 git选项 ![image-20250316164251608](C:/Users/luojuan/AppData/Roaming/Typora/typora-user-images/image-20250316164251608.png)

      ```
      2 git init
      ```

    ![image-20250316164444476](C:/Users/luojuan/AppData/Roaming/Typora/typora-user-images/image-20250316164444476.png)

3. **关联GitHub的远程仓库 git_using_report**

   ```
   git remote add origin https://github.com/luo57wuqi/仓库名.git
   git remote add origin https://github.com/luo57wuqi/git_using_report.git
   ```

   ![image-20250316164655391](C:/Users/luojuan/AppData/Roaming/Typora/typora-user-images/image-20250316164655391.png)

4. **添加文件到换成 并且提交**1

   ```
   1 提交缓存
   		git add xxx文件
   		eg git add README.md
   2 提交 附加信息
       git commit -m "添加git代理配置文档"
       eg git commit -m "first time to updata a local file"
   ```

5. 推送到远程仓库

   ```
   1 首次推送
    git push -u origin main
   2 非首次推送
   git push origin main
   ```

   **问题**  

   error: src refspec main does not match anyerror: **本地分支与远程分支名称不匹配**

   failed to push some refs to 'https://github.com/luo57wuqi/git_using_repor
   t.git' 

    ![image-20250316165358712](C:/Users/luojuan/AppData/Roaming/Typora/typora-user-images/image-20250316165358712.png)

   ```
   新建的时候没有任何分支---导致推送到main失败
   
   推送成功后，GitHub 默认分支会自动更新为 main。
   
   git branch -M main 
   # 重命名本地分支为 main 在本地执行以下命令，将 master 分支重命名为 main
   git push -u origin main --force 
   # 强制推送并覆盖远程分支 使用 -u 参数关联远程分支并推送 -force 会覆盖远程仓库内容，确保远程分支与本地一致 
   ```

   ![image-20250316170147802](C:/Users/luojuan/AppData/Roaming/Typora/typora-user-images/image-20250316170147802.png)![image-20250316170205021](C:/Users/luojuan/AppData/Roaming/Typora/typora-user-images/image-20250316170205021.png)

 **已经有了原创仓库 里面还有一个README.md文件**

#### 发现：git push origin master 多了一个分支叫做master 而在github新建文件的时候的 已经有一个 分支 main

```
1 在这个文件下打开gitabsh shell
输入:    git init
Initialized empty Git repository in D:/编程jupyter/哎自学是门手艺/上手写程序/git
_sever_failed_solve/.git/

2 git add README.md
3 git status
4 git add . # 提交到换成区域
5 git commit -m "初始化项目：覆盖远程 README.md"
6 git push -u origin master -f # 强制推送到远程仓库（谨慎使用！会覆盖远程历史）
7 git remote -v  # 确认远程地址正确 
        origin  https://github.com/luo57wuqi/git_sever_failed_solve.git (fetch)
        origin  https://github.com/luo57wuqi/git_sever_failed_solve.git (push)
8 git remote set-url origin https://github.com/luo57wuqi/git_sever_failed_solve.git
9 git push origin master  # 测试推送
```

![image-20250316162427533](C:/Users/luojuan/AppData/Roaming/Typora/typora-user-images/image-20250316162427533.png)

## 需求2 拉取自学是门手艺-提交笔记-查看笔记日志

如何一边阅读一边发送到自己的仓库呢？---记录我的阅读情况

```
# 0 git init # 及时有.git文件
git init # 这样就可以加入管理了

# 提交更改文件
1 git add 克隆仓库.md # git add.# 提交当前目录下所有文件

# 提交更改的评论（笔记）
git commit -m "我克隆成功了自学是门手艺这个代码了，哈哈"
 评论：[master (root-commit) 739ea4d] 我克隆成功了自学是门手艺这个代码了，哈哈
 改变： 一个文件改变 19代码写入  1 file changed, 19 insertions(+)
 属性：新建了文件 create mode 100644 "my-notes/\345\205\213\351\232\206\344\273\223\345\272\223.md"

# 3 查看这个项目的更改情况--或者叫做笔记   输出每条提交的哈希值（如 1a2b3c4d）、作者、日期和提交信息。
git log
    评论 commit 739ea4d0ea90099fb5a292ffd0a163db99d62551 (HEAD -> master)
    作者 Author: luo57wuqi <3206178825@qq.com>
    日期 Date:   Sun Mar 16 17:44:36 2025 +0800
    评论内容：我克隆成功了自学是门手艺这个代码了，哈哈

# cd 进入某个 文件 cd my-notes  进入my-notes 文件夹下
```

![image-20250316175243034](C:/Users/luojuan/AppData/Roaming/Typora/typora-user-images/image-20250316175243034.png)

## 需求3 恢复版本

```
 日志
git log # 所有日志
            commit 739ea4d0ea90099fb5a292ffd0a163db99d62551 (HEAD -> master)
            Author: luo57wuqi <3206178825@qq.com>
            Date:   Sun Mar 16 17:44:36 2025 +0800

                我克隆成功了自学是门手艺这个代码了，哈哈

git log --oneline # 简化提交历史 
					739ea4d (HEAD -> master) 我克隆成功了自学是门手艺这个代码了，哈哈
					
git reflog # 查看所有操作记录（包括已删除的提交
            739ea4d (HEAD -> master) HEAD@{0}: commit (initial): 我克隆成功了自学是门手艺这
            个代码了，哈哈
```

