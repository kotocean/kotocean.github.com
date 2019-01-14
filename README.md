# kotocean.github.io
知识的海洋的博客园

## centos7 安装jenkins

## java8
安装之前先检查一下系统有没有自带open-jdk
```
rpm -qa |grep java
rpm -qa |grep jdk
rpm -qa |grep gcj
```

如果没有输入信息表示没有安装。

如果安装可以使用`rpm -qa | grep java | xargs rpm -e --nodeps` 批量卸载所有带有Java的文件  这句命令的关键字是java

首先检索包含java的列表
`yum list java* `
检索1.8的列表
`yum list java-1.8*`

安装1.8.0的所有文件
`yum install java-1.8.0-openjdk* -y`

使用命令检查是否安装成功
`java -version`

### jenkins
// 安装最新版本的Jenkins
```
sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
sudo rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
sudo yum install jenkins
```

更改默认端口8080
编辑文件`/etc/sysconfig/jenkins`　　　　//该文件由rpm包jenkins生成
```
sudo service jenkins start | stop | restart
sudo chkconfig jenkins on
```

在浏览器输入http://IP:8081　　　　//正常跳出如下界面

首次进入会要求输入初始密码, 
初始密码在:/var/lib/jenkins/secrets/initialAdminPassword
