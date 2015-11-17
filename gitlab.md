# gitlab安装使用

## gitlab安装
### 安装方式：
 有两种安装方式
### 第一种：采用 Omnibus方式安装
Omnibus方式安装支持Ubuntu 12.04/14.04, centos 6/7。
> 优点：安装过程简单，安装速度快。采用包安装方式，安装的软件包便于管理。
> 缺点：数据库默认采用PostgreSQL，不支持mysql，不容易定制。
Omnibus文档
> `http://doc.gitlab.com/omnibus/`
安装方法和下载地址：
> `https://about.gitlab.com/downloads`
packages list:
> `https://packages.gitlab.com/gitlab/gitlab-ce`

### 第二种：源码安装方式
> 优点：可定制性强。数据库既可以选择MySQL,也可以选择PostgreSQL
> 缺点：依赖软件包太多，配置流程繁琐，容易出现各种各样的问题
安装文档：
`http://doc.gitlab.com/ce/install/README.html

Omnibus gitlab源码目录位置
`/opt/gitlab/embedded/service/`
nginx配置文件
`/var/opt/gitlab/nginx`
git版本库地址
`/var/opt/gitlab/git-data`

收费版和免费版比较
`https://about.gitlab.com/features/#compare`


## gitlab 基本功能
### 1、访问方式：
可以通过http和ssh两种方式提交代码。
http方式每次操作都需要输入用户名密码，ssh方式需要添加ssh公钥
添加ssh-key：
login>>Profile Settings>>ssh keys

### 2、用户和项目权限
分为Guest,Reporter,Developer,Master,Owner这几个角色，这几个角色的权限从低到高排列。
> Guest:只能提交评论和问题
> Reporter:可以拉取和下载代码，不可以提交代码、创建分支、发起合并请求
> Developer: 能够推送和删除没有保护的分支,添加标签，发起和管理合并请求
> Master:可以对没有保护和有保护的分支进行操作，发起和管理合并请求，管理项目人员，修改项目信息。
> Owner:拥有以上用户的所有权限，可以删除项目

详细权限列表：
`https://gitlab.com/help/permissions/permissions.md`
### 3、代码提交和审查流程
1. 开发成员克隆项目到自己本地。
2. 创建自己的分支。
 3. 在自己的分支上写代码，并提交。
4. 推送到远程服务器，分支是自己的分支。
5. 创建一个合并请求，指定审核人。
6. 团队的管理员或者领导者审查并且决定是否合并员工提交的分支到主分支上。
（比如员工小明,角色developer，就推送到xiaoming分支。分支的命名规则为开发人员姓名+所开发的功能。 小明的分支名：xiaoming-newfeature,也可以简写）

## 使用文档
`https://gitlab.com/help`

## 待解决的问题
1. SMTP邮箱配置不成功
2. 开发人员的命令行工具未解决

## 安装和使用过程中遇到的问题：
1. 在浏览器中访问GitLab出现502、500错误 原因：内存不足。
	解决办法：gitlab最低要求是1G内存，建议2核心、2G内存。
2. clone时会出现401错误 原因：git版本太低。 解决办法： git版要求是 1.7.10+ 建议2.0以上。
3. `8080`端口冲突 原因：由于unicorn默认使用的是8080端口。
	解决办法：打开/etc/gitlab/gitlab.rb,打开`# unicorn['port'] = 8080的`注释，将8080修改为9090。
相关文档：
`https://github.com/gitlabhq/gitlabhq/blob/master/doc/install/installation.md`
`https://about.gitlab.com/applications/`
`http://doc.gitlab.com/omnibus/`




## 第三方工具
`https://www.google.com/search?q=gitlab&oq=gitlab+&aqs=chrome..69i57j69i60l3j69i65j69i59.2101j0j7&sourceid=chrome&es_sm=91&ie=UTF-8#q=gitlab+command-line+wrapper`
gitlab command line tools
`https://github.com/numa08/git-gitlab`

## 本地测试环境用户
gitlab user
root   lab123123
php1/2/3 lab123123

vagrant user
php1/2/3  123123
