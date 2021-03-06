# 为了解决restful风格的访问路径问题，在web.xml文件中的中央调度器的url-pattern需要配置为/，解决静态资源无法访问的三种方法
1、解决web.xml中配置/拦截之后不能访问静态资源第一种方法，需要在web.xml中添加以下配置，表示访问时不拦截这些静态资源
```
<servlet-mapping>
    <servlet-name>default</servlet-name>
    <url-pattern>*.jpg</url-pattern>
</servlet-mapping>
<servlet-mapping>
    <servlet-name>default</servlet-name>
    <url-pattern>*.png</url-pattern>
</servlet-mapping>
<servlet-mapping>
    <servlet-name>default</servlet-name>
    <url-pattern>*.css</url-pattern>
</servlet-mapping>
<servlet-mapping>
    <servlet-name>default</servlet-name>
    <url-pattern>*.js</url-pattern>
</servlet-mapping>
```

2、解决web.xml中配置/拦截之后不能访问静态资源第二种方法，在springmvc.xml文件中添加
```
<mvc:default-servlet-handler/>
```
	
3、解决web.xml中配置/拦截之后不能访问静态资源的第三种方法，在springmvc.xml文件中添加
```
<mvc:resources location="/images/" mapping="/images/**"/>
<mvc:resources location="/js/" mapping="/js/**"/>
<mvc:resources location="/css/" mapping="/css/**"/>
```

# 前、后台相对路径和绝对路径（Servlet中的sendRedirect重定向除外）
## 1、前台路径
前台路径的参照路径是：当前web服务器的根，即http://127.0.0.1:8080
因为 绝对路径 = 参照路径 + 相对路径，所以当前超链接所提交的请求绝对路径是：
http://localhost:8080/welcome
<a href="/welcome.html">跳转到欢迎页面</a>

## 2、后台路径
后台路径的参照路径是：web应用的根路径。
当前web应用的根路径是：http://localhost:8080/springmvc
也就是说，现在要求的绝对路径是：参照路径 + 相对路径
http://localhost:8080/springmvc/welcome.html

# 处理器映射器HandlerMapping
## 1、BeanNameUrlHandlerMapping（默认）
org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping
## 2、SimpleUrlHandlerMapping
org.springframework.web.servlet.handler.SimpleUrlHandlerMapping
在springmvc.xml中配置：
```
<!-- 注册处理器映射器 -->
<!-- 注册处理器映射器 -->
<!-- 注册处理器映射器 -->
<bean class="org.springframework.web.servlet.handler.SimpleUrlHandlerMapping">
	<!-- 
	<property name="mappings">
		<props>
			<prop key="/welcome.html">myController</prop>
			<prop key="/test.html">myController</prop>
		</props>
	</property>
	 -->
	<property name="urlMap">
		<map>
			<entry key="/welcome.html" value-ref="myController" />
			<entry key="/test.html" value-ref="myController" />
		</map>
	</property>
</bean>
```
# 处理器适配器HandlerAdapter
## 1、SimpleControllerHandlerAdapter


## 2、HttpRequestHandlerAdapter


# 处理器
## 1、继承自AbstractController类


## 2、继承自MultiActionController类


# 视图解析器

<!-- 注册视图解析器(视图解析器按照定义顺序选择执行，或者可以设置order属性，大于0的数字) -->
<!-- 1、内部资源视图解析器InternalResourceViewResolver -->
```
<!-- 
<bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
	<property name="prefix" value="/WEB-INF/jsp/"></property>
	<property name="suffix" value=".jsp"></property>
</bean>
 -->
```

<!-- 2、BeanName资源视图解析器BeanNameViewResolver -->
```
<!-- <bean id="" class="org.springframework.web.servlet.view.BeanNameViewResolver"/> -->
```
<!-- 定义一个内部资源视图 -->
```
<!-- 
<bean id="internalResource" class="org.springframework.web.servlet.view.JstlView">
	<property name="url" value="/WEB-INF/jsp/welcome.jsp"/>
</bean>
 -->
```
<!-- 定义一个外部资源视图 -->
```
<!-- 
<bean id="taobao" class="org.springframework.web.servlet.view.RedirectView">
	<property name="url" value="http://www.taobao.com"/>
</bean>
 -->
```

<!-- 3、Xml资源视图解析器XmlViewResolver -->
```
<!-- 
<bean class="org.springframework.web.servlet.view.XmlViewResolver">
	<property name="location" value="classpath:myViews.xml"/>
</bean>
 -->
```

<!-- 4、Properties资源视图解析器ResourceBundleViewResolver -->
```
<!-- 
<bean class="org.springframework.web.servlet.view.ResourceBundleViewResolver">
	<property name="basename" value="myViews"/>
</bean>
 -->
```



