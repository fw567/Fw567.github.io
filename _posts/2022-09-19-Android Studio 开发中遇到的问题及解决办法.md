Android Studio 开发中遇到的问题及解决办法
出现的问题：
Gradle sync failed: Could not find method dependencyResolutionManagement() for arguments [settings_85pb7rne0n0dcsfovjf5fgfbb$_run_closure1@70dbe55e] on settings 'HelloWorld' of type org.gradle.initialization.DefaultSettings. 

解决问题：
1.首先在project structure中找到Android gradle plungin version将其改为4.1.3，gradle最低的版本限制为6.5，以下的都不可以。

2.更新gradle 文件进行解决：
将build.gradle中的文字替换为:
// Top-level build file where you can add configuration options common to all sub-projects/modules.
buildscript {
    repositories {
        google()
        jcenter()
    }
    dependencies {
        classpath "com.android.tools.build:gradle:4.1.3"

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }

}

allprojects {
    repositories {
        google()
        jcenter()
    }
}

task clean(type: Delete) {
    delete rootProject.buildDir
}

具体如下图：![avator](https://kjimg10.360buyimg.com/ott/jfs/t1/143277/37/29407/68677/63287bd9Ee4dd37ab/1dbaa815db530c24.png)



3.最后是将seething.gradle大部分进行删除，只留下两个：
rootProject.name = "HelloWorld"
include ':app'

seeting.grade处的设置：![avator](https://kjimg10.360buyimg.com/ott/jfs/t1/105104/2/31522/8388/63287c56E18b25efc/7839e426df1a66b5.png)

