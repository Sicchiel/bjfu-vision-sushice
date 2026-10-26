# Task 1 — 终端文件操作命令记录

环境：Ubuntu 22.04 + bash

## 1. 新建目录
```bash
mkdir -p task1/playground/src task1/playground/backup
ls -ld task1 task1/playground task1/playground/src task1/playground/backup
```
`-p`：父目录不存在时一起创建，已存在不报错。

## 2. 创建文件
```bash
printf 'hello from task1\n' > task1/playground/src/a.txt
```

## 3. 复制文件
```bash
cp task1/playground/src/a.txt task1/playground/backup/a.txt.bak
```
目录递归复制用 `cp -r`。

## 4. 移动 / 重命名
```bash
mv task1/playground/backup/a.txt.bak task1/playground/backup/b.txt
```
同目录内 `mv` 即重命名。

## 5. 修改权限
```bash
chmod 640 task1/playground/backup/b.txt   # 属主读写，同组只读，其他无权限
chmod 750 task1/playground/src            # 属主读写执行，同组读执行，其他无权限
ls -l task1/playground/backup task1/playground/src
```
权限位含义：`r=4 w=2 x=1`，三组依次是属主 / 属组 / 其他。

## 6. 删除文件
```bash
rm -f task1/playground/backup/b.txt
```
删目录用 `rm -r`，`-f` 表示文件不存在也不报错。

## 7. 查看结果
```bash
find task1 -print | sort
```

## 8. Git 分支与冲突
```bash
git init -b main
git add -A && git commit -m "chore: 初始化培训仓库"
git checkout -b dev
# 改 README
git commit -am "feat(dev): 更新版本号并新增 dev 说明"
git checkout main
# 改 README 同一行
git commit -am "fix(main): 更新版本号并补充热修复说明"
git merge dev            # 产生冲突
# 编辑 README 删除冲突标记后
git add README.md && git commit -m "merge: 合并 dev 到 main 并解决冲突"
git log --graph --oneline --decorate --all
```

## 9. GitHub 推送
```bash
ssh-keygen -t ed25519 -C "你的邮箱"      # 已有可跳过
cat ~/.ssh/id_ed25519.pub                # 贴到 GitHub → Settings → SSH and GPG keys
ssh -T git@github.com
git remote add origin git@github.com:<用户名>/training.git
git push -u origin main
git push origin dev
```
