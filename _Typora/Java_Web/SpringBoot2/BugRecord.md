# Bug记录



## maven错误

### Failed to execute goal org.apache.maven.plugins:maven-surefire-plugin:2.22.2

pom.xml中加入以下代码

```xml


<build>
    <plugins>

        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>2.22.2</version>
            <configuration>
                <skipTests>true</skipTests>
            </configuration>
        </plugin>
    </plugins>

</build>

</project>

```





## 资源路径错误

### SpringBoot整合jsp的时候访问不到静态资源

springboot 默认的静态资源的值有四个：

- *classpath:/META-INF/resources/*
- *classpath:/resources/*
- *classpath:/static/*
- *classpath:/public/*

如果你没有特别配置静态资源的位置，那么默认的静态资源的位置就是resource 下面的static文件夹，毕竟不用自己新建文件夹

那么你的页面引入的静态文件可以这么写：

` <script type="text/javascript" src="/js/jquery.min.js"></script> `

这样就需要在static下面创建js文件夹，将jqeruy.js放在这个js文件夹下面

![image-20210523141031182](R:\GITHUB\MyNotes\_Typora\Java_Web\SpringBoot2\BugRecord.imgs\image-20210523141031182.png)



## 整合pagehelper的时候查询查询了所有的数据，而不是进行了分页

在SSM中整合pagehelper只需要导入一个依赖，但是Springboot中需要导入三个依赖

```xml
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper</artifactId>
    <version>5.1.4</version>
</dependency>
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper-spring-boot-starter</artifactId>
    <version>1.2.5</version>
</dependency>
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper-spring-boot-autoconfigure</artifactId>
    <version>1.2.5</version>
</dependency>
```

导入这三个插件就可以了



