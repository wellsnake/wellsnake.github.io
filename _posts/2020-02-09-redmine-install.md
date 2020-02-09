---
title: "Redmine 安装说明 ( CentOS + MySql + Ruby )"
date: 2020-02-08 17:41:42
categories: jekyll update
tags: redmine centos ruby mysql
sharing: true
---

## 安装环境说明

> OS : CentOS-7
> MySql : 5.7.29
> Ruby : 2.4.6
> Rails : 5.2.4.1
> Redmine : 4.1.0

## 基本环境安装

### 修改 CentOS 的 yum 源

```shell
# 备份源文件
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
# 修改源文件
vi /etc/yum.repos.d/CentOS-Base.repo
```

将以下内容拷贝至编辑的文件内，源地址修改为中国科大的镜像地址

```shell
# CentOS-Base.repo 文件内容

# The mirror system uses the connecting IP address of the client and the
# update status of each mirror to pick mirrors that are updated to and
# geographically close to the client.  You should use this for CentOS updates
# unless you are manually picking other mirrors.
#
# If the mirrorlist= does not work for you, as a fall back you can try the
# remarked out baseurl= line instead.

[base]
name=CentOS-$releasever - Base
#mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os
baseurl=https://mirrors.ustc.edu.cn/centos/$releasever/os/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

#released updates
[updates]
name=CentOS-$releasever - Updates
# mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates
baseurl=https://mirrors.ustc.edu.cn/centos/$releasever/updates/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

#additional packages that may be useful
[extras]
name=CentOS-$releasever - Extras
# mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras
baseurl=https://mirrors.ustc.edu.cn/centos/$releasever/extras/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

#additional packages that extend functionality of existing packages
[centosplus]
name=CentOS-$releasever - Plus
# mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus
baseurl=https://mirrors.ustc.edu.cn/centos/$releasever/centosplus/$basearch/
gpgcheck=1
enabled=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
```

### 安装环境依赖的软件包

安装 Redmin 环境过程中需要许多软件依赖才能安装成功

```shell
yum install -y gcc gcc-c++ make automake autoconf libtool pcre pcre-devel zlib zlib-devel \
openssl openssl-devel vim git svn ImageMagick ImageMagick-devel ghostscript kernel-devel \
wget net-tools imake imake libxml2-devel expat-devel cmake  libaio libaio-devel bzr bison \
ncurses5-devel mysql-devel
```

### 设置安装目录

```shell
# 安装包或安装过程中的临时文件存放目录
mkdir -p /u01/src
# redmine 目录
mkdir -p /u01/server
# 日志存放目录
mkdir -p /u01/log
# 临时文件存放目录（ Rdemin 转换 pdf 时需要使用）
mkdir -p /u01/data/tmp
# Rdemin 上传附件存放目录
mkdir -p /u01/data/files
```

### 添加访问代理

> 此步骤可选，主要目的是加速 Gem 软件包的安装，也可以通过修改 Gem 的源地址来加速安装，文章后面会详细介绍

```shell
# 修改环境配置
vim /etc/profile
```

在文件末尾添加以下内容，其中{IP}根据实际情况进行修改

```shell
export http_proxy=http://{IP}:6152
export https_proxy=http://{IP}:6152
```

成功后输入以下命令使配置生效

```shell
source /etc/profile
```

### 防火墙配置

说明：

1. 本文档将 Redmine 默认访问端口设置成 80
  
2. 本文档将 MySql 默认访问端口设置成 3306

```shell
# 开启 80 端口
firewall-cmd --zone=public --add-port=80/tcp --permanent
# 开启 3306 端口
firewall-cmd --zone=public --add-port=3306/tcp --permanent
# 防火墙配置生效
firewall-cmd --reload
```

## 安装 Mysql 环境

因为Redmine[官方说明](https://www.redmine.org/projects/redmine/wiki/RedmineInstall) MySql 的版本支持为5.5 - 5.7，所以不能直接使用 yum 来安装最新版的 MySql

### 下载M ySql 官方安装源

```shell
cd /u01/src
# 下载 MySql 下载源软件包
wget https://repo.mysql.com//mysql80-community-release-el7-3.noarch.rpm
# 安装本地软件包
yum localinstall mysql80-community-release-el7-3.noarch.rpm
```

### 修改 MySql 下载源文件

因为当前启用的默认版本是下载8.0，所以需要修改文件，将其中的5.7版本设置成可用，8.0版本设置成不可用

```shell
# 查看当前启用的 MySql 安装版本
yum repolist all | grep mysql

# 系统会显示以下信息，其中 mysql80-community/x86_64为 当前默认版本
mysql-cluster-7.5-community/x86_64 MySQL Cluster 7.5 Community      禁用
mysql-cluster-7.5-community-source MySQL Cluster 7.5 Community - So 禁用
mysql-cluster-7.6-community/x86_64 MySQL Cluster 7.6 Community      禁用
mysql-cluster-7.6-community-source MySQL Cluster 7.6 Community - So 禁用
mysql-cluster-8.0-community/x86_64 MySQL Cluster 8.0 Community      禁用
mysql-cluster-8.0-community-source MySQL Cluster 8.0 Community - So 禁用
!mysql-connectors-community/x86_64 MySQL Connectors Community       启用:    141
mysql-connectors-community-source  MySQL Connectors Community - Sou 禁用
!mysql-tools-community/x86_64      MySQL Tools Community            启用:    105
mysql-tools-community-source       MySQL Tools Community - Source   禁用
mysql-tools-preview/x86_64         MySQL Tools Preview              禁用
mysql-tools-preview-source         MySQL Tools Preview - Source     禁用
mysql55-community/x86_64           MySQL 5.5 Community Server       禁用
mysql55-community-source           MySQL 5.5 Community Server - Sou 禁用
mysql56-community/x86_64           MySQL 5.6 Community Server       禁用
mysql56-community-source           MySQL 5.6 Community Server - Sou 禁用
!mysql57-community/x86_64          MySQL 5.7 Community Server       禁用:    404
mysql57-community-source           MySQL 5.7 Community Server - Sou 禁用
!mysql80-community/x86_64          MySQL 8.0 Community Server       启用
mysql80-community-source           MySQL 8.0 Community Server - Sou 禁用

# 修改安装源，启用 MySql5.7 版本安装
vim /etc/yum.repos.d/mysql-community.repo

# 将文件内 mysql57 对应的 enabled 设置成1，并将 mysql80 对应的 enabled 设置成0，因为当前只能有一个启用的版本

# mysql-community.repo 文件内容
# ......
[mysql57-community]
name=MySQL 5.7 Community Server
baseurl=http://repo.mysql.com/yum/mysql-5.7-community/el/7/$basearch/
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql

[mysql80-community]
name=MySQL 8.0 Community Server
baseurl=http://repo.mysql.com/yum/mysql-8.0-community/el/7/$basearch/
enabled=0
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
# ......
```

### 安装 MySql

```shell
# 经过上面的配置，输入以下命令后系统会自动安装 MySql5.7 版本
yum install mysql-community-server
```

### MySql 管理命令

```shell
# 启动 MySql
systemctl start mysqld.service
# 设置 MySql 为开机启用
systemctl enable mysqld.service

# 查看 MySql 服务状态
systemctl status mysqld.service
# 显示以下信息说明 MySql 服务已经成功启动
● mysqld.service - MySQL Server
   Loaded: loaded (/usr/lib/systemd/system/mysqld.service; enabled; vendor preset: disabled)
   Active: active (running) since 三 2020-02-05 11:07:55 CST; 18min ago
     Docs: man:mysqld(8)
           http://dev.mysql.com/doc/refman/en/using-systemd.html
  Process: 1058 ExecStart=/usr/sbin/mysqld --daemonize --pid-file=/var/run/mysqld/mysqld.pid
  $MYSQLD_OPTS (code=exited, status=0/SUCCESS)
  Process: 1016 ExecStartPre=/usr/bin/mysqld_pre_systemd (code=exited, status=0/SUCCESS)
 Main PID: 1091 (mysqld)
   CGroup: /system.slice/mysqld.service
           └─1091 /usr/sbin/mysqld --daemonize --pid-file=/var/run/mysqld/mysqld.pid

2月 05 11:07:54 localhost.localdomain systemd[1]: Starting MySQL Server...
2月 05 11:07:55 localhost.localdomain systemd[1]: Started MySQL Server.
```

### 修改 MySql 密码和本机访问限制

```shell
# 查看 MySql 初始密码
grep 'temporary password' /var/log/mysqld.log
# 系统会显示以下信息，其中 wI;pF>Thw9Ja 即为安装后的初始密码
2020-02-04T10:13:34.057678Z 1 [Note] A temporary password is generated for root@localhost: wI;pF>Thw9Ja
# 登陆 MySql 服务器，输入初始密码即可登陆
mysql -uroot -p

# 系登陆后统会进入 MySql 客户端模式
# 修改初始密码
ALTER USER 'root'@'localhost' IDENTIFIED BY '1234567890';
# 启用其他电脑访问 MySql
# 注意：外网生产环境不推荐这么做，建议将其中的 % 修改成需要访问的 IP 地址
use mysql;
update user set host = '%' where user = 'root';
flush privileges;
```

## 安装 Ruby 环境

### 安装 RVM

```shell
gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB

# 如果有错误信息执行以下命令
gpg --keyserver hkp://pool.sks-keyservers.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 \
7D2BAF1CF37B13E2069D6956105BD0E739499BDB

# 安装 RVM
\curl -sSL https://get.rvm.io | bash -s stable

# 将root用户加入rvm组
usermod -a -G rvm root

# 安装完成后执行 rvm 环境配置脚本
/etc/profile.d/rvm.sh

# 检查安装依赖环境
rvm requirements
```

### 安装 Ruby

```shell
# 列出当前可安装的版本
rvm list known

# 系统会显示如下信息
# MRI Rubies
[ruby-]1.8.6[-p420]
[ruby-]1.8.7[-head] # security released on head
[ruby-]1.9.1[-p431]
[ruby-]1.9.2[-p330]
[ruby-]1.9.3[-p551]
[ruby-]2.0.0[-p648]
[ruby-]2.1[.10]
[ruby-]2.2[.10]
[ruby-]2.3[.8]
[ruby-]2.4[.6]
[ruby-]2.5[.5]
[ruby-]2.6[.3]
[ruby-]2.7[.0-preview1]
# ......

# 安装 2.4 版本
rvm install 2.4

# 将安装版本设置系统默认版本
rvm use 2.4 --default
```

### 修改 Rubygems 默认源

说明：

1. 如果之前设置过代理可以略过此步骤
2. 如果访问默认源速度没有问题可以略过此步骤

```shell
# 列出默认源
gem sources
# 移除默认源
gem sources --remove https://rubygems.org/
# 添加科大源
gem sources -a https://mirrors.ustc.edu.cn/rubygems/  
```

### 安装 Rails

```shell
gem install rails -v 5.2.4.1
# 如果有报错信息则执行以下内容后再安装一次
gem install sprockets -v 3.7.2
gem install rails -v 5.2.4.1
```

## 安装 Redmine

### 下载安装包

```shell
cd /u01/src
# 下载安装包
wget https://www.redmine.org/releases/redmine-4.1.0.tar.gz
# 解压文件
tar -zxvf redmine-4.1.0.tar.gz -C /u01/server/
# 修改目录名称
cd /u01/server/
mv redmine-4.1.0/ redmine
```

### 创建数据库

```SQL
# 创建 redmine 账号和数据库
CREATE DATABASE redmine CHARACTER SET utf8mb4;
CREATE USER 'redmine'@'localhost' IDENTIFIED BY '1234567890';
GRANT ALL PRIVILEGES ON redmine.* TO 'redmine'@'localhost';
```

### 数据库配置

```shell
cd /u01/server/redmine
# 将配置文件示例修改成默认配置文件
cp config/database.yml.example config/database.yml
# 修改配置文件
vim config/database.yml
# database.yml文件内容
# ......
production:
  adapter: mysql2
  # 数据库名称
  database: redmine
  # 数据库地址
  host: localhost
  # 访问端口号，不配置默认使用3306
  port: 3306
  # 数据库用户
  username: redmine
  # 数据库用户密码
  password: "1234567890"
  # Use "utf8" instead of "utfmb4" for MySQL prior to 5.7.7
  encoding: utf8mb4
# ......
```

### 安装依赖包

```shell
# 安装 bundler
gem install bundler
bundle install --without development test
# 安装 RMagick 依赖
bundle install --without development test rmagick
# 执行 Session store secret generation
bundle exec rake generate_secret_token
```

### 数据初始化

```shell
# 执行数据库迁移脚本
RAILS_ENV=production bundle exec rake db:migrate
# 基础数据初始化，选择 zh
RAILS_ENV=production bundle exec rake redmine:load_default_data
```

### 文件目录权限设置

说明：根据「设置安装目录」章节的内容进行设置

```shell
cd /u01/server/redmine
chown -R root:root /u01/data/files /u01/log /u01/data/tmp public/plugin_assets plugins
chmod -R 755  /u01/data/files /u01/log /u01/data/tmp public/plugin_assets plugins
```

### 基础配置

```shell
# 将配置文件示例修改成默认配置
cp config/configuration.yml.example config/configuration.yml
vim config/configuration.yml
# configuration.yml 文件内容
# ......
# 附件保存路径
attachments_storage_path: /u01/data/files
# 版本管理系统日志路径
scm_stderr_log_file: /u01/log/redmine_scm_stderr.log
# imagemagick命令路径
imagemagick_convert_command: /usr/bin/convert
# ......
```

### 日志配置

```shell
# 将配置文件示例修改成默认配置
cp config/additional_environment.rb.example config/additional_environment.rb
vim config/additional_environment.rb
# 将以下内容添加到文件末尾
# additional_environment.rb 文件内容
# ......
config.logger = Logger.new('/u01/log/logfile.log', 2, 1000000)
config.logger.level = Logger::INFO
# ......
```

### 测试运行

说明：只供测试使用，生产环境不推荐

```shell
# 开启测试服务，端口为80，开放任意 IP 地址访问
bundle exec rails server webrick -e production -b 0.0.0.0 -p 80
# 浏览器访问 http://{IP} 即可访问 Redmine
# 首次用户名和密码为 admin admin
# 登陆后系统会提示修改初始密码
```

### 安装主题

说明：推荐安装 PurpleMine2 主题

```shell
cd /u01/server/redmine
# 下载最新的代码，也可以直接下载压缩包解压后将目录放在redmine/public/themes目录下
git clone https://github.com/mrliptontea/PurpleMine2.git public/themes
```
登陆 Rdemine 进入 管理 > 配置 > 显示 > 主题 中选择「PurpleMine2」即可

### 安装插件

- 通过 [官网](https://www.redmine.org/plugins?page=1&sort=rating) 或其他途径获取插件信息，注意查看每个插件的版本兼容信息
- 将插件文件夹拷贝到 redmine/plugins 目录下或通过 `git clone { 插件源代码地址 } plugins/{ 插件名称 }` 直接下载最新的插件
- 执行以下命令安装插件，部分特殊插件安装会在插件介绍中说明
  
```shell
cd /u01/server/redmine
# 安装插件所需依赖
bundle install --without development test --no-deployment
# 执行插件数据库迁移脚本
bundle exec rake redmine:plugins:migrate RAILS_ENV=production
```

- 插件安装完成后必须重启 Redmine 服务

```shell
bundle exec rails server webrick -e production -b 0.0.0.0 -p 80
```

- 删除插件

```shell
# 还原插件数据库迁移脚本
bundle exec rake redmine:plugins:migrate NAME={插件名称} VERSION=0 RAILS_ENV=production
# 删除插件目录
rm -rf plugins/{插件名称}
```

### 插件推荐

- easy_gantt 甘特图

```shell
# 还需要单独执行以下命令
gem install redmine_extensions
rake db:migrate RAILS_ENV=production
```

- easy_mindmup/easy_wbs 项目管理工作包并通过思维导图的方式展现
- redmine_checklists 任务明细可添加checklist
- redmine_contacts 可维护项目关系人
- redmine_custom_workflows 自定义工作流
- redmine_dashboard 敏捷看板
- redmine_dmsf 上传附件文件管理可在并能在任务描述中使用代码来快速生成文件连接和图片预览
- redmine_drawio 可以使用 Drawio 画流程图
- redmine_issues_tree 任务树状结构显示
- redmine_issue_templates 任务模版
- redmine_lightbox2 可直接预览图片不用跳转到新的页面
- redmine_mentions 可以直接@相关人员
- redmine_more_filters 更多筛选条件
- redmine_people 更详细的人员管理
- redmine_pivot_table 数据透视图
- redmine_products 产品和订单管理
- redmine_questions Q&A功能
- redmine_revision_branches 更详细的版本管理信息
- redmineup_tags 可维护标签 `和redmine_issues_tree插件有冲突`
- redmine_serial_number_field 自定义属性的字段生成规则可定制
- redmine_wiki_extensions wiki扩展可以进行评论和其他一些扩展功能
- redmine_datetime_custom_field 自定义字段增加了时间类型
- 

## To Do List

1. 配置 Nginx
2. LDAP 服务配置
3. 插件详细介绍
4. 与 Git 代码库集成
