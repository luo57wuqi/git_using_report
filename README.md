## # git的使用方法

## git是什么

[Git - is what?](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control)

What is “version control”, and why should you care? 

Version control is a system that r**ecords changes to a file or set of files over time** 记录历史更改

 so that you can **recall specific versions later.**   恢复某个版本



## 1需求：

我有一个git配置代理的.md文件再xx目录下，

我有一个gihub账号3206178825@qq.com 名字是 luo57wuqi

2 如何发送呢？

```
1 新建仓库 不用新建README.me文件，也会导致没有分支
2 初始化本地文件所在的文件夹 git init
3 关联远程仓库 git remote add origin https://github.com/luo57wuqi/仓库名.git
4 文件 提交到缓存 git add README.md
5 提交到本地仓库 git commit -m "新建README.md文件"
6 推送到远程仓库 
	1 首次推送
   	git push -u origin main
  2 非首次推送
  	git push origin main
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

## 已经有了原创仓库 里面还有一个README.md文件

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

## 需求2 我已经拉取了自学是门手艺

如何一边阅读一边发送到自己的仓库呢？---记录我的阅读情况