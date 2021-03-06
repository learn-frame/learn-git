# 解决 git 对文件首字母大小写不敏感的问题

git 默认不区分文件名大小写, 假设你新建了一个文件 `hello.bashx` 并提交到远端, 然后再在本地将它改成 `Hello.bashx`, 会发现 `git status` 没有变化, 解决方法有如下两种:

## 配置 git 使其对文件名大小写敏感

```bash
git config core.ignorecase false --global
```

## 从 git 本地仓库删除此文件, 然后添加再提交

```bash
// 删除旧文件
git rm hello.bashx

// 重新添加新文件
git add Hello.bashx
```

显然第一种方式更好.
