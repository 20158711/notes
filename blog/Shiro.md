# 重要单词

	principal 		主角，主体
	credentials		证书
	authentication	认证，身份证明
	authorization	授权



# Shiro认证过程

	1, 创建SecurityManager
	2，主体提交认证
	3，SecurityManager认证
	4，Authentication认证
	5，Realm验证

# Shiro授权过程

	1, 创建SecurityManager
	2，主体授权
	3，SecurityManager认证
	4，Authorizer授权
	5，Realm获取角色权限数据

# Shiro中的Realm
	1, IniRealm
		user.ini文件
		[users]
	    yanbing1025=123456,admin
	    [roles]
	    admin=user:delete
	2, JdbcRealm
		
		//权限开关，默认为false
	     jdbcRealm.setPermissionsLookupEnabled(true);
	
		默认sql
	    String DEFAULT_AUTHENTICATION_QUERY = "select password from users where username = ?";
	    String DEFAULT_SALTED_AUTHENTICATION_QUERY = "select password, password_salt from users where username = ?";
	    String DEFAULT_USER_ROLES_QUERY = "select role_name from user_roles where username = ?";
	    String DEFAULT_PERMISSIONS_QUERY = "select permission from roles_permissions where role_name = ?";

# 自定义Realm

	继承AuthorizingRealm

# 自定义Filter

	继承AuthorizationFilter

# 内置过滤器

	anon
	authBasic
	authc
	user
	logout
	
	perms
	roles
	ssl
	port