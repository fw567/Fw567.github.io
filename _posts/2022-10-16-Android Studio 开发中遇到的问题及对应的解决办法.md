**<br>Android Studio 开发中遇到的问题及解决办法</br>**
出现的问题：
Gradle sync failed: Could not find method dependencyResolutionManagement() for arguments [settings_85pb7rne0n0dcsfovjf5fgfbb$_run_closure1@70dbe55e] on settings 'HelloWorld' of type org.gradle.initialization.DefaultSettings. 

解决方法：
1.#首先在**Project Structure**中找到**Android gradle plungin version**将其改为**4.1.3**，gradle最低的版本限制为**6.5**，在此以下的版本都不可以。

2.更新gradle 文件：
将build.gradle中的内容替换为:

```
// Top-level build file where you can add configuration options common to all sub-projects/modules.
buildscript {
    repositories {
      maven { url 'http://maven.aliyun.com/nexus/content/repositories/google' }
      maven { url 'http://maven.aliyun.com/nexus/content/repositories/jcenter'}
        google()
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:4.1.3'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}
allprojects {
    repositories {
//        maven { url 'http://maven.aliyun.com/nexus/content/repositories/google' }
//        maven { url 'http://maven.aliyun.com/nexus/content/repositories/jcenter'}
        google()
        jcenter()
    }

    tasks.withType(Javadoc) { // 新增
        options.addStringOption('Xdoclint:none', '-quiet')
        options.addStringOption('encoding', 'UTF-8')
    }
}

task clean(type: Delete) {
    delete rootProject.buildDir
}
```

具体如下图：![](https://kjimg10.360buyimg.com/ott/jfs/t1/143277/37/29407/68677/63287bd9Ee4dd37ab/1dbaa815db530c24.png)

3.最后是将seeting.gradle大部分进行删除，只留下两个：
rootProject.name = "HelloWorld"
include ':app'

seeting.gradle处的设置：![](https://kjimg10.360buyimg.com/ott/jfs/t1/105104/2/31522/8388/63287c56E18b25efc/7839e426df1a66b5.png)
    
3.出现Could not resolve all dependencies for configuration ':classpath'.报错时，可以将工程级的gradle-wrapper.properties中的内容置换为

```
#Sun Oct 16 10:27:46 CST 2022
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
distributionUrl=https\://services.gradle.org/distributions/gradle-6.5.1-bin.zip
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
```

设置结果如下面所示：

![](https://m.360buyimg.com/babel/jfs/t1/184032/36/29384/32869/634b7361E88c43991/cd53d45a82c5c8e8.png)

