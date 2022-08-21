# 清除暂存区文件

有时你 git add. 了一批文件, 但不想要了, 可以通过 `git reset HEAD`, 将这些变更在暂存区中清理掉.

![git reset HEAD](https://edge.yancey.app/beg/a79drb0l-1661072058402.png)

有时你本地为某文件做了变更, 但想要暂存区中这个文件的变更, 可以通过 `git checkout -- index.md`. 举个例子:

你有一个文件 index.md, 里面是 `hello, world`; 然后把它改成了 `Hello, World`, 并 git add . 到了暂存区. 然后你继续在本地修改这个文件, 改成了 `hello, world!`. 最后发现还不如暂存区的 `Hello, World` 好. 所以使用 `git checkout -- index.md` 就可以回退到暂存区里的改动.
