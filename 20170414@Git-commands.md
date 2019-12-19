# GIT常用命令汇总
_By zhaigf, Jun 2, 2014_

> 常用GIT命令汇总，不断更新中

_* update Apr  8, 2019_
_* update Dec 17, 2019_

#### 1. 如何恢复被误删除的文件？

直接从本地把文件checkout出来，具体做法：
```
git checkout file
```

同时恢复多个被删除的文件：
```
git ls-files -d | xargs -i git checkout {}
```

#### 2. 如何恢复历史版本的代码？
```
git branch <new-branch-name> <version>   # 新建所需要版本的分支
git checkout <new-branch-name>           # 检出分支代码
```

#### 3. 如果提交代码后发现某些代码还未加入，如何补充提交？
```
git commit --amend   # 可在上次提交的基础增加代码文件
```

#### 4. 在提交时发现某些文件错误地stage了，如何恢复？
```
git reset HEAD <file>
```

#### 5. 如何修改某次提交的comment？
如果是最近一次，使用
```
git commit --amend
```

如果不是最近一次，使用如下命令：
```
git rebase -i HEAD~commit_count    # 将所要修改和那次提交的"pick"改成"edit"
git commit --amend
git rebase --contine
```

#### 6. git带分支的push和pull
```
git push bb develop:develop
git pull bb develop         # 到当前分支
```

#### 7. git创建可共享的本地库（可以作为远程库存放在网盘中）
```
git init --bare --shared    # 在需要创建的目录中执行
```

#### 8. git中文文件名无法正常显示
```
git config core.quotepath false # core.quotepath设为false的话，就不会对0x80以上的字符进行quote，中文显示正常
```

#### 9. 在开发流上Rebase master流的内容
```
git checkout dev-branch
git rebase master
```

如果有冲突，需要修正冲突文件并stage
```
git add confilct-file
git rebase --continue
```

#### 10. 显示分支提交结构
```
git log --oneline --decorate --graph --all
```

#### 11. 分支合并

切换到Master分支
```
git checkout master
```

对develop分支进行合并
```
git merge --no-ff develop
```

#### 12. 创建远程分支

假设本地当前分支为master, 需要创建的分支是test。

在当前分支下创建test的本地分支
```
git checkout -b test
```

将test分支推到远程，假设远程的仓库为origin
```
git push origin test
```

将本地分支test关联到远程分支test上
```
git branch --set-upstream-to=origin/test
```

查看所有分支
```
git branch -a
```

