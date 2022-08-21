# 基础概念

## 原理

在 .git 的 object 文件夹中存储了 commit, tree, blob 三种类型的对象. 这三者也是 git 最重要的三个对象.

commit 不必多说, 就是我们每次 git commit 生成的那个对象, 有 tree, parent, author, committer 等对象.

tree 就是这个 commit 对应的文件状态的一个快照. 它是以文件夹维度的, 比如下图 912fa6 就是 415c5 这个 commit 的树, 而 912fa6 这棵树下又存在文件夹 images 和 styles. 那么这些文件夹就以 912fa6 的子树存在.

blob 即为单个文件, 之所以使用 blob, 是因为 git 把两个内容相同的文件视为一个 blob, 这意味着某个工程有 a.js, b.js, 但它俩内容完全一致, git 就认为是一个 blob, 这样就节省了空间.

![Commit, Tree, Blob](https://edge.yancey.app/beg/pikqp287-1661002559568.png)

## 查看各种 hash

可以通过以下命令来看一个 hash 对应的类型和文件内容:

```bash
git cat-file -t 912fa6 # 查看 912fa6 这个 hash 的类型
git cat-file -p 912fa6 # 查看 912fa6 这个 hash 的文件内容
```

![查看各种 hash](https://edge.yancey.app/beg/mc041oka-1661004376292.png)

## 分离头指针与 HEAD

当 checkout 到某个 commit 时, 因为没有关联任何分支, 这就叫分离头指针(HEAD Detected), git 会给你一个 warning, 希望你给它指定一个分支名.

![分离头指针](https://edge.yancey.app/beg/9m3lfyfe-1661013931591.png)

我们使用 git log 可以看出, HEAD 没有指向任何分支.

![分离头指针](https://edge.yancey.app/beg/zuiio82z-1661014022054.png)

再说一下 HEAD, HEAD 指向就是最新的 commit, 因此你可以用 `HEAD^` 或者 `HEAD~` 指代本次提交的父 commit; 用 `HEAD^2` 或者 `HEAD~2` 指代本次提交的爷 commit.

## fast-forward

本地分支往远端分支做 push, 如果远端分支不是本地分支的祖先, 那它俩就不是 fast forward 了. 反之, 它俩就是 fast forward 的关系. 解决方式如下:

```bash
gti fetch / git merge --allow-unrelated-histories origin/master
git fetch / git rebase
git pull --rebase
```

## 创建分支

创建分支有下面两种方式, 第二种的好处是创建分支并切换到该分支.

```bash
git branch feature/xxx

git checkout -b feature/xxx
```

## merge 和 rebase 的区别

考察下图这个情形, 欲将 bugFix 分支合并到 master 分支:

![before-merge-or-rebase](https://edge.yancey.app/beg/986jgi5x-1661064573364.jpg)

### git merge

merge 会创建一个新的 commit, 此时 master 现在指向了一个拥有两个父节点的提交记录. 假如从 master 开始沿着箭头向上看, 在到达起点的路上会经过所有的提交记录. 这意味着 master 包含了对代码库的所有修改.

![after-merge](https://edge.yancey.app/beg/r4ccsxdz-1661064573235.jpg)

### git rebase

rebase 实际上就是取出一系列的提交记录, "复制"它们, 然后在另外一个地方逐个的放下去. rebase 的优势就是可以创造更线性的提交历史.

![after-rebase](https://edge.yancey.app/beg/zxp7ccq9-1661064573235.jpg)

## 分离的 Head

分离的 Head 是指你可以 checkout 到指定的 commit 而非 branch.

```bash
git checkout 1e2f53

git checkout HEAD^

git checkout master^

git checkout HEAD~4

# 强制修改分支位置
# 下面的命令会将 master 分支强制指向 HEAD 的第 3 级父提交
git branch -f master HEAD~3
```

## 撤销修改之 revert VS reset

一言以蔽之: git reset 是把 HEAD 向后移动, 而 git revert 是 HEAD 继续前进. git reset 就是回退到上一次提交, 本次提交就被删掉了(实际被删掉的 commit 被放到了暂存区, 并未被完全移除); git revert 会创建一个新的 commit, 使这个新的 commit 跟上一次提交相同.

下面的图例中, 左图为 reset, 右图为 revert

![reset](https://edge.yancey.app/beg/aqgde5eg-1661064573535.jpg)
![revert](https://edge.yancey.app/beg/nvratmvx-1661064573530.jpg)

## git cherry-pick

用于将某些次提交合并到一个分支, 比如在 feature/a 提交了三个 commit, 分别是 5e2e1f0, cdc0c1e, a7fef64, 我想取前两个提交合并到另一个分支 feature/b, 可以这么做:

```bash
git checkout feature/b

git cherry-pick 5e2e1f0 cdc0c1e
```

## git rebase -i HEAD~

命令行的 rebase 操作

## git fetch

- 从远程仓库下载本地仓库中缺失的提交记录
- 更新远程分支指针(如 origin/master)

## git log

```bash
git log
git log -n4 # 只看最新四条
git log --oneline # 精简的 log
git log --all --graph # 查看所有分支的 log,
```

## git help

下面例子打开 web 页面关于 git log 的教程文档.

```bash
git help --web log
```

## git diff

```bash
git diff # 工作区和暂存区的差异
git diff -- README.md docs/concept.md # 指定文件工作区和暂存区的差异
git diff --cached # 暂存区和 HEAD 的差异

git diff feat/a master -- README.md # 两个分支之间 diff 的比较, 可以指定文件
```

## git reset

```bash
git reset --hard XXXXXX # 强制回退到某个 commit, 这导致之后的 commit 全部消失
```

## git rm / git mv

删除文件和修改文件名的标准做法. 虽然大部分情况都会先手动删除, 手动修改文件名. 再 git add . 一把梭. 但用这两个最优雅, 虽然我懒得用...

## git stash

```bash
git stash
git stash list
git stash apply # 恢复 stash 区到工作区, 但保留 stash
git stash pop # 恢复 stash 区到工作区, 会删除最新的 stash
```
