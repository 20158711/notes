# 核心领域概念

- 认证 (authentication)

	建立主体(principal)的过程
	
- 授权 (authorization)

	或称（访问控制[access-control]



```
xmlns:sec="http://www.thymeleaf.org/thymeleaf-extras-springsecurity4
thymeleaf中的springsecurity命名空间
```

# Springboot集成springSecurity

	compile('org.springframework.boot:spring-boot-starter-security')
	compile('org.thymeleaf.extras:thymeleaf-extras-springsecurity4:3.0.2.RELEASE')

example
```
package com.example.demo.config;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

/**
 * 安全配置类
 */
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Autowired
    public void configureGlobal(AuthenticationManagerBuilder auth) throws Exception {
        auth.inMemoryAuthentication()//认证信息存储在内存中
        .withUser("yanbing1025").password("123456").roles("ADMIN");
    }

    /**
     * 自定义配置
     * @param http
     * @throws Exception
     */
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
                .antMatchers("/css/**","/js/**","/index").permitAll()//都可以访问
                .antMatchers("/users/**").hasRole("ADMIN")//需要相应角色才能访问
                .and()
                .formLogin()//基于Form表单登录验证
                .loginPage("/login").failureUrl("/login-error");//自定义登录界面
    }

}
```

# sec:authorize="isAuthenticated()"不解析	

```
检查命名空间版本：
	xmlns:sec="http://www.thymeleaf.org/thymeleaf-extras-springsecurity4"
检查依赖版本
	<dependency>
            <groupId>org.thymeleaf.extras</groupId>
            <artifactId>thymeleaf-extras-springsecurity4</artifactId>
            <version>3.0.2.RELEASE</version>
    </dependency>
二者一致才生效
```