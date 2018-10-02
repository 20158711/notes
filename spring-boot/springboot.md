## IOC(控制反转)

## DI依赖注入

* 指容器负责创建对象和维护对象间的依赖关系，而不是通过对象本身负责自己的创建和解决自己的依赖关系

* 控制反转是通过依赖注入实现的

* 依赖注入目的是为了解耦，体现了一种“组合“的理念。（继承的子类会与父类耦合)

* Spring IoC容器（ApplicationContext）负责创建Bean。

## 声明Bean的注解

* @Component
* @Service
* @Repository
* @Controller
* @ComponentScan     自动扫描包名下所有使用＠Service，＠Component，＠Repository，＠Controller的类，并注册为Bean。
## 注入Bean的注解

* @Autowired:     Spring提供
   @Inject:		JSR-330
* @Resource:      JSR-250
* 可注解在set方法上或者属性

## 配置

* @Configuration	:声明当前类是一个配置类，里面可能有＠Bean
* ＠Bean                    :注解在方法上，声明当前方法的返回值是一个Bean

## ＠Value

```
@Value("I love you")
private String normal;
@Value("#{systemPropertiey['os.name']}")

```

