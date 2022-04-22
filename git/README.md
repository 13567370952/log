# git
## 22-04-22
### git操作

新建仓库
git init
git add README.md
git commit -m "first commit"
git remote add origin xxx
git push -u origin master

已存在
git remote add origin xxx
git push -u origin master


添加
git add .
提交
git commit -m 'some info'

查看日志
git log --pretty=oneline --all --graph --abbrev-commit

推送
git push -u origin master

重置
git reset --heard id

分支查看
git branch 
git branch xxx

切换分支
git checkout xxx
git checkout -b xxx

合并
git merge

下载本地
git clone xxx mytest
git fetch

git pull origin master

自定义本地信息
git config --global user.name "xxx"
git config --global user.email "xxx"

生成秘钥
ssh-keygen -t rsa
打印公钥
cat ~/.ssh/id_rsa_pub。
cat /c/Users/2020-2/.ssh/id_rsa.pub
验证
echo -n "a8226993e59fcc6a314f10aa18af344d2054bd6337d8dc6559173914ff432f7e" | ssh-keygen -Y sign -n gitea -f /c/Users/2020-2/.ssh/id_rsa.pub
ssh -T git@gitee.com -p xxxx