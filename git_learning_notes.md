
* 下载安装git
* vim ~/.gitconfig
* name email
* alias(命令的缩写)
    - co=checkout(切换分支)
    - ci=commit
    - st=status
    - pl=pull
    - ps=push
    - dt=difftool(提交代码前对比代码)
    - ca=commit -am(备注信息)
    - b=branch
* 项目的建立(ssh公钥)
    - ssh-keygen -t rsa -C '邮箱地址‘  一路回车
    - ls -al (显示所有文件，包括git的隐藏文件)
    - cd .ssh/       ls -al
    - id_rsa:私钥  id_rsa.pub:公钥
    - cat id_rsa.pub
* 码云 组织--->新建仓库--->管理--->公钥管理--->添加个人公钥
* 仓库里复制SSH（不用每次输入账号密码）
* 回到命令行 cd
* ls(查看当前文件夹)
* mkdir doc(新建文件夹)。cd进去
* git clone (仓库里的ssh复制接到clone后面)    yes

* cd 到对应的仓库里，可以查看文件
* 在仓库下， vim .gitignore  (忽略一些文件)
    - insert
    - .DS_Store(mac下存储文件夹信息的)
    - node_modules
    - dist
    - *.log(日志，不需要)
* git st 查看状态
    - git add .  (提交到本地)
    - git ca "备注信息“  (用于代码提交到本地)
    - git push (推送到远程)

* git在远程和在本地的仓库都新建完成



* git 更新
    - git st 查看状态
    - git pull
    - git merge " "(没有引号，里面填分支名称，比如 origin)  master
        ----> 例如：git merge origin master
    - git add .
    - git ca "备注"
    - git push
    - git tag tag-order   (打标签： 标签名为tag-order)
    - git push origin tag-order (给远程的origin的分支打上tag-order的标签)
