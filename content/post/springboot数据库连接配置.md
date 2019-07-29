---
title: "Springboot数据库连接配置"
date: 2019-07-29T16:00:47+08:00
draft: false
categories: ["springboot"]
tags: ["spring","数据库"]
---

## SpringBoot数据库连接

spring boot 的数据库连接写在配置文件中，1.x与2.x略有不同

## application.yml 配置

```yml
spring:
    datasource:
        dbname:
            driver-class-name: "com.mysql.cj.jdbc.Driver"  
            jdbc-url: "jdbc:mysql://localhost:3306/dbname"
            username: "root"
            password: "password"
```

以上配置为 spring 2.1.6,对于spring 2.0以下的配置有以下修改

```yml
spring:
    datasource:
        dbname: 
            driver-class-name: "com.mysql.jdbc.Driver"
            url: "jdbc:mysql://localhost:3306/dbname"
            username: "root"
            password: "password"

```

1.x和2.x的变化主要有驱动名字和url

## 数据库配置 JdbcTemplate

```java
@Configuration
public class DatabaseConfig {
    @Bean(name = "dbname")
    @Qualifier("dbname")
    @Primary
    @ConfigurationProperties(prefix = "spring.datasource.dbanem")
    public DataSource dbname() {
        return DataSourceBuilder.create().build();
    }

    @Bean(name = "dbnameTemplate")
    public static JdbcTemplate dbnameTemplate(@Qualifier("dbname") DataSource dataSource) {
        return new JdbcTemplate(dataSource);
    }
}
```

## 数据库使用 Controller

```java
@Component
@RestController
@RequestMapping(value = "api/")
public class TestController {
    
    @Autowired
    @Qualifier("dbnameTemplate")
    protected JdbcTemplate dbname;

    //编写sql语句
    String sql = "select * from user;";

    //执行查询，并写入map对象
    Map<String, Object> datamap = dbname.queryForMap(sql);

}

```

> 最动人时光，未必地老天荒。



