#  如何在本地用ssh链接远端github
>  windows 版本

> 好处：成功连链接以后，每次都直接用git就行， 不必再次登录---**以后 push/pull 完全不用输密码**

## 一、生成 SSH 公钥 + 私钥
1. 打开 Git Bash 或者 cmd，cd 到**~/.ssh**文件夹. 如果没有，就要先新建， 用md命令 

2. 运行下面这行（生成 两个文件： 一个公钥文件，一个私钥文件）：
```bash
ssh-keygen -t ed25519 -f "起的文件名" -C "comment信息，用于识别机器等"
```
>  ed25519 非唯一选项。ssh-keygen后面的option可以根据自己的喜好书写
>  
3. 连续按 **3 次回车**，不要设置密码！（设置密码反而每次都要输，我们要免密）
##  二、查看并复制公钥
继续在 Git Bash  中执行：
```bash
cat 文件名.pub
```
或 cmd 中
```cmd
type 文件名.pub
```
或，直接找到 文件名.pub，用notepad记事本打开。

会输出一段以`ssh-ed25519 ... 结尾的字符串。**把这一整行全部复制！**
##  三、把公钥粘贴到 GitHub
打开 GitHub 官网：
1. 右上角头像 → **Settings**
2. 左侧 **SSH and GPG keys**
3. 点 **New SSH key**
4. Title 随便写（比如：我的笔记本）
5. Key 类型保持 **Authentication key**
6. 把刚才复制的**公钥**粘贴到大框里
7. 点 **Add SSH key**

 完成！
##  四、把你的仓库改成 SSH 地址（关键！）
进入你的仓库文件夹：
```bash
cd 本地文件夹
```

执行这条命令，切换成 SSH：
```bash
git remote set-url origin xxxxx
```
xxx 是仓库url， 在这里下图中的位置复制就行
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/a9bbb0e5649a4f9bb94afcfa7dc7f3f2.png)

> 这个我弄了，没有成功。我没管，后续也successfully connect 了
##  五、测试是否成功
```bash
ssh -T git@github.com
```
出现：
```
Hi xxx! You've successfully authenticated...
```
就说明 **SSH 配置成功！**

如果出现下面的情况 denied

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/8c474a75348c41859c75a5a6b9c0cce5.png)
要在.ssh文件下建立一个 config 文件， 加入以下信息

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/14139e08a54a45d7bb59ea5a0e4bd72d.png)

# 六、以后提交代码，直接免密
```bash
git add .
git commit -m "更新内容"
git push
```
**不用输密码，直接成功！**

---

# 超简总结
1. 生成密钥：`ssh-keygen -t ed25519 -C "---"`
2. 复制公钥：`cat ----.pub`
3. 粘贴到 GitHub → Settings → SSH keys
4. 仓库切换 SSH 地址
5. 永久免密
