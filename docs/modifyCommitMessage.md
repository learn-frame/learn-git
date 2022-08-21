# 修改 commit 的内容

## 修改最新的一条 commit msg

```bash
git commit --amend
```

## 修改非最新的 commit msg

以下面为例, 我们想修改 c5ba018 这条 commit 的 msg, 要通过 rebase 交互式界面完成.

![git log](https://edge.yancey.app/beg/k0twcpba-1661063526075.png)

需要注意的是, 如果你要修改 c5ba018, 就需要定位到它的父 commit 即 7158d14, 如下所示.

```bash
git rebase -i 7158d14
```

此时你就可以看到 7158d14 所有的四个子 commit. 由于我们要改 c5ba018 的 msg, 所以就把前面的 pick 改成 reword 或者 r, 然后 wq 保存.

![rebase 交互式页面](https://edge.yancey.app/beg/ikxw66x2-1661063818499.png)

保存后它会立即弹出 c5ba018 这条 commit 编辑页, 你直接修改 commit msg 然后 wq 保存即可.

![修改指定 commit msg](https://edge.yancey.app/beg/ju2oe5wc-1661063986402.png)
