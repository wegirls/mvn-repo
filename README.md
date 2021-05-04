# github maven仓库

一、上传源码到仓库

1.进入github设置界面,设置名称

2.生成token

3.在本地maven的setting.xml文件添加以下属性

```xml
<server>
   <id>github</id>
   <username>github用户名</username>
   <password>此处填写上面生成的token</password>
</server>
```
4.单项目源码配置文件看[dm](https://github.com/wegirls/dm/blob/master/pom.xml "dm")  父子模块源码配置看[handy-starer](https://github.com/wegirls/handy-starter/blob/main/pom.xml "handy-starer")

5.源码上传github

> 执行 mvn clean deploy上传到github

二、仓库使用

1.pom.xml配置文件添加以下属性(以我自己的仓库为例)

```xml
<repositories>
	<repository>
		<id>mvn-repo</id>
		<url>https://raw.githubusercontent.com/wegirls/mvn-repo/master</url>
		<snapshots>
		<enabled>true</enabled>
		<updatePolicy>always</updatePolicy>
	   </snapshots>
	</repository>
</repositories>

<dependencies>
	<dependency>
		<groupId>com.wegirls</groupId>
		<artifactId>dm</artifactId>
		<version>1.0.0</version>
	</dependency>
</dependencies>
```
2.由于各种原因,raw.githubusercontent.com经常无法下载文件导致依赖无法正常下载

3.为了稳定性我把github的maven仓库同步到gitee,然后再通过gitee拉取maven依赖

4.通过gitee添加maven依赖的方式如下：

```xml
<repositories>
	<repository>
		<id>mvn-repo</id>
		<url>https://gitee.com/wegirl/mvn-repo/raw/master</url>
	</repository>
</repositories>

<dependencies>
	<dependency>
		<groupId>com.wegirl</groupId>
		<artifactId>dm</artifactId>
		<version>1.0.0</version>
	</dependency>
</dependencies>
```
5.通过这样方式能正常下载依赖,但是每次mvn clean deploy的时候都需要在gitee仓库进行源码同步操作

三、存在的问题

1.如果maven配置文件配置了阿里云等等镜像,会导致该仓库无法正常下载。

2.暂时没时间研究这个问题

3.解决方法是maven配置文件先把阿里云镜像配置注销再使用
