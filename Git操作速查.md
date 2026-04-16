# Git操作速查

## 当前仓库信息

- 本地仓库路径：`D:\cursorwj\GN_viaim`
- 默认分支：`main`
- 远端名称：`origin`
- 远端地址：`https://github.com/wanyongqi/gn_viaim.git`

## 最常用流程

### 1. 查看当前状态

```powershell
git status
```

用途：
- 看当前有哪些文件被修改、暂存、未跟踪
- 看本地分支和远端分支的关系

### 2. 暂存改动

暂存全部改动：

```powershell
git add .
```

只暂存某一个文件：

```powershell
git add "630版本/630简约版测试点.md"
```

### 3. 提交到本地仓库

```powershell
git commit -m "docs: 更新630简约版测试点"
```

用途：
- 把已经暂存的改动提交到本地仓库

### 4. 推送到远端仓库

```powershell
git push
```

用途：
- 把本地已经提交的内容推送到 GitHub

## 新仓库初始化流程

如果当前目录还不是 Git 仓库，可用下面流程初始化：

```powershell
git init
git branch -M main
git add .
git commit -m "chore: initial commit"
git remote add origin https://github.com/wanyongqi/gn_viaim.git
git push -u origin main
```

## 查看信息常用命令

### 查看提交历史

```powershell
git log --oneline
```

### 查看远端地址

```powershell
git remote -v
```

### 查看分支跟踪关系

```powershell
git branch -vv
```

### 查看最近一次提交改了什么

```powershell
git show --stat
```

### 查看未暂存改动

```powershell
git diff
```

### 查看已暂存但未提交的改动

```powershell
git diff --cached
```

## 日常推荐用法

如果你只改了一个文档，建议优先按文件提交，不要默认 `git add .`：

```powershell
git status
git add "630版本/630简约版测试点.md"/git add .
git commit -m "docs: 更新630简约版测试点（你的提交说明）"
git push
```

这样更不容易把其他顺手改动一起带进去。

## 常见状态说明

### `nothing to commit, working tree clean`

意思：
- 当前没有可提交改动

### `untracked files`

意思：
- 有新文件还没有纳入 Git 跟踪

处理：

```powershell
git add .
```

### `Changes not staged for commit`

意思：
- 文件改了，但还没加入暂存区

处理：

```powershell
git add .
```

### `main...origin/main [ahead 1]`

意思：
- 本地比远端多 1 个提交
- 本地已经提交成功，但还没有推到远端

处理：

```powershell
git push
```

### `main...origin/main [behind 1]`

意思：
- 本地落后远端 1 个提交

处理：

```powershell
git pull
```

## 常见报错及处理

### `fatal: your current branch 'main' does not have any commits yet`

意思：
- 仓库已初始化，但还没有第一次提交

处理：

```powershell
git add .
git commit -m "chore: initial commit"
```

### `fatal: not a git repository`

意思：
- 当前目录不是 Git 仓库，或者不在正确目录

处理：
- 先确认当前路径
- 进入正确目录后再执行 Git 命令

### `fatal: unable to access 'https://...': Recv failure: Connection was reset`

意思：
- 到 GitHub 的 HTTPS 连接被重置
- 一般是网络、代理、VPN 或防火墙问题

处理：

```powershell
git push
```

如果重试仍失败：
- 检查浏览器是否能正常访问 GitHub
- 切换网络或代理
- 必要时改用 SSH

### `Permission denied (publickey)`

意思：
- 走 SSH 推送时，本机没有可用 SSH key，或 GitHub 没配置公钥

处理：
- 生成 SSH key
- 把公钥添加到 GitHub
- 再执行 `git push`

## 最短记忆版

```powershell
git status
git add .
git commit -m "你的提交说明"
git push
```

## 提交信息建议

- `docs:` 文档内容更新
- `chore:` 仓库配置、`.gitignore`、规则文件调整
- `test:` 测试用例、测试数据、验证脚本调整

示例：

```powershell
git commit -m "docs: 更新630简约版测试点"
git commit -m "chore: 更新Cursor规则和skills"
git commit -m "test: 补充录音相关测试用例"
```
