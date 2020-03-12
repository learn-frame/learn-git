# 基础概念

## 创建分支

创建分支有下面两种方式, 第二种的好处是创建分支并切换到该分支.

```batch
git branch feature/xxx

git checkout -b feature/xxx
```

## merge 和 rebase 的区别

考察下图这个情形, 欲将 bugFix 分支合并到 master 分支:

![before-merge-or-rebase](../images/before-merge-or-rebase.jpg)

### merge

merge 会创建一个新的 commit, 此时 master 现在指向了一个拥有两个父节点的提交记录. 假如从 master 开始沿着箭头向上看, 在到达起点的路上会经过所有的提交记录. 这意味着 master 包含了对代码库的所有修改.

![after-merge](../images/after-merge.jpg)

### rebase

rebase 实际上就是取出一系列的提交记录, "复制"它们, 然后在另外一个地方逐个的放下去. rebase 的优势就是可以创造更线性的提交历史.

![after-rebase](../images/after-rebase.jpg)
