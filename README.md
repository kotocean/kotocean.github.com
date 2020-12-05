# kotocean.github.io
知识的海洋的博客园

## 目录索引
1. [【云IDE】](cloud.ide/README.md)

## GitHub缓存加速网站，为开发者服务
GitClone - https://gitclone.com/
一般使用说明：
1. 使用站内搜索，直接查询
2. 搜索没有结果，以surveyJS为例，github的克隆地址为：https://github.com/surveyjs/survey-library.git
实际克隆时，使用gitclone的加速克隆，地址为 https://gitclone.com/github.com/surveyjs/survey-library.git
也就是去掉原来的https://，替换为gitclone的网址即可。

### 其他加速
+ go get
+ stackoverflow

## centos7 安装jenkins

## java8
安装之前先检查一下系统有没有自带open-jdk
```
rpm -qa |grep java
rpm -qa |grep jdk
rpm -qa |grep gcj
```

如果没有输入信息表示没有安装。

如果安装可以使用`rpm -qa | grep java | xargs rpm -e --nodeps` 批量卸载所有带有Java的文件  这句命令的关键字是java。

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

Jenkins的默认安装路径是`/var/lib/jenkins`。所有的job相关的文件，都在`workspace/`目录下。

### jenkins用户加入docker用户组
把当前用户加入docker用户组
`$sudo gpasswd -a ${USER} docker`

另外，如果当前没有docker用户组，添加：
```
sudo vim /etc/group
    docker:x:580:docker
    dockerroot:x:509:
```
查看是否添加成功：
`cat /etc/group | grep ^docker`
重启docker
`sudo systemctl restart docker`

### 修改git提交时的可执行权限
git update-index --chmod +x mvnw
git ls-files --stage
修改完成后，由100644到100755，然后提交即可。否则提交上去的文件，在Jenkins构建时没有可执行权限。

### maven设置
[设置镜像源](http://maven.apache.org/guides/mini/guide-mirror-settings.html)
```
<settings>
  ...
  <mirrors>
    <mirror>
      <id>UK</id>
      <name>UK Central</name>
      <url>http://uk.maven.org/maven2</url>
      <mirrorOf>central</mirrorOf>
    </mirror>
  </mirrors>
  ...
</settings>
```
设置maven bin的下载路径，[download.cgi](http://maven.apache.org/download.cgi)
选择想要的文件，右键复制链接，如 http://mirrors.hust.edu.cn/apache/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.zip
maven命令行的参数为，`mvnw -s settings.xml clean package -DskipTests`。

## Todo
+ 自动部署到目标机器上
