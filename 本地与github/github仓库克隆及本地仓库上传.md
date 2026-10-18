# 本地克隆与上传

> 全程使用 **SSH 协议**（默认已配置好SSH密钥）

## 一、方式1：本地已有文件： 创建Git仓库，gitclone到本地，将本地文件push到git仓库

### 1. 本地已有文件
查看已有文件的类型和内容，想好git仓库的名称和结构

### 2. 创建Git仓库
1. 登录GitHub → 右上角 `+` → **New repository**
2. 仓库名 和 本地文件夹名一致（建议）
3. **可勾选** `Add a README file`、`Add .gitignore`、`Add license`
4. 点击 `Create repository`

### 3. gitclone到本地
在本地电脑上相应位置，输入并执行
```bash
# 关联远程仓库 origin
git remote add origin git@github.com:你的用户名/仓库名.git
```

### 4. 本地暂存 + 提交 + 推送
```bash
git add .
git commit -m "初始化仓库"
git push -u origin main     # 主分支推送（新版git默认分支名 main）
```
> `-u`：绑定上游分支，后续直接 `git push` 即可

---
## 二、方式2：本地仓库 → 初始化为Git仓库 → 关联并推送到GitHub（推荐）
### 1. 本地创建目录并进入, 初始化为本地Git仓库
```bash
# 创建文件夹（自定义仓库名）
mkdir my-project
# 进入文件夹
cd my-project
```

```bash
git init
```

### 2. 前往 GitHub 网页端**手动新建空仓库**

### 3. 复制仓库 SSH 地址，本地关联远程

```bash
# 关联远程仓库 origin
git remote add origin git@github.com:你的用户名/仓库名.git
```

### 4. 首次推送
```bash
git add .
git commit -m "初始化仓库"
```

```bash
# 主分支推送（新版git默认分支名 main）
git push -u origin main
```
> `-u`：绑定上游分支，后续直接 `git push` 即可

---

# 常见问题排查

1. 提示权限 denied：检查 GitHub 账号是否添加了本机 ~/.ssh/id_rsa.pub 公钥
2. 首次连接询问 yes/no：输入 yes 回车即可（信任主机）
3. 本地测试 SSH 连通性：
```bash
ssh -T git@github.com
```
出现 Hi 用户名! You've successfully authenticated... 代表连接正常。

# 极简流程总结
1. `mkdir 仓库名 && cd 仓库名`
2. `git init`
3. 新建文件 → `git add . && git commit -m "初始化"`
4. GitHub 网页建**空仓库**，复制SSH地址
5. `git remote add origin 仓库SSH地址`
6. `git push -u origin main`