https://www.jianshu.com/p/13d18c631549

https://juejin.im/post/5c6eaa066fb9a049fc042048

1、新建 buildSrc

只留 src/main,其他文件及文件夹删除

build.gradle 内容删除

2、新建 src/main/groovy

src/main/resources/META-INF/gradle-plugins/plugin.properties

3、修改 build.gradle 内容
```
apply plugin: 'groovy'
dependencies {
    compile gradleApi()//在使用自定义插件时候，一定要引用org.gradle.api.Plugin
    compile 'com.android.tools.build:gradle:3.2.0'//使用自定义transform时候，需要引用com.android.build.api.transform.Transform
    compile 'org.ow2.asm:asm:6.0'
    compile 'commons-io:commons-io:2.6'
}
repositories {
    mavenCentral()
    jcenter()
    google()
}
```

注意 gradle 版本与主工程一致    

4、新建 groovy 与 java 文件      
新建自定义 plugin 
+ 集成 Transform 类，实现 Plugin 接口    
+ 重写最重要的一个方法 transform 方法    

自定义类 LifecycleClassVisitor 处理输入的 class 文件    
visitMethod 中调用 LifecycleOnCreateMethodVisitor 处理方法   

LifecycleOnCreateMethodVisitor 中   
visitCode 插入字节码   



5、引入插件
```text
apply plugin: com.example.asmdemo.LifecyclePlugin
```


        
