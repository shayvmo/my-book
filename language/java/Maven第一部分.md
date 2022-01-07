## Maven

2020年12月16日



[官网](https://maven.apache.org/)

[参考教程](http://www.imooc.com/wiki/mavenlesson/mavenintroduction.html)



### Maven 安装与配置



1、Windows

首先在 Maven 官网上，找到[下载地址](http://maven.apache.org/download.cgi)，并下载该版本[apache-maven-3.6.3-bin.zip](https://downloads.apache.org/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.zip)

配置 MAVEN_HOME



2、Maven配置

- 修改本地仓库地址

  - 在 Maven 的使用过程中，会自动将项目依赖的 jar 包从中央仓库下载到本地仓库，默认本地仓库路径是`${user.home}/.m2/repository`，这样的话，会占用较多的 C 盘空间，因此，我们可以自定义该路径

  - 进入 maven 路径的 conf 目录， setting.xml

  - ```xml
    <localRepository>D:\javaspace\repo</localRepository>
    ```

- 修改镜像位置

  - ```xml
    <mirrors>
        <!-- mirror
         | Specifies a repository mirror site to use instead of a given repository. The repository that
         | this mirror serves has an ID that matches the mirrorOf element of this mirror. IDs are used
         | for inheritance and direct lookup purposes, and must be unique across the set of mirrors.
         |
        <mirror>
          <id>mirrorId</id>
          <mirrorOf>repositoryId</mirrorOf>
          <name>Human Readable Name for this Mirror.</name>
          <url>http://my.repository.com/repo/path</url>
        </mirror>
         -->
    	<mirror>
    		<id>alimaven</id>
    		<name>aliyun maven</name>
    		<url>http://maven.aliyun.com/nexus/content/groups/public/</url>
    		<mirrorOf>central</mirrorOf>
    	</mirror>
      </mirrors>
    
    ```

    

#### 使用maven 创建项目

在 cmd 中切换到我们存放代码的目录，并执行命令：

```shell
mvn archetype:generate -DgroupId=com.mic.tech -DartifactId=firstProject -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

参数说明：

- **-DgourpId**: 组织名，一般为公司网址的反写；
- **-DartifactId**: 项目名-模块名；
- **-DarchetypeArtifactId**: 用来指定 ArchetypeId，这里用到的是maven-archetype-quickstart，即创建一个简单 Java 应用；
- **-DinteractiveMode**: 是否使用交互模式



### Maven POM 模型

> POM（项目对象模型）是 Maven 最基本，也是非常重要的一个概念。通常情况下，我们可以看到 POM 的表现形式是 pom.xml，在这个 XML 文件中定义着关于我们工程的方方面面，当我们想要通过 Maven 命令来进行操作的时候，例如：编译，打包等等，Maven 都会从 pom.xml 文件中来读取工程相关的信息。



#### Maven 的坐标

- **groupId**：groupId 为我们组织的逆向域名，这里的组织可以是公司，团体，小组等等。例如Apache 基金会的项目都是以 org.apache 来作为 groupId 的；
- **artifactId**：该组织下，项目的唯一标识；
- **packaging**：项目类型，描述的是项目在打包之后的输出结果，常见的 jar 类型的输出结果是一个jar 包，war 类型则输入 war 包，一般 Web 项目的打包方式为 war。
- **version**：项目的版本号，用来标记本项目的某一特定版本。SNAPSHOT 则是用来标记项目过程中的快照版本，该版本类型表明本项目不是稳定版本，常见的还有 RELEASE，则表示该版本为本项目的稳定版本



#### 超级 POM





### 生命周期

- clean
- default
- site



#### clean

clean 生命周期包括：

1. **pre-clean**： 清理前的准备工作；
2. **clean**：清理上一次构建的结果；
3. **post-clean**： 清理结束后需要完成的工作



#### default

1. **validate**：验证阶段。验证项目构建过程中需要的信息的正确性；
2. **compil**：编译阶段；
3. **test**：测试阶段。使用测试框架对项目进行测试，打包过程中，非必要阶段，可以跳过执行。
4. **package**：打包阶段。将编译好的文件打包成 jar 包，war 包或者 ear 包；
5. **verify**：检查阶段。检查打包结果的有效性；
6. **install**：本地部署阶段。将包部署到本地仓库，可以提供给本地开发过程中其他项目使用；
7. **deploy**：远程仓库部署阶段。将最终的包复制到远程仓库，提供给使用该仓库的其他开发者使用



#### site

1. **pre-site**：准备阶段。在生成站点前所需要做的工作；
2. **site**：生成站点阶段；
3. **post-site**：结束阶段。生成站点结束后所需要做的工作；
4. **site-deploy**：发布阶段。我们可以将上面生成的站点发布到对应服务器中



