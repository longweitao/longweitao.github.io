#### 从无到有搭建一个属于自己Android 框架

#### 从零开始 ，搭建一个 ·`Kotlin` +` MVP`  + `模块化`   的项目 



##### 首先 ，整个项目使用` Kotlin` 进行开发  ，在创建项目时 ， 勾选  ` Include Kotlin support`

![create_project_mark](D:\BLOG\longweitao.github.io\images\myproject\create_project_mark.png)



##### 既然是模块化开发 ，自然少不了模块的分割 。

> File --> New --> New Module --> Android Library (建议选择这个) --> Finish

![create_module](D:\BLOG\longweitao.github.io\images\myproject\create_module.jpg)



##### 在根目录下，查看项目的module 。也可以在setting.gradle 文件下，进行module的删除操作 。

![setting.gradle](D:\BLOG\longweitao.github.io\images\myproject\setting.gradle.jpg)



##### 将模块依赖到主app  

> 右键项目  open Module Settings    -> app(Dependencies ) ->  

![dependencies](D:\BLOG\longweitao.github.io\images\myproject\dependencies.jpg)



当我们成功依赖完Module ，会在app 模块下builde.gradle 文件中 , 找到project 的依赖 。

```groovy
dependencies {
    implementation fileTree(include: ['*.jar'], dir: 'libs')
    implementation project(':base_utils')      //  base module 的依赖
}

```



既然我们有了base Module 。那是不是我们的一些必要的依赖， 都可以放到base_utils 中进行统一管理 。。。

如下 ：   以下是 base_utils中的依赖库 。

```groovy
dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    api "org.jetbrains.kotlin:kotlin-stdlib-jdk7:$kotlin_version"
    api "org.jetbrains.kotlinx:kotlinx-coroutines-android:$kotlin_coroutines"
    api "com.android.support:appcompat-v7:$android_support"
    api "com.android.support:recyclerview-v7:$android_support"
    api "com.android.support:cardview-v7:$android_support"
    api "com.android.support:design:$android_support"
    api 'com.android.support.constraint:constraint-layout:1.1.3'
    api 'com.github.bumptech.glide:glide:4.7.1'
    api 'org.greenrobot:eventbus:3.1.1'
}

```

 需要注意  ，base中  依赖的前缀为  `api` 而在app Module下 ， 依赖的前缀为 `implementation`   

二者区别为 ：

> implementation  : 只能在当前模块内使用     
>
> api :  其他模块依赖于此模块时，此模块使用api声明的依赖包是可以被其他模块使用



下一步 ，我的操作是  ，定义全局的版本号，以便对依赖库进行统一管理 ，防止后面项目中更新版本遗漏 ，出现jar包冲突现象。

在项目跟目录下 ，build.gradle 文件中 

```groovy
// Top-level build file where you can add configuration options common to all sub-projects/modules.

buildscript {
	// 定义全局版本号 ， 使用方法见 上面 dependencies 
    ext.kotlin_version = '1.3.10'
    ext.compile_sdk = 28
    ext.build_tools = '28.0.3'
    ext.min_sdk = 21
    ext.target_sdk = compile_sdk
    ext.android_support = '28.0.0'
    ext.kotlin_coroutines = '0.30.2'
    ext.kotlin_serialization = "0.6.2"

    repositories {
        google()
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.2.1'
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        google()
        mavenCentral()
        jcenter()
        // 添加远程仓库 
        maven { url 'https://jitpack.io' }
        maven { url "https://kotlin.bintray.com/kotlinx" }
    }
}

task clean(type: Delete) {
    delete rootProject.buildDir
}

```







