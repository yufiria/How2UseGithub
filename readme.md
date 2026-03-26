# Git 快速入门

只记这几个命令

## 1) 配置

```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
```

## 2) 核心 6 命令

```bash
git clone <仓库地址>                # 拉代码
git status                          # 看改动
git add .                           # 加入暂存区
git commit -m "本次改动说明"         # 提交
git pull                            # 先同步远程
git push                            # 推送到远程
```

## 3) 正常的 4 步

先 pull，再改；改完 commit，最后 push。

```bash
git pull
# 改代码...
git add .
git commit -m "本次改动说明"
git push
```

## 4) 一个常用补充

```bash
git checkout -b feature/xxx         # 新建并切换分支
```
