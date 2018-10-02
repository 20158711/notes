# jpa

实现：EclipseLink  Hibernate  Apache OpenJPA

实体：

	关系数据库中的表
	每个实例对应于表中的行
	类必须用javax.persistence.Entity注解
	必须有无参构造函数
	实体实例被当作分离对象进行传递，则必须实现Serializable接口
	必须要有对象标识符：
		简单主键（javax.persistence.Id)
		复合主键（javax.persistence.EmbeddedId和javax.persistence.IdClass）

关系：

	一对一 @OneToOne
	一对多 @OneToMany
	多对一 @ManyToOne
	多对多 @ManyToMany

EntityManager接口

	1, 定义用于与持久性上下文进行交互的方法
	2, 创建和删除持久实体实例，通过实体的主键查找实体
	3, 允许在实体上运行查询

Spring Data JPA

	CurdRepository
	PagingAndSortingRepository0

Spring Data JPA、Hibernate、Spring boot集成

	compile('org.springframework.boot:spring-boot-starter-data-jpa')
	runtime('mysql:mysql-connector-java')
	
	  datasource:
	    url: jdbc:mysql://localhost/blog?useSSL=false&serverTimezone=UTC&characterEncoding=utf-8
	    username: root
	    password: root
	    driver-class-name: com.mysql.jdbc.Driver
	
	  jpa:
	    show-sql: true
	    hibernate:
	      ddl-auto: create-drop
	      
	 create database blog default charset utf8 collate utf8_general_ci;
	 
	 @Entity
	 @Id
	 @GeneratedValue(strategy = GenerationType.IDENTITY)//自增

# ManyToMany

	@ManyToMany(fetch = FetchType.EAGER)
	@JoinTable(
	        name = "sys_role_user",
	        joinColumns = {@JoinColumn(name = "sys_user_id",referencedColumnName = "id")},
	        inverseJoinColumns = {@JoinColumn(name = "sys_role_id",referencedColumnName = "id")}
	)
	List<SysRole> roles;
	
	create table sys_role_user
	(id bigint unsigned auto_increment primary key,
	  sys_user_id bigint unsigned not null,
	  sys_role_id bigint unsigned not null
	)
	
	注意：
		在SysRole.java中就不要用mapby... ,不然会产生死循环，导致栈溢出错误
		若出现懒加载错误，可添加(fetch=FetchType.EAGER)来解决

# 强制使用INnodb

​	

	spring.jpa.database-platform: org.hibernate.dialect.MySQL5InnoDBDialect


# 类上的注解

	@Table(name="table_name")	//定义表名


# 属性上的注解

	@Column(length=20,nullable=false,name="column_name")
	@Temporal(TemporalType.DATE)	  //用在Date类型属性上
	@Lob							//大文本类型
	@Transient						//不持久化，表中没有该字段
	@Basic(fetch=FecthType.LAZY)	  //懒加载

# 关系的概念

	关系维护端负责外键或关系表的更新
	关系被维护端没有权力更新外键记录
	关联表一般定义在关系维护端（@JoinTable)
	双向一对多和多对一
	mappedBy=""
	1，1-m 多的一方 为关系的 维护端，
		@OneToMany(
			cascade={CascadeType.ALL},
			fetch = FetchType.EAGER,
			mappedBy = "order"		//指明由OrderItem中order属性维护关系
			)
		//ToMany默认懒加载
		private Set<OrderItem> itemSet=new HashSet<>();
		
	2，m-1
		@ManyToOne(
			cascade = {CascadeType.MERGE,CascadeType.REFRESH},	//不能要级联删除
	    	optional = true)								 //为true表示可以为空
	    @JoinColumn(name = "order_id")							//指定外键
	    private Order order;
	    
	双向多对多


​	

# 自定义的 JPQL （批量删除，更新）

```java
public interface NewsDao extends JpaRepository<News,Long> {
    Page<News> findNewsByNewsTitleLike(String title, Pageable pageable);
    @Transactional @Modifying
    @Query("delete from News n where n.id in (:ids)")
    int deleteByIds(@Param("ids")List<Long> list);
}
	可以自定义
	
@Modifying @Query("update Person set email = :email where lastName =:lastName")
void updatePersonEmailByLastName(@Param("lastName")String lastName,@Param("email")String email);
```

# 联合主键

	@Embeddable 标识主键类，且实现序列化


# 常见错误

	使用Lombok的Data注解，重写了hashCode方法导致的，不用Data就行了
	
	could not initialize proxy [org.yanbing1025.jpastudy.po.Order#999] - no Session
	spring.jpa.open-in-view: true，
	并且在调用的方法上 加上事物注解 @Tractional 即可

# 关于@DynamicInsert@DynamicUpdate无效

# @Column(columnDefinition)的用法



	创建数据库的时候要设置默认值或更新默认值才生效：
		create_time timestamp default current_timestamp '创建时间' NOT NULL
		update_time timestamp default current_timestamp on update current_timestamp comment '修改时间'
	注解方式
		@Column(columnDefinition="timestamp default current_timestamp comment '活动开始时间'")
		@Column(columnDefinition="timestamp default current_timestamp on update current_timestamp comment '修改时间'")
		
		或
		
		@org.hibernate.annotations.CreationTimestamp  // 由数据库自动创建时间
	    private Timestamp createTime;
	    
	    @Column(columnDefinition)用于自定义字段属性

# 更新时只更新非空字段的实现方法

	由于jpa不像Mybatis那样主要由自己写SQL语句，因此要实现此功能需要手动将数据库的的查询出来为old，再将用户传过来的new要修改的非空的属性复制到old中，再调用jpa中的dao.save()即可。

# 拷贝非空属性工具类	

	public class UpdateNotNullUtil {
	
	/**
	 *  将src中非空且同名的properties复制到dest中
	 *  BeanUtils.copyProperties方法定义如下
	 *  public static void copyProperties(Object source, Object target, String... ignoreProperties) throws BeansException {
	 *         copyProperties(source, target, null, ignoreProperties);
	 *  }
	 * @param src
	 * @param dest
	 */
	
	public static void copyNotNullProperties(Object src,Object dest){
	    BeanUtils.copyProperties(src, dest,getNullProperties(src));
	}
	
	/**
	 * 查找src中空的properties并返回
	 * @param src
	 * @return
	 */
	private static String[] getNullProperties(Object src){
	    BeanWrapper srcBean=new BeanWrapperImpl(src);
	    PropertyDescriptor[] descriptors = srcBean.getPropertyDescriptors();
	    Set<String> emptyName=new HashSet<>();
	    for (PropertyDescriptor descriptor : descriptors) {
	        Object value = srcBean.getPropertyValue(descriptor.getName());
	        if (value == null) {
	            emptyName.add(descriptor.getName());
	        }
	    }
	    String[] result=new String[emptyName.size()];
	    return emptyName.toArray(result);
	}
}

# 一对多处联接

    @Entity
    @Setter @Getter
    @DynamicInsert
    @DynamicUpdate
    public class Category {
        @Id @GeneratedValue(strategy = GenerationType.IDENTITY)
        @Column(length = 11)
        private Long id;
    
        @ManyToOne
        private Category parent;
    
        @OneToMany(mappedBy = "parent", cascade=CascadeType.REMOVE, fetch=FetchType.LAZY)
        private Set<Category> categories=new HashSet<>();
    
        @Column(length = 50)
        private String name;
    
        private Byte status=1;
    
        private Integer sortOrder;
    
        @Temporal(value = TemporalType.TIMESTAMP)
        @Column(columnDefinition = "timestamp default current_timestamp")
        private Date createTime;
    
        @Temporal(value = TemporalType.TIMESTAMP)
        @Column(columnDefinition = "timestamp default current_timestamp on update current_timestamp")
        private Date updateTime;
    }











