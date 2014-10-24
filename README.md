概述 Overview
==================

`jetbrick-template` 是一个新一代 Java 模板引擎，具有高性能和高扩展性。 适合于动态 HTML 页面输出或者代码生成，可替代 `JSP` 页面或者 `Velocity` 等模板。 指令和 `Velocity` 相似，表达式和 `Java` 保持一致，易学易用。

* 支持类似于 Velocity 的多种指令
* 支持模板热加载
* 支持强类型/弱类型切换
* 支持静态方法/字段
* 支持可变参数方法调用
* 支持方法重载
* 支持扩展方法
* 支持扩展函数
* 支持自定义标签 #tag
* 支持宏定义 #macro
* 支持布局 layout
* 支持安全管理器

文档 Documents
=================

http://subchen.github.io/jetbrick-template/


简单易用的指令
=================

`jetbrick-template` 指令集和老牌的模板引擎 `Velocity` 非常相似，易学易用。

```html
#define(List userlist)
<table>
  <tr>
    <td>序号</td>
    <td>姓名</td>
    <td>邮箱</td>
  </tr>
  #for (UserInfo user : userlist)
  <tr>
    <td>${for.index}</td>
    <td>${user.name}</td>
    <td>${user.email}</td>
  </tr>
  #end
</table>
```

基本开发 API 
=================

```java
public class JetxTest {

    @Test
    public void test() {
        // 0. 准备一些 Model 数据作为测试
        List<User> users = Arrays.asList(
            new User("张三", "zhangsan@qq.com"),
            new User("李四", "lisi@qq.com"),
            new User("王五", "wangwu@qq.com"),
        );

        // 1. 创建一个默认的 JetEngine
        JetEngine engine = JetEngine.create();

        // 2. 获取一个模板对象 (从默认的 classpath 下面)
        JetTemplate template = engine.getTemplate("/users.jetx");

        // 3. 创建 context 对象
        Map<String, Object> context = new HashMap<String, Object>();
        context.put("users", users);

        // 4. 渲染模板到自定义的 Writer
        StringWriter writer = new StringWriter();
        template.render(context, writer);

        // 5. 打印结果
        System.out.println(writer.toString());
    }
}
```

Maven 依赖 pom.xml
=============================

Release 版本已发布到 Maven 中央库： http://central.maven.org/maven2/com/github/subchen/

```xml
<dependency>
    <groupId>com.github.subchen</groupId>
    <artifactId>jetbrick-template-core</artifactId>
    <version>2.0</version>
</dependency>
```

开源许可 License
===================

```
Copyright 2013-2014 Guoqiang Chen, Shanghai, China. All rights reserved.

  Author: Guoqiang Chen
   Email: subchen@gmail.com
  WebURL: https://github.com/subchen

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
