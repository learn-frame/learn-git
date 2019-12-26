# 删除本地远程跟踪分支

在远端, 如 GitHub 上手动删除了某个分支, 在本地使用 `git branch -a` 仍然能显示哪些已在远端被删除的分支.

通过 `git remote prune origin`, 再运行 `git branch -a` 时就干净了~