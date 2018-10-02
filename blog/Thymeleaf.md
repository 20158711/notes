# Thymeleaf:
```
自然模板，所风即所得
```
方言1：

	<html xmlns:th="http://www.thymeleaf.org">
		<p th:text="#{home.welcome}">Welcome</p>

方言2：

	<span data-th-text="...">

变量表达式：

	<span th:text="${book.author.name}">

消息表达式（国际化）：

	<span th:text="#{header.address.city}">

选择表达式：

	<div th:object="${book}">
		<span th:text="*{title}"></span> 
		//取book里面的title,在当前选择的对象而不是整个上下文
	</div>

链接表达式：

	//相对路径，没有应用程序上下文
	<a th:href="@{../doc/rep}">...</a>
	
	//相对路径，没有应用程序上下文
	<a th:href="@{~/doc}">...</a>
	
	//和协议相对
	<a th:href="@//static.mycompany.com/res.initial}">...</a>
	
	//绝对地址
	<a th:href="@{http://www.bidu.com/main}">...</a>
	
	//相对于static
	<link th:fragment="css" th:href="@{/css/bootstrap.css}" rel="stylesheet"/>
	
	//相对于templates
	<div th:replace="~{fragment/header::header}"></div>

分段表达式：

	th:insert  	//插入片段
	th:replace  //替换片段
	th:include	//插入片段内容
	
	<!--定义片段-->
	<div th:fragment="copy">
		&copy; 2018
	</div>
	<div id="copy-section">
		&copy; 2018
	</div>
	
	<!--引用片段-->
	<div th:insert="~{footer::copy}</div>
	<div th:replace="~{footer::copy}</div>
	<!--通过id引用片段-->
	<div th:insert="~{footer::#copy-section}</div>


字面量：

	文本：
	<span th:text="hello">hello</span>
	<span th:text="2013+2">2015</span>
	
	bool
	<div th:if="${user.isAdmin()}==false">...
	
	null
	<div th:if="${variable.something}==null">...
	
	算术操作 + - * / %
	<div th:with="isEven=(${prodStat.count} % 2==0)">...
	
	比较运算 < ,> ,>=, <= ,== ，!=(gt ,lt ,ge ,le ,eq ,ne)
	<ul class="pagination" data-th-if="${page.totalPages le 7}:>
	
	条件运算
	<tr th:class="${row.even}? 'even' : 'odd' ">
	
	无操作占位
	<tr th:class="${row.even}? 'even' : '_' ">
	
	设置属性值
	<form action="login" th:attr="action=@{/login.action}">
		<input type="submit" value="val" th:attr="value=#{sub.submit}"/>
	</form>
	
	设置到指定属性值
	<form action="login" th:action="@{/login.action}">
		<input type="submit" value="val" th:value="#{sub.submit}"/>
	</form>
​	
迭代器
	
	<li th:each="book :${books}" th:text="${book.title}">En</li>
	迭代器状态变量
	index count size current even/odd first last
	<tr th:each="prod,iterStat:${prods}" th:class="${iterStat.odd}?'odd'>

条件语句

	th:if/th:unless/switch
	<a href="login" th:if="${not #lists.isEmpty (prod.comments)}">view</a>
	<a href="login" th:unless="${not #lists.isEmpty (prod.comments)}">view</a>
	<div th:switch="${user.role}">
		<p th:case="'admin'">User is admin</p>
		<p th:case="#{roles.manager}">User is manager</p>
		<p th:case="*">User is some other thing</p>
	</div>

注释
	
	//解析时删除
	<!--/*--> 
		<div>jfdsfja</div>
	<!--*/-->
	
	//原型被注释，解析时要显示
	<!--/*/
		<div>jfdsfja</div>
	/*/-->

内联
	
	[[]]或[()]分别对应于th:text和th:utext 转义与不转义
	<p>The message is "[(${msg})]"</p>	--> <p>The message is <b>great!</b></p>
	<p>The message is "[(${msg})]"</p>	--> <p>The message is &lt;b&gt;great!&lt;/b&gt;</p>
	
	//禁用内联表达示
	<p th:inline="none">A double array looks like this: [[1,2,3],[4,5]]!</p>
​	
基本对象
	
	#ctx 	上下言文对象
	${#ctx.request}	
	${#ctx.response}
	${#ctx.session}
	${#ctx.servletContext}
	
	//获取参数中的内容
	${param.foo}
	${param.size()}
	${param.isEmpty()}
	${param.containKey('foo')}
	
	//获取session中的内容
	${session.foo}
	${session.size()}
	${session.isEmpty()}
	${session.containKey('foo')}
	
	//获取application中的内容
	${application.foo}
	${application.size()}
	${application.isEmpty()}
	${application.containKey('foo')}
	
	//
	#request		javax.servlet.http.HttpServletRequest
	#session		javax.servlet.http.HttpSession
	#servletContext	javax.servlet.http.ServletContext

application.yml

	spring.thymeleaf.enconding=UTF-8
	spring.thymeleaf.cache=false
	spring.thymeleaf.mode=HTML5

​	
绑定数据到对象

	<form action="/users" method="POST" th:object="${user}">
	<input type="text" name="id" th:value="*{id}">
	<input type="text" name="name" th:value="*{name}">
	<input type="text" name="email" th:value="*{email}">
	public String save(Model model){
	    model.addAttribute("user",new User());
	    return "users/form";
	}
​	
实现包含整个头部，每个页面的标题可以自定义

header.html
---

	<!DOCTYPE html>
	<html lang="en"
	xmlns:th="http://www.thymeleaf.org">
	<head th:fragment="header(title)">
	<title th:replace="${title}">title</title>
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
	</head>
	<body>
	
	</body>
	</html>
index.html
---

	<!DOCTYPE html>
	<html lang="en"
	  xmlns:th="http://www.thymeleaf.org"
	  xmlns:sec="http://www.thymeleaf.org/thymeleaf-extras-springsecurity4">
	<head th:replace="~{fragment/header::header(~{::title})}">
	<title>我的主页</title>
	</head>
	<body>
	</body>
	</html>
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	
​	