解压：tar -zxvf mysql-5.6.36-linux-glibc2.5-x86_64.tar.gz 

挪动位置： mv mysql-5.6.36-linux-glibc2.5-x86_64 /usr/local/mysql 

创建MySQL用户： useradd -s /sbin/nologin mysql 

创建MySQL数据库文件存放目录/data/mysql并更改权限：

 mkdir -p /data/mysql;chown -R mysql:mysql /data/mysql; 

进入/usr/local/mysql目录，初始化： ./scripts/mysql_install_db --user=mysql --datadir=/data/mysql 

这期间遇到错误该安装就安装，比如perlyum install -y perl-Module-Install和 yum install -y libaio，

不然会报错复制配置文件： cp support-files/my-default.cnf /etc/my.cnf 

修改配置文件：vim /etc/my.cnf basedir = /usr/local/mysql datadir = /data/mysql port = 3306 

复制启动脚本，并修改其属性 cp support-files/mysql.server /etc/init.d/mysqld chmod 755 /etc/init.d/mysqld 修改启动脚本：vim /etc/init.d/mysqld basedir= datadir=/data/mysql 

接下来就是启动和检查了把mysqld服务加入系统服务列表chkconfig --add mysqld 开机启动 chkconfig mysqld on 启动服务 service mysqld start 最后是把msyql加入环境变量打开文件vim /etc/profile 最后面加上export PATH=/usr/local/mysql/bin:$PATH 保存好后source /etc/profile 可以运行MySQL啦