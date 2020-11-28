# JSp+Servlet

## jsp基础语法

1.  注释

   1. HTML注释:/<!--注释-->
   2. jsp注释:<%--注释--%>
   3. Java代码注释

2. 声明:<%! 变量定义/方法定义/类%>

3. jps表达式:<%=变量或表达式%>

4. jsp指令

   4.1 page指令 <%@page attribute="value"...%>

   4.2 include指令<%@include file="URL"%>

   ​	作用：是在标签插入的位置插入静态的文件内容

   ​	好处：页面代码复用、结构清晰易于维护

   4.3 taglib指令<%@taglib uri="" prefix%>

   ​	用来自定义新的标签

5. jsp动作13个

## Front 设计模式

__DispatchServlet__

## SpringMVC

1. SpringMVC重要组件
   1. dispatchServlet前端控制器，接受所有请求
   2. HandlerMapping解析请求格式，判断期望要执行哪个具体方法
   3. HanderAdapter负责调用具体方法
   4. ViewResovler视图解析器

```java
public static void main(String[] args){
    
}
```

### 拦截器



拦截器：拦截请求，针对的是_控制器_方法

AOP拦截的是在特定方法前后