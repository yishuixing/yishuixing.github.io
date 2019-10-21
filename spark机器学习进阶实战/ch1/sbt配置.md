1. ~/.sbt/repositories
```
[repositories]
local
huaweicloud-maven: https://repo.huaweicloud.com/repository/maven/
maven-central: http://maven.aliyun.com/nexus/content/groups/public
sbt-plugin-repo: https://repo.scala-sbt.org/scalasbt/sbt-plugin-releases, [organization]/[module]/(scala_[scalaVersion]/)(sbt_[sbtVersion]/)[revision]/[type]s/[artifact](-[classifier]).[ext]
============选上面或下面==============
[repositories]
local:file:///D:/s/mvnRepo
aliyun: https://maven.aliyun.com/repository/central
central: http://repo1.maven.org/maven2
central-sbt: http://repo1.maven.org/maven2, [organization]/[module]/(scala_[scalaVersion]/)(sbt_[sbtVersion]/)[revision]/[type]s/[artifact](-[classifier]).[ext], bootOnly
sbt-plugins: https://dl.bintray.com/sbt/sbt-plugin-releases/, [organization]/[module]/(scala_[scalaVersion]/)(sbt_[sbtVersion]/)[revision]/[type]s/[artifact](-[classifier]).[ext], bootOnly
bintray-sbt-plugins: http://dl.bintray.com/coursera/sbt-plugins/, [organization]/[module]/(scala_[scalaVersion]/)(sbt_[sbtVersion]/)[revision]/[type]s/[artifact](-[classifier]).[ext], bootOnly
sonatype-oss-releases
```
2. 设置所有项目均使用全局仓库配置，忽略项目自身仓库配置
```

该参数可以通过 Java System Property 进行设置。在 SBT 中，有三种方法可以设置 Java System Property，可以根据需要自行选择。

方法一：修改SBT配置文件（推荐）

提醒一下，  sbt-1.3.0/conf/ 目录下有两个配置文件，  sbtconfig.txt 仅适用于  Windows 平台，而  sbtopts 仅适用于  Mac/Linux 平台。
针对 Windows 平台，打开 sbt-1.3.0/conf/sbtconfig.txt 文件，在末尾新增一行，内容如下：

-Dsbt.override.build.repos=true
针对 Mac/Linux 平台，打开 sbt-1.3.0/conf/sbtopts 文件，在末尾新增一行，内容如下：

-Dsbt.override.build.repos=true
方法二： 设置环境变量

在 Windows 上通过 set 命令进行设置，

set SBT_OPTS="-Dsbt.override.build.repos=true"
在 Mac/Linux 上使用 export 命令进行设置，

export SBT_OPTS="-Dsbt.override.build.repos=true"
方法三： 传入命令行参数

执行 sbt 命令时， 直接在命令后面加上配置参数，

sbt -Dsbt.override.build.repos=true
idea 中sbt加如下参数
-Dsbt.override.build.repos=true
-Dsbt.ivy.home=D:\s\ivyRepo
```
3 常用交互命令
```
sbtVersion
show overrideBuildResolvers
show fullResolvers
compile
run
package
clean	删除所有生成的文件 （在 target 目录下）。
compile	编译源文件（在 src/main/scala 和 src/main/java 目录下）。
test	编译和运行所有测试。
console	进入到一个包含所有编译的文件和所有依赖的 classpath 的 Scala 解析器。输入 :quit， Ctrl+D （Unix），或者 Ctrl+Z （Windows） 返回到 sbt。
run <参数>*	在和 sbt 所处的同一个虚拟机上执行项目的 main class。
package	将 src/main/resources 下的文件和 src/main/scala 以及 src/main/java 中编译出来的 class 文件打包成一个 jar 文件。
help <命令>	显示指定的命令的详细帮助信息。如果没有指定命令，会显示所有命令的简介。
reload	重新加载构建定义（build.sbt， project/*.scala， project/*.sbt 这些文件中定义的内容)。在修改了构建定义文件之后需要重新加载
```

启动配置：

 https://www.scala-sbt.org/1.x/docs/Launcher-Configuration.html 

4. 怎样从sbt工程转为eclipse工程(导入后一问题不少，放弃直接用idea)

   ```
   在工程目录下 project/plugins.sbt中加
   addSbtPlugin("com.typesafe.sbteclipse" % "sbteclipse-plugin" % "5.2.4")
   然后可以执行
   sbt eclipse
   最后就可以导入了
   另参考 https://www.lightbend.com/blog/integrating-sbt-and-eclipse
   ```

5. windows下错误：

   ```
   java.io.IOException: Could not locate executable null\bin\winutils.exe in the Hadoop binaries
   环境变量加 HADOOP_HOME="F:\\bd\\soft\\spark-2.4.4-bin-hadoop2.7"
   代码加下面，没起作用
   System.setProperty("HADOOP_HOME_DIR", "F:\\bd\\soft\\spark-2.4.4-bin-hadoop2.7")
   ```

说明：各个章节独立的sbt工程，没有父工程，sbt 多模块的比较麻烦，先不考虑，聚焦问题，别被干扰了