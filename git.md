# Git 笔记



### 本地仓库上传到github

```bash
git init
git add README.md
git commit -m "first commit"
git remote rm origin
git remote add origin https://github.com/eatamath/git-tutorial.git
git pull --rebase origin master  //不加这句可能报错，原因是 github 中的 README.md 文件不在本地仓库中
//可以通过该命令进行代码合并
git push -u origin master
```

### git push

用本地分支`lbranch-3`覆盖远程分支`rbranch-1`

```bash
git push -f origin master:refs/for/gpu-server
```

### git ignore

```bash
git rm -r --cached . 
git add .
git commit -m "update .gitignore"
```

