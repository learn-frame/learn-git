# 合并几个 commit

## 合并几个连续的 commit

和修改 commit 的内容一样, 也使用 git rebase -i

假如想把前七个进行合并, 就选一个作为 pick(必须要有一个是 pick 的), 剩下的六个变成 s, 也就是 squash.

![使用 squash](https://edge.yancey.app/beg/5jlwd2g8-1661066536547.png)

保存后进入如下页面, 你可以给它个总的 commit msg, 比如叫做**学习 vite 配置和插件系统**.

![给一个总的 commit msg](https://edge.yancey.app/beg/k6o674k1-1661066536549.png)

可以看到被合并了.

![合并之后的 log](https://edge.yancey.app/beg/1ri6yf1o-1661066536550.png)

## 合并几个不连续的 commit

也是通过 git rebase -i, 比如下面代码, 我想合并 123456 和 abcdef 两个 commit. 我需要把 abcdef 这一行手动剪切到 123456 这一行下面, 并将 abcdef 的 pick 改成 squash.

```bash
pick 123456 feat:xxx
pick 7890jq feat: yyy
pick abcdef feat: zzzz
```

也就是变成下面的形式:

```bash
pick 123456 feat:xxx
s abcdef feat: zzzz
pick 7890jq feat: yyy
```

保存后, 会让你 `git rebase --continue`, 才会进入合并 commit msg 信息的页面.
