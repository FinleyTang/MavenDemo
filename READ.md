## 在 IntelliJ IDEA 中使用 Maven 工具构建 JAR 包的简单示例

### 1、创建 Maven 项目
在 IntelliJ IDEA 的欢迎界面中，选择 “Create New Project” -> “Maven”，然后根据向导创建一个新的 Maven 项目。

### 2、修改 pom.xml 文件
在项目中找到 pom.xml 文件，**添加**以下内容：
```xml
<build>
    <plugins>
        <!-- 在 jar 打包时使用 maven-assembly-plugin 插件 -->
        <plugin>
            <artifactId>maven-assembly-plugin</artifactId>
            <version>3.1.0</version>
            <configuration>
                <descriptorRefs>
                    <descriptorRef>jar-with-dependencies</descriptorRef>
                </descriptorRefs>
                <archive>
                    <manifest>
                        <mainClass>com.example.Main</mainClass>
                    </manifest>
                </archive>
            </configuration>
            <executions>
                <execution>
                    <id>make-assembly</id>
                    <phase>package</phase>
                    <goals>
                        <goal>single</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

上述代码配置了一个名为 maven-assembly-plugin 的 Maven 插件，用于将项目打包为一个包含依赖项的 JAR 文件。其中，mainClass 指定了项目的主类名。

### 3、编写代码
在 src/main/java 目录下创建 com.example.Main 类，并编写如下代码：


```java
package com.example;

public class Main {
public static void main(String[] args) {
System.out.println("Hello, world!");
}
}
```

### 4、打包 JAR 文件
在 IntelliJ IDEA 中，打开 Maven 项目工具窗口（View -> Tool Windows -> Maven Projects），然后双击 “package” 生命周期阶段，或者右键点击该阶段，选择 “Run Maven Build”。

这样，Maven 就会在 target 目录下生成名为 example-1.0-SNAPSHOT-jar-with-dependencies.jar 的 JAR 文件，其中包含了项目的编译输出以及所依赖的所有库。

可以通过以下命令行运行该 JAR 文件：

`java -jar example-1.0-SNAPSHOT-jar-with-dependencies.jar`
输出应该为：
`
Hello, world!`
这就是使用 IntelliJ IDEA 和 Maven 工具构建 JAR 包的一个简单示例。