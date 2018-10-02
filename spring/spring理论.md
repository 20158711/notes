## 控制反转：

```
IOC Inversion of Control

	传统：程序主动去创建依赖对象
	IOC: IOC容器控制对象的创建

Spring实现控制反转的方式：
	
	属性注入	（spring xml 调用set方法 注入属性）
	构造器注入	(spring xml 调用constructor方法 注入)
	自动装配	 (
		@Component,@Repository,@Service,@Controller
		//@Required：该依赖关系必须装配（手动或自动装配），否则将抛出BeanInitializationException异常。
		//@Autowired：自动装配，默认按类型进行自动装配。
		//@Qualifier：如果按类型自动装配时有不止一个匹配的类型，那么可以使用该注解指定名字来消除歧义。
        )
```

## spring的优点

* 轻量
* 方便地整合其它框架
* 依赖关系十分明朗（DI)