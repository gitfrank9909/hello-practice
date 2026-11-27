# hello-practice

一个用来练手 Git / GitHub 协作流程的练习仓库。

目标：一个人就能走完 **建分支 → 提交 → 推送 → 发 Pull Request → 合并** 的完整闭环，不需要别人配合。

---

## 0. 准备：把仓库弄到本地

```bash
git clone https://github.com/gitfrank9909/hello-practice.git
cd hello-practice
```

> 如果建仓库时勾选了 `Add a README file`，clone 下来就有本文件。
> 如果是空仓库，把本文件放进目录，然后 `git add . && git commit -m "docs: add README"` 即可。

---

## 1. 先记住四个词

| 词 | 含义 |
|---|---|
| `main` | 稳定主线，随时应该是「能用」的状态 |
| `feature/xxx` | 从 main 切出去的工作分支，改动都发生在它上面 |
| commit | 一次带说明的改动快照 |
| PR (Pull Request) | 请求「把 A 分支的改动合并进 B 分支」的申请，附带 diff 和讨论区 |
| merge | 把分支的改动真正并回主线 |

规则只有一条：**不要直接在 main 上改**。PR 的本质是「我这条分支上的改动，请你合并到那条分支」，所以必须先有分支。

---

## 2. 完整练习流程

### 第 1 步 · 切出分支

```bash
git checkout main
git pull
git checkout -b feature/first-pr
```

`git branch` 可以看到当前在 `feature/first-pr` 上，前面有个 `*`。

### 第 2 步 · 改点东西并提交

打开本文件，把最下面的「练习签到」打上勾，随便加一行自己的备注。然后：

```bash
git add README.md
git commit -m "docs: 完成第一次 PR 练习"
```

想确认改了什么：`git status`、`git diff`、`git log --oneline --graph`。

### 第 3 步 · 推送分支到远端

```bash
git push -u origin feature/first-pr
```

`-u` 会建立追踪关系，之后在这个分支上直接 `git push` 就行。

### 第 4 步 · 发起 Pull Request（网页）

推上去后打开仓库页面，GitHub 通常会弹出黄色横幅 `Compare & pull request`，点它；
或者进 `Pull requests` → `New pull request`。

关键是两个下拉框别选反：

- **base**: `main` —— 改动要合到哪
- **compare**: `feature/first-pr` —— 你的改动在哪

填标题和描述（写清「做了什么、为什么」，比 `update` 有用得多）→ `Create pull request`。

### 第 5 步 · 评审与讨论

切到 `Files changed` 逐行看 diff，可以给自己留条评论。
要改就在同一分支继续 `commit` + `push`，PR 会自动更新，不用重开。

### 第 6 步 · 合并收尾

点 `Merge pull request` → `Confirm` → 顺手点 `Delete branch` 删掉已合并的分支。
三种合并方式里，新手选默认的 **Create a merge commit** 最不容易出错。

合并后回到本地：

```bash
git checkout main
git pull
git branch -d feature/first-pr
```

---

## 3. 命令速查

| 命令 | 作用 |
|---|---|
| `git status` | 看当前在哪个分支、改了哪些文件 |
| `git branch` | 列出本地分支 |
| `git checkout -b <name>` | 新建并切换到分支 |
| `git add .` | 把改动放入暂存区 |
| `git commit -m "msg"` | 生成一次提交 |
| `git push -u origin <branch>` | 推送分支并建立追踪 |
| `git pull` | 拉取并合并远端更新 |
| `git log --oneline --graph` | 看提交历史与分支图 |

---

## 4. 进阶：给别人仓库提 PR

区别只在第一步。没有对方仓库的写权限时：

1. 在对方仓库点 **Fork**，复制一份到自己账号下
2. clone **自己那份**（不是原仓库）
3. 建分支 → 提交 → push 到自己的 fork
4. 发 PR 时 **base 指向原仓库的 main**，compare 指向自己 fork 上的分支

这就是开源贡献的标准路径。

---

## 5. 练习签到

- [ ] 我成功切出了分支
- [ ] 我提交了改动并 push 到远端
- [ ] 我发出了第一个 Pull Request
- [ ] 我把它合并进了 main

> 把上面的 `[ ]` 改成 `[x]`，就是本次练习的第 2 步改动。
