## 常用技术
+ Spring Bean的声明周期
+ Spring 事务 @Transactional注解
+ Spring面向切面编程AOP


## Java语言与虚拟机学习
+ [【javase specs】](https://docs.oracle.com/javase/specs/index.html)

## Gradle阿里云镜像仓库配置
```
# build.gradle
allprojects {
	repositories {
		maven { url "http://maven.aliyun.com/nexus/content/groups/public"}
		maven{ url "http://maven.aliyun.com/nexus/content/repositories/jcenter"}
	}
}
```
Gradle插件仓库配置
```
# settings.gradle
pluginManagement {
	repositories {
//		gradlePluginPortal()
		maven { url 'https://maven.aliyun.com/repository/gradle-plugin'}
		maven { url 'https://repo.spring.io/plugins-release' }
	}
}
```
