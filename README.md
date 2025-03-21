## # git的使用方法

## git是什么

[Git - is what?](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control)

What is “version control”, and why should you care? 

Version control is a system that r**ecords changes to a file or set of files over time** 记录历史更改

 so that you can **recall specific versions later.**   恢复某个版本

# 不断简化

```
1 看日志 git log
2 克隆远程 git clone 地址
3 提交更改 
		  git add 文件 git commit -m"更新的信息/笔记" 
      git add origin 远程地址.git 
      git push origin xxx分支名字（远程和本地一致）
4 recall 版本 还不会
5 git https需要 重新设置下代理 
git config --global http.proxy http://127.0.0.1:17890
git config --global https.proxy http://127.0.0.1:17890
```

## 总结

#### **1. 初始化仓库与首次推送**  

[问小白 - AI助手](https://www.wenxiaobai.com/chat/200006)

**代码示例**：  
```bash
git init
git remote add origin https://github.com/luo57wuqi/git_using_report.git
git add README.md
git commit -m "first commit"
git branch -M main
git push -u origin main
```
**作用**：  

- 初始化本地Git仓库。  
- 关联远程仓库地址。  
- 提交文件到本地仓库并重命名分支为`main`。  
- 首次推送代码到远程仓库的`main`分支。  

**效果**：  
- 若远程仓库为空，首次推送成功后会创建`main`分支并上传代码。  
- 若远程仓库已存在`main`分支，需确保本地分支与远程分支名称一致。  

---

#### **2. 解决SSH密钥配置问题**  
**代码示例**：  
```powershell
ssh-keygen -t ed25519 -C "3206178825@qq.com"  # 生成密钥时误输入文件名`yes`
mkdir -Force ~/.ssh
Move-Item -Path .\yes ~/.ssh\id_ed25519
Move-Item -Path .\yes.pub ~/.ssh\id_ed25519.pub
cat ~/.ssh/id_ed25519.pub
ssh -T git@github.com
```
**作用**：  
- 生成Ed25519算法的SSH密钥对。  
- 修复密钥路径错误，将密钥文件移动到正确目录（`~/.ssh`）。  
- 验证SSH连接是否成功。  

**效果**：  
- 密钥文件生成后，公钥内容需手动添加到GitHub账户的SSH设置中。  
- 成功执行`ssh -T git@github.com`后显示认证成功提示。  

---

#### **3. 分支管理与强制推送**  
**代码示例**：  
```bash
git branch -M main          # 重命名本地分支为main
git push -u origin main -f  # 强制推送本地分支到远程
git push origin --delete master  # 删除远程`master`分支
git branch -d master        # 删除本地`master`分支
```
**作用**：  
- 将默认分支从`master`迁移到`main`以符合GitHub新规范。  
- 强制覆盖远程分支历史（慎用）。  
- 清理旧的`master`分支。  

**效果**：  
- 强制推送可能导致远程仓库历史被覆盖，需谨慎操作。  
- 删除分支后，远程仓库仅保留`main`分支。  

---

#### **4. 处理远程仓库无文件或分支冲突**  
**代码示例**：  
```bash
git remote remove origin                   # 删除旧远程地址
git remote add origin <新仓库地址>          # 重新关联远程仓库
git push -u origin main                   # 重新推送代码
git pull origin main --allow-unrelated-histories  # 合并不相关历史
```
**作用**：  
- 重置远程仓库关联地址。  
- 解决因分支名称不一致或历史冲突导致的推送失败问题。  

**效果**：  
- `--allow-unrelated-histories`允许合并不相关的提交历史，解决`fatal: refusing to merge unrelated histories`错误。  

---

#### **5. 版本恢复与日志查看**  
**代码示例**：  
```bash
git log --oneline       # 查看简化提交历史
git reflog              # 查看所有操作记录（包括已删除提交）
git checkout <commit-id># 恢复特定版本
```
**作用**：  
- 快速查看提交历史的关键信息。  
- 恢复误删除的提交或分支。  

**效果**：  
- `git reflog`可找回因强制推送或分支删除丢失的提交记录。  

6.继续上传记录--先设置代理--SSH 切换 Http 上传

```
ssH 没有链接收集网络失败了---
1 检测问题
    1. 检查 SSH 连接
    运行以下命令测试 SSH 连接：
    ssh -T git@github.com
    成功连接：显示 Hi 用户名! You've successfully authenticated。
    连接失败：提示超时或权限错误。
    ssh: connect to host github.com port 22: Connection timed out-----校园网的问题
2 换成ssh 
  git remote set-url origin git@github.com:用户名/仓库名.git 设置ssh传输
  ssh -T git@github.com 验证
2 换http  重新设置代理
我的梯子的端口是 17890
git config --global http.proxy http://127.0.0.1:7890
git config --global https.proxy http://127.0.0.1:7890

git remote set-url origin https://github.com/用户名/仓库名.git  the-scraft-of-selfteaching
git remote set-url origin https://github.com/luo57wuqi/the-scraft-of-selfteaching.git

3 检测代理
如果找到你自己的梯子代理
1 去安装的梯子的应用查看---我自己的梯子应用和官网没有
2 去安装梯子的exe所在的文件夹，找到以 一个config的文件，记事本打开---里面可能有端口设置的 信息

1 设置端口00没有设置无法访问国外资源---当然得有梯子（还有配置host DSNip ，不过我还不会）
git config --global http.proxy http://127.0.0.1:7890
git config --global https.proxy http://127.0.0.1:7890
设置 git的获取https,http请求使用的端口代理 http://127.0.0.1:7890 和https://127.0.0.1:782 

2 取消配置 代理（如果你的代理端口是错误的，找到你自己梯子的端口后再 使用 1cmd 命令 设置）
git config --global --unset http.proxy 
git config --global --unset https.proxy

3 检测是否 已经设置好代理了
git config --global --edit
里面有你设置的 端口 就说明设置config成功了

4 检测能否获取github的数据
git clone https://github.com/github/gitignore.git


```



```
检测代理
原来是需要重新设置代理

cmd 打开不是poweshell
curl -x http://127.0.0.1:17890 https://github.com

C:\Users\luojuan\qingyun\resources\static\clash>curl -x http://127.0.0.1:17890 https://github.com
curl: (35) Recv failure: Connection was aborted

C:\Users\luojuan\qingyun\resources\static\clash>git config --global http.proxy http://127.0.0.1:7890

C:\Users\luojuan\qingyun\resources\static\clash>git config --global https.proxy http://127.0.0.1:7890

C:\Users\luojuan\qingyun\resources\static\clash>curl -x http://127.0.0.1:17890 https://github.com








<!DOCTYPE html>
<html
  lang="en"
```

![image-20250316230919332](D:/%E7%BC%96%E7%A8%8Bjupyter/%E5%93%8E%E8%87%AA%E5%AD%A6%E6%98%AF%E9%97%A8%E6%89%8B%E8%89%BA/%E4%B8%8A%E6%89%8B%E5%86%99%E7%A8%8B%E5%BA%8F/git_using_report/images/image-20250316230919332.png)

```
commit 739ea4d0ea90099fb5a292ffd0a163db99d62551
Author: luo57wuqi <3206178825@qq.com>
Date:   Sun Mar 16 17:44:36 2025 +0800

    我克隆成功了自学是门手艺这个代码了，哈哈
q

git log 按下 q 退出查看日志 
```



---

### **整体代码作用总结**  
1. **仓库初始化与推送**：从零开始配置本地仓库并推送至远程。  
2. **SSH认证配置**：生成密钥、修复路径错误、绑定GitHub账户。  
3. **分支管理**：迁移默认分支、清理旧分支、解决分支冲突。  
4. **错误处理**：解决推送失败、历史冲突、远程仓库无分支等问题。  
5. **版本控制**：提交日志查看、版本恢复与操作记录追踪。  

---

### **行动建议**  
1. **SSH密钥生成**：  
   - 生成密钥时直接按回车使用默认路径（`~/.ssh/id_ed25519`），避免手动输入路径导致错误。  
2. **分支命名规范**：  
   - 在团队协作中提前统一分支命名（如`main`），减少冲突。  
3. **谨慎使用强制推送**：  
   - `git push -f`会覆盖远程历史，仅在私有分支或紧急修复时使用。  
4. **历史合并冲突**：  
   - 长期项目应避免使用`--allow-unrelated-histories`，保持分支历史一致性。  
5. **版本恢复**：  
   - 定期使用`git log`和`git tag`标记重要版本，便于快速回滚。  

通过以上步骤，可系统化掌握Git核心操作，高效管理代码版本与协作流程。







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
  		
origin：远程仓库的默认别名（通常指向克隆的原始仓库地址）。
main：本地分支名称（Git 默认主分支名，旧版本可能用 master）。
作用：将本地 main 分支的所有新提交推送到远程仓库 origin 的同名分支（main）
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

**5 git push -u origin main 只是推送最新的更改**

```git
git push -u origin main
git remote -v # 查看远程对应的仓库
git add .  # 把所有文件加入缓存 准备提交
git status # 检查状态
git commit -m "提交所有文件"  # 提交到本地仓库 和 提交信息
git remote remove origin  # 删除远程仓库的地址
git remote add origin https://github.com/你的账号名/the-scraft-of-selfteaching.git # 添加仓库地址  luo57wuqi
git push -u origin main  # 如果分支是 main # 把本地仓库的代码上传远程仓库


git branch -M main # 重命名本地分支

# 新建一个远程仓库 而本地的项目 删除git历史 代码保留
cd /path/to/project
rm -rf .git  # 删除本地 Git 历史（保留代码）
git init     # 重新初始化
git add .   # 提交所有文件
git commit -m "Initial commit" # 初始文件提交
git remote add origin https://github.com/luo57wuqi/the-scraft-of-selfteaching.git # 链接配置仓库地址
git push -u origin main   # 上传文件到远程仓库
```

**6 SSH通信**

```
替代方案：改用 HTTPS 协议
如果 SSH 仍失败，切换为 HTTPS 推送：

Bash
git remote set-url origin https://github.com/luo57wuqi/the-scraft-of-selfteaching.git
git push -f origin master
```



```
# ssH通讯
PS D:\编程jupyter\哎自学是门手艺\上手写程序\the-craft-of-selfteaching> 
1 ssh -T git@github.com
The authenticity of host 'github.com (20.205.243.166)' can't be established.
This host key is known by the following other names/addresses:
    C:\Users\luojuan/.ssh/known_hosts:2: [ssh.github.com]:443
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com' (ED25519) to the list of known hosts.
git@github.com: Permission denied (publickey).
没有获得SSH通讯

# 查看存在ssh密钥没有
ls ~/.ssh/id_ed25519.pub  #  id_rsa.pub
ls : 找不到路径“C:\Users\luojuan\.ssh\id_ed25519.pub”，因为该路径不存在。

# 生成ssH密钥

+----[SHA256]-----+


# 获取本地ssh密码
cat ~/.ssh/id_ed25519.pub
cat : 找不到路径“C:\Users\luojuan\.ssh\id_ed25519.pub”，因为该路径不存在。
所在位置 行:1 字符: 1
+ cat ~/.ssh/id_ed25519.pub
+ ~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (C:\Users\luojuan\.ssh\id_ed25519.pub:String) [Get-Content], ItemNotFoundException
    + FullyQualifiedErrorId : PathNotFound,Microsoft.PowerShell.Commands.GetContentCommand

# 一堆SSH文件到 C:\Users\luojuan\
PS D:\编程jupyter\哎自学是门手艺\上手写程序\the-craft-of-selfteaching> #  .ssh Ŀ¼ڣ
>> mkdir -Force ~/.ssh
>>
>> # ƶԿļ ~/.ssh/
>> Move-Item -Path .\yes ~/.ssh\id_ed25519
>> Move-Item -Path .\yes.pub ~/.ssh\id_ed25519.pub


    目录: C:\Users\luojuan


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----         2025/3/16      0:10                .ssh


PS D:\编程jupyter\哎自学是门手艺\上手写程序\the-craft-of-selfteaching> # ȨΪǰûɶд
>> icacls ~\.ssh\id_ed25519 /reset
>> icacls ~\.ssh\id_ed25519 /grant:r "$env:username:(R,W)"
~\.ssh\id_ed25519: The system cannot find the path specified.
Successfully processed 0 files; Failed processing 1 files
Invalid parameter "(R,W)"


# 获得ssh文件
cat ~/.ssh/id_ed25519.pub



# 和github通讯
ssh -T git@github.com
Hi luo57wuqi! You've successfully authenticated, but GitHub does not provide shell access.


# 传输文件
git push -f origin master
Enumerating objects: 291, done.
Counting objects: 100% (291/291), done.
Delta compression using up to 4 threads
Compressing objects: 100% (277/277), done.
Writing objects:  14% (43/291), 15.04 MiB | 145.00 KiB/s
```

根据你的操作，**SSH 密钥文件被错误保存到了当前目录**（路径错误）。以下是修正步骤：

### **1. 找到生成的密钥文件**

- **私钥文件**：`D:\编程jupyter\哎自学是门手艺\上手写程序\the-craft-of-selfteaching\yes`
- **公钥文件**：`D:\编程jupyter\哎自学是门手艺\上手写程序\the-craft-of-selfteaching\yes.pub`

### **2. 将密钥文件移动到正确位置**

在 PowerShell 中执行以下命令：

```
Powershell# 创建 .ssh 目录（如果不存在）
mkdir -Force ~/.ssh

# 移动并重命名密钥文件到 ~/.ssh/
Move-Item -Path .\yes ~/.ssh\id_ed25519
Move-Item -Path .\yes.pub ~/.ssh\id_ed25519.pub
```

### **3. 设置私钥文件权限**

```
Powershell# 设置权限为仅当前用户可读写
icacls ~\.ssh\id_ed25519 /reset
icacls ~\.ssh\id_ed25519 /grant:r "$env:username:(R,W)"
```

### **4. 查看公钥内容并添加到 GitHub**

```
Powershell
cat ~/.ssh/id_ed25519.pub
```

复制输出内容，登录 GitHub → **Settings → SSH and GPG keys → New SSH key** → 粘贴并保存。

### **5. 测试 SSH 连接**

```
Powershell
ssh -T git@github.com
```

正常应显示：

```
 Hi luo57wuqi! You've successfully authenticated, but GitHub does not provide shell access.
```

### **6. 重新推送代码**

```
Powershell
git push -f origin master
```







###  教程

1. github官网新建一个仓库  git_using_report 不用添加一个README.md文件

2. 初始git仓库

   1. 打开要上传的md所在的文件夹--打开gitbash 右键就出现了 git选项 ![image-20250316164251608](D:/%E7%BC%96%E7%A8%8Bjupyter/%E5%93%8E%E8%87%AA%E5%AD%A6%E6%98%AF%E9%97%A8%E6%89%8B%E8%89%BA/%E4%B8%8A%E6%89%8B%E5%86%99%E7%A8%8B%E5%BA%8F/git_using_report/images/image-20250316164251608.png)

      ```
      2 git init
      ```

    ![image-20250316164444476](D:/%E7%BC%96%E7%A8%8Bjupyter/%E5%93%8E%E8%87%AA%E5%AD%A6%E6%98%AF%E9%97%A8%E6%89%8B%E8%89%BA/%E4%B8%8A%E6%89%8B%E5%86%99%E7%A8%8B%E5%BA%8F/git_using_report/images/image-20250316164444476.png)

3. **关联GitHub的远程仓库 git_using_report**

   ```
   git remote add origin https://github.com/luo57wuqi/仓库名.git
   git remote add origin https://github.com/luo57wuqi/git_using_report.git
   ```

   ![image-20250316164655391](D:/%E7%BC%96%E7%A8%8Bjupyter/%E5%93%8E%E8%87%AA%E5%AD%A6%E6%98%AF%E9%97%A8%E6%89%8B%E8%89%BA/%E4%B8%8A%E6%89%8B%E5%86%99%E7%A8%8B%E5%BA%8F/git_using_report/images/image-20250316164655391.png)

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

   failed to push some refs to 'https://github.com/luo57wuqi/git_using_reporha
   t.git' 

    ![image-20250316165358712](D:/%E7%BC%96%E7%A8%8Bjupyter/%E5%93%8E%E8%87%AA%E5%AD%A6%E6%98%AF%E9%97%A8%E6%89%8B%E8%89%BA/%E4%B8%8A%E6%89%8B%E5%86%99%E7%A8%8B%E5%BA%8F/git_using_report/images/image-20250316165358712.png)

   ```
   新建的时候没有任何分支---导致推送到main失败
   
   推送成功后，GitHub 默认分支会自动更新为 main。
   
   git branch -M main 
   # 重命名本地分支为 main 在本地执行以下命令，将 master 分支重命名为 main
   git push -u origin main --force 
   # 强制推送并覆盖远程分支 使用 -u 参数关联远程分支并推送 -force 会覆盖远程仓库内容，确保远程分支与本地一致 
   ```

   ![image-20250316170147802](D:/%E7%BC%96%E7%A8%8Bjupyter/%E5%93%8E%E8%87%AA%E5%AD%A6%E6%98%AF%E9%97%A8%E6%89%8B%E8%89%BA/%E4%B8%8A%E6%89%8B%E5%86%99%E7%A8%8B%E5%BA%8F/git_using_report/images/image-20250316170147802.png)![image-20250316170205021](D:/%E7%BC%96%E7%A8%8Bjupyter/%E5%93%8E%E8%87%AA%E5%AD%A6%E6%98%AF%E9%97%A8%E6%89%8B%E8%89%BA/%E4%B8%8A%E6%89%8B%E5%86%99%E7%A8%8B%E5%BA%8F/git_using_report/images/image-20250316170205021.png)

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

![image-20250316162427533](D:/%E7%BC%96%E7%A8%8Bjupyter/%E5%93%8E%E8%87%AA%E5%AD%A6%E6%98%AF%E9%97%A8%E6%89%8B%E8%89%BA/%E4%B8%8A%E6%89%8B%E5%86%99%E7%A8%8B%E5%BA%8F/git_using_report/images/image-20250316162427533.png)

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

## 需求4 本地文件上传到远程仓库和合并多个分子的历史

### 分步分析代码作用及效果：
1. **检查SSH密钥是否存在**  
   ```powershell
   ls ~/.ssh/id_ed25519.pub
   ```
   **作用**：检查默认路径下是否存在SSH公钥文件。  
   **效果**：系统提示路径不存在，说明未生成SSH密钥。

2. **生成SSH密钥**  
   ```powershell
   ssh-keygen -t ed25519 -C "3206178825@qq.com"
   ```
   **作用**：生成Ed25519算法的SSH密钥对。  
   **效果**：用户误输入保存文件名为`yes`（应为默认路径`~/.ssh/id_ed25519`），导致密钥文件被错误命名。

3. **修复密钥路径**  
   ```powershell
   mkdir -Force ~/.ssh
   Move-Item -Path .\yes ~/.ssh\id_ed25519
   Move-Item -Path .\yes.pub ~/.ssh\id_ed25519.pub
   ```
   **作用**：创建`.ssh`目录，将密钥文件移动到正确路径并重命名。  
   **效果**：成功修复密钥路径，后续SSH认证正常。

4. **验证GitHub SSH连接**  
   ```powershell
   ssh -T git@github.com
   ```
   **作用**：测试SSH密钥是否与GitHub绑定成功。  
   **效果**：返回成功认证提示，验证通过。

5. **强制推送本地仓库到远程`master`分支**  ----远程的是main 所有不会改变那个分支的文件和提交历史版本
   
   ```powershell
   git push -f origin master
   ```
   **作用**：强制覆盖远程`master`分支的提交历史。  
   **效果**：本地代码被完整推送至GitHub，但可能破坏远程仓库历史。
   
6. **尝试克隆远程仓库失败**  
   
   ```powershell
   git clone https://github.com/giuhut/the-craft-of-selfteaching .git
   ```
   **作用**：克隆远程仓库到本地。  
   **效果**：因路径冲突（`.git`已存在）导致失败。
   
7. **切换并合并分支**  合并两个分支 发送到远程
   
   ```powershell
   git checkout -b main
   git merge master
   git push -u origin main
   ```
   **作用**：创建`main`分支，合并`master`分支内容，推送至远程。  
   **效果**：因远程`main`分支与本地历史冲突，推送失败。
   
8. **解决历史冲突**   合并不相干的提交历史
   
   ```powershell
   git pull origin main --allow-unrelated-histories
   ```
   **作用**：允许合并不相关的提交历史。  
   **效果**：成功合并本地与远程代码，最终推送生效。
   
   ```powershell
   git log --oneline
       013311b (HEAD -> main, origin/main) Merge branch 'main' of github.com:luo57wuqi/the-scraft-of-selfteaching
       9ae291f (origin/master, master) Complete project rewrite
       946b401 成功提交一个修改和查看日志
       739ea4d 我克隆成功了自学是门手艺这个代码了，哈哈
   ```
   
   
   
9. **删除远程`master`分支**  
   
   ```powershell
   git push origin --delete master
   git branch -d master
   
   # 远程的master没了 限制只有一个main 而且提交历史也在
   ```
   **作用**：删除远程和本地的`master`分支。  
   **效果**：完成从`master`到`main`分支的迁移。

---

### 整体代码作用总结：
1. **初始化SSH认证**：生成并配置SSH密钥，绑定GitHub账户。
2. **强制推送本地代码**：覆盖远程仓库的`master`分支历史。
3. **分支迁移**：将默认分支从`master`切换为`main`，解决历史冲突后完成推送。
4. **清理旧分支**：删除远程和本地的`master`分支，统一使用`main`。

---

### 行动建议：
1. **SSH密钥生成**：确保生成密钥时使用默认路径（直接按回车），避免手动输入导致路径错误。
2. **谨慎使用强制推送**：`git push -f`可能覆盖他人提交，建议仅在私有分支使用。
3. **分支管理**：在团队协作中，提前约定分支命名规则（如使用`main`），避免冲突。
4. **克隆仓库**：若本地已有`.git`目录，需先删除或选择其他路径再克隆。
5. **合并历史冲突**：`--allow-unrelated-histories`是临时解决方案，长期应保持分支历史一致性。PS D:\编程jupyter\哎自学是门手艺\上手写程序\the-craft-of-selfteaching> ls ~/.ssh/id_ed25519.pub  #  id_rsa.pub

## 需求5 版本恢复和查看某版本的内容--查看某个文件



### **一、回到某个版本的文件**

1. **查看文件的历史版本** 使用 `git log` 查看文件的提交历史，找到目标版本的提交哈希：

   ```
   git log <文件路径>
   ```

   示例：

   ```
    git log README.md
   
   >>>
   commit d732549a9cb1c908e173fb17e592c2024928e97a (HEAD -> main, origin/main)
   Author: luo57wuqi <3206178825@qq.com>
   Date:   Sun Mar 16 23:23:41 2025 +0800
   
       增加git常用命令在最后一行 目前还不知都如何回到某个版本时候的文件 生成的哈希i
   d 就可以重新恢复了 可以回到最新吗，就是我查看不恢复
   
   commit f865115694497ef55910bec0b94ae3671b7d0c9e
   Author: luo57wuqi <3206178825@qq.com>
   Date:   Sun Mar 16 23:18:33 2025 +0800
   
        使用前检测代理 更新SSH https传输
   
   commit 9722906f81ef3cdc3624aeda667b3830cf46d0bc
   Author: luo57wuqi <3206178825@qq.com>
   Date:   Sun Mar 16 18:24:10 2025 +0800
   
       写笔记 传修改
   
   commit 1675ce24dd70ea77613c779e6eabf7ab0f31f4d2
   Author: luo57wuqi <3206178825@qq.com>
   Date:   Sun Mar 16 17:06:51 2025 +0800
   
       更新第一次发送到远程仓库的版本
   
   commit 1c93158476a1edbc8107ef995da046e261f269e0
   Author: luo57wuqi <3206178825@qq.com>
   Date:   Sun Mar 16 16:51:09 2025 +0800
   
       first time to updata a local file
   q # 退出版本查看
   ```

2. **查看文件的某个版本内容** 使用 `git show` 查看某次提交中文件的内容：

   ```
   git show <提交哈希>:<文件路径>
   ```

   示例：

   ````
   git show  1c93158476a1edbc8107ef995da046e261f269e0:README.md
   
   >>>
   ## # git的使用方法
   ## git是什么
   [Git - is what?](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Co
   ntrol)
   What is “version control”, and why should you care?
   Version control is a system that r**ecords changes to a file or set of files ove
   r time** 记录历史更改
    so that you can **recall specific versions later.**   恢复某个版本
   
   ## 1需求：
   我有一个git配置代理的.md文件再xx目录下，
   我有一个gihub账号3206178825@qq.com 名字是 luo57wuqi
   2 如何发送呢？
   ```
   ```
   ###  教程
   ````

3. **恢复文件的某个版本** 使用 `git checkout` 将文件恢复到某个版本：

   ```
   git checkout <提交哈希> -- <文件路径>
   ```

   示例：

   ```
   # 1 恢复 1c93158476a1edbc8107ef995da046e261f269e0 版本的 README.md
   git checkout  1c93158476a1edbc8107ef995da046e261f269e0 -- README.md
   
   luojuan@▒▒▒▒ĵ▒▒▒ MINGW64 /d/编程jupyter/哎自学是门手艺/上手写程序/git_using_report (main)
   
   # 2 这个时候又历史缓存了 提交到本控制中--方便恢复
   
   git commit -m "恢复 README.md 到 946b401 版本"
   [main 54d8ee5] 恢复 README.md 到 946b401 版本
    1 file changed, 10 insertions(+), 994 deletions(-)
   
   # 3 上传到远程仓库
   git push origin main
   
   Enumerating objects: 5, done.
   Counting objects: 100% (5/5), done.
   Delta compression using up to 4 threads
   Compressing objects: 100% (2/2), done.
   Writing objects: 100% (3/3), 473 bytes | 473.00 KiB/s, done.
   Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
   remote: Resolving deltas: 100% (1/1), completed with 1 local object.
   To https://github.com/luo57wuqi/git_using_report.git
      d732549..54d8ee5  main -> main
   
   ```

4. **恢复后提交更改** 恢复文件后，需要提交更改以更新仓库状态：

   ```
   # 1 d732549a9cb1c908e173fb17e592c2024928e97a 恢复前端最新的版本
   git checkout d732549a9cb1c908e173fb17e592c2024928e97a -- README.md
   # 提交恢复历史
   git commit -m "恢复 README.md 到 d732549a9cb1c908e173fb17e592c2024928e97a 版本"
   ```

![image-20250316234746155](D:/%E7%BC%96%E7%A8%8Bjupyter/%E5%93%8E%E8%87%AA%E5%AD%A6%E6%98%AF%E9%97%A8%E6%89%8B%E8%89%BA/%E4%B8%8A%E6%89%8B%E5%86%99%E7%A8%8B%E5%BA%8F/git_using_report/images/image-20250316234746155.png)

## 理论git常用

以下是 Git 常用命令的总结，涵盖日常开发中的主要操作场景：

---

### **一、仓库操作**
1. **初始化仓库**  
   ```bash
   git init
   ```

2. **克隆远程仓库**  
   ```bash
   git clone <仓库URL>
   ```

3. **查看远程仓库**  
   ```bash
   git remote -v
   ```

4. **添加远程仓库**  
   ```bash
   git remote add origin <仓库URL>
   ```

5. **修改远程仓库地址**  
   ```bash
   git remote set-url origin <新仓库URL>
   ```

---

### **二、提交与修改**
1. **查看当前状态**  
   ```bash
   git status
   ```

2. **添加文件到暂存区**  
   ```bash
   git add <文件名>  # 添加指定文件
   git add .        # 添加所有修改
   ```

3. **提交更改**  
   ```bash
   git commit -m "提交信息"
   ```

4. **查看提交历史**  
   ```bash
   git log          # 完整提交历史
   git log --oneline  # 简化提交历史
   ```

5. **撤销工作区修改**  
   ```bash
   git checkout -- <文件名>  # 撤销指定文件的修改
   ```

6. **撤销暂存区修改**  
   ```bash
   git reset HEAD <文件名>  # 将文件从暂存区移回工作区
   ```

7. **修改最后一次提交**  
   ```bash
   git commit --amend
   ```

---

### **三、分支操作**
1. **查看分支**  
   ```bash
   git branch       # 查看本地分支
   git branch -a    # 查看所有分支（包括远程分支）
   ```

2. **创建分支**  
   ```bash
   git branch <分支名>
   ```

3. **切换分支**  
   ```bash
   git checkout <分支名>
   ```

4. **创建并切换分支**  
   ```bash
   git checkout -b <分支名>
   ```

5. **合并分支**  
   ```bash
   git merge <分支名>  # 将指定分支合并到当前分支
   ```

6. **删除分支**  
   ```bash
   git branch -d <分支名>  # 删除本地分支
   git push origin --delete <分支名>  # 删除远程分支
   ```

7. **重命名分支**  
   ```bash
   git branch -m <旧分支名> <新分支名>
   ```

---

### **四、远程操作**
1. **拉取远程分支**  
   ```bash
   git pull origin <分支名>
   ```

2. **推送本地分支**  
   ```bash
   git push origin <分支名>
   ```

3. **强制推送（慎用）**  
   ```bash
   git push -f origin <分支名>
   ```

4. **查看远程分支**  
   ```bash
   git branch -r
   ```

5. **拉取远程分支并创建本地分支**  
   ```bash
   git checkout -b <本地分支名> origin/<远程分支名>
   ```

---

### **五、标签操作**
1. **查看标签**  
   ```bash
   git tag
   ```

2. **创建标签**  
   ```bash
   git tag <标签名>  # 轻量标签
   git tag -a <标签名> -m "标签信息"  # 附注标签
   ```

3. **推送标签到远程**  
   ```bash
   git push origin <标签名>  # 推送单个标签
   git push origin --tags    # 推送所有标签
   ```

4. **删除标签**  
   ```bash
   git tag -d <标签名>  # 删除本地标签
   git push origin --delete <标签名>  # 删除远程标签
   ```

---

### **六、撤销与回退**
1. **撤销工作区修改**  
   ```bash
   git restore <文件名>
   ```

2. **撤销暂存区修改**  
   ```bash
   git restore --staged <文件名>
   ```

3. **回退到指定提交**  
   ```bash
   git reset --hard <提交哈希>
   ```

4. **撤销某次提交**  
   ```bash
   git revert <提交哈希>
   ```

---

### **七、其他实用命令**
1. **查看文件修改差异**  
   ```bash
   git diff          # 查看工作区与暂存区的差异
   git diff --cached  # 查看暂存区与最新提交的差异
   git diff HEAD     # 查看工作区与最新提交的差异
   ```

2. **查看某次提交的修改**  
   ```bash
   git show <提交哈希>
   ```

3. **查看某文件的修改历史**  
   ```bash
   git log <文件名>
   ```

4. **查看某文件的详细修改记录**  
   ```bash
   git blame <文件名>
   ```

5. **清理未跟踪文件**  
   ```bash
   git clean -f  # 删除未跟踪的文件
   git clean -fd # 删除未跟踪的文件和目录
   ```

---

### **八、配置**
1. **查看配置**  
   ```bash
   git config --list
   ```

2. **设置用户名和邮箱**  
   ```bash
   git config --global user.name "你的名字"
   git config --global user.email "你的邮箱"
   ```

3. **设置默认编辑器**  
   ```bash
   git config --global core.editor "vim"
   ```

4. **设置代理**  
   ```bash
   git config --global http.proxy "http://127.0.0.1:8080"
   git config --global https.proxy "https://127.0.0.1:8080"
   ```

5. **取消代理**  
   ```bash
   git config --global --unset http.proxy
   git config --global --unset https.proxy
   ```

---

### **九、高级操作**
1. **合并多个提交**  
   ```bash
   git rebase -i HEAD~3  # 合并最近3次提交
   ```

2. **查看操作日志**  
   ```bash
   git reflog
   ```

3. **暂存当前修改**  
   ```bash
   git stash  # 暂存修改
   git stash pop  # 恢复暂存的修改
   ```

4. **查看暂存列表**  
   ```bash
   git stash list
   ```

5. **应用指定暂存**  
   ```bash
   git stash apply stash@{1}
   ```

---

### **十、常见问题**
1. **解决冲突**  
   - 合并或拉取时出现冲突，手动修改冲突文件后执行：
     ```bash
     git add <冲突文件>
     git commit
     ```

2. **恢复误删分支**  
   - 通过 `git reflog` 找到误删分支的提交哈希，然后创建新分支：
     ```bash
     git checkout -b <分支名> <提交哈希>
     ```

3. **修复提交信息**  
   - 修改最后一次提交信息：
     ```bash
     git commit --amend
     ```

---

通过以上命令，你可以高效管理 Git 仓库。如果遇到具体问题，请提供更多上下文信息进一步分析。

## 理论git版本控制

### **一、回到某个版本的文件**

1. **查看文件的历史版本** 使用 `git log` 查看文件的提交历史，找到目标版本的提交哈希：

   ```
   git log <文件路径>
   ```

   示例：

   ```
   git log README.md
   ```

2. **查看文件的某个版本内容** 使用 `git show` 查看某次提交中文件的内容：

   ```
   git show <版本哈希值>:<文件名>
   ```

   示例：

   ```
   git show 946b401:README.md
   ```

3. **恢复文件的某个版本** 使用 `git checkout` 将文件恢复到某个版本：

   ```
   git checkout <提交哈希> -- <文件路径>
   ```

   示例：

   ```
   git checkout 946b401 -- README.md
   ```

4. **恢复后提交更改** 恢复文件后，需要提交更改以更新仓库状态：

   ```
   git commit -m "恢复 README.md 到 946b401 版本"
   ```

### **二、回到最新版本**

1. **查看最新版本的文件** 使用 `git checkout` 将文件恢复到最新版本：

   ```
   git checkout main -- <文件路径>
   ```

   示例：

   ```
   git checkout main -- README.md
   ```

2. **拉取远程最新代码** 如果远程仓库有更新，先拉取最新代码：

   ```
   git pull origin main
   ```

### **三、常用命令总结**

| **操作**                   | **命令**                                |
| -------------------------- | --------------------------------------- |
| 初始化仓库                 | `git init`                              |
| 克隆远程仓库               | `git clone <仓库URL>`                   |
| 查看当前状态               | `git status`                            |
| 添加文件到暂存区           | `git add <文件路径>` 或 `git add .`     |
| 提交更改                   | `git commit -m "提交信息"`              |
| 查看提交历史               | `git log`                               |
| 查看文件的修改历史         | `git log <文件路径>`                    |
| 查看某次提交的修改         | `git show <提交哈希>`                   |
| 恢复文件的某个版本         | `git checkout <提交哈希> -- <文件路径>` |
| 恢复到最新版本             | `git checkout main -- <文件路径>`       |
| 创建分支                   | `git branch <分支名>`                   |
| 切换分支                   | `git checkout <分支名>`                 |
| 创建并切换分支             | `git checkout -b <分支名>`              |
| 合并分支                   | `git merge <分支名>`                    |
| 删除分支                   | `git branch -d <分支名>`                |
| 拉取远程分支               | `git pull origin <分支名>`              |
| 推送本地分支               | `git push origin <分支名>`              |
| 查看远程仓库               | `git remote -v`                         |
| 撤销工作区修改             | `git checkout -- <文件路径>`            |
| 撤销暂存区修改             | `git reset HEAD <文件路径>`             |
| 回退到某次提交（保留修改） | `git reset <提交哈希>`                  |
| 回退到某次提交（丢弃修改） | `git reset --hard <提交哈希>`           |
| 撤销某次提交的修改         | `git revert <提交哈希>`                 |
| 查看操作日志               | `git reflog`                            |
| 暂存当前修改               | `git stash`                             |
| 恢复暂存的修改             | `git stash pop`                         |

### **四、操作示例**

#### **场景 1：恢复文件的某个版本**

1. 查看文件历史：

   ```
   git log README.md
   ```

2. 恢复文件到指定版本：

   ```
   git checkout 946b401 -- README.md
   ```

3. 提交更改：

   ```
   git commit -m "恢复 README.md 到 946b401 版本"
   ```

#### **场景 2：恢复到最新版本**

1. 恢复文件到最新版本：

   ```
   git checkout main -- README.md
   ```

2. 拉取远程最新代码：

   ```
   git pull origin main
   ```

### **五、注意事项**

1. **备份数据** 在执行 `git reset --hard` 或 `git checkout` 前，确保工作目录和暂存区没有未保存的修改。
2. **团队协作** 如果仓库是多人协作的，避免使用 `git reset --hard` 回退已推送的提交，优先使用 `git revert`。
3. **找回丢失的提交** 如果不小心回退了提交，可以通过 `git reflog` 找回丢失的提交哈希。

通过以上方法，你可以轻松地回到某个版本的文件，查看或复制代码，然后再恢复最新版本。如果仍有疑问，请提供具体场景进一步分析。
