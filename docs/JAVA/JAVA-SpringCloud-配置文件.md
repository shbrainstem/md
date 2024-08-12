#### 一、两个默认配置文件

##### 1.1.application.yml
>application.yml 是Spring Boot应用中最常用的配置文件，它在Spring应用上下文完全初始化之后加载。这是存放大多数应用级配置的地方，比如数据源、JPA设置、日志级别、端口等。

###### 1.1.1.特点
- 加载较晚，通常在所有Spring Bean都初始化完成之后。
- 适用于不需要在启动早期就确定的配置。
- 可以覆盖默认配置和其他配置源的配置。

######  1.1.2.示例
```
server:
  port: 8080

spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
    username: user
    password: pass
```
##### 1.2.bootstrap.yml
>bootstrap.yml 是在Spring Boot应用启动早期加载的配置文件，主要用于初始化Spring Environment，它比application.yml更早被加载。

######  1.2.1.特点
- 加载最早，在Spring Boot的配置加载链路中是最先被读取的。
- 主要用于配置Spring Cloud Config Server、Nacos、Consul等外部配置中心，以及一些需要在启动初期就确定的配置，比如加密密钥、OAuth2认证信息等。
- 不能被application.yml或application.properties中的配置覆盖。
###### 1.2.2.示例

```
spring:
  cloud:
    config:
      uri: http://config-server:8888
      profile: dev
      label: master
      name: myapp
```
##### 1.3.注意事项
- 如果同时使用了bootstrap.yml和application.yml，请确保它们之间没有冲突的配置，bootstrap.yml中的配置无法被application.yml覆盖。
- 还可以使用.properties扩展名替代.yml，即bootstrap.properties和application.properties。
- 在Spring Boot 2.x版本中，YAML配置文件的支持得到了增强，包括对嵌套对象和集合的支持，使得配置更加灵活和强大。

#### 二、不同环境读不同配置

##### 2.1 如何定义不同的环境配置

###### 2.1.1.创建配置文件：
> 为每个环境创建单独的配置文件。这些文件的命名通常遵循application-{profile}.yml或application-{profile}.properties的模式，其中{profile}是环境的名称。例如，对于开发环境，文件名是application-dev.yml；对于生产环境，则是application-prod.yml。

###### 2.1.2.在配置文件中定义配置项：
>在每个配置文件中，你可以定义特定于该环境的配置。

```
 # application-dev.yml
spring:
  profiles: dev
  datasource:
    url: jdbc:mysql://localhost:3306/dev_db
    username: dev_user
    password: dev_pass

 # application-prod.yml
spring:
  profiles: prod
  datasource:
    url: jdbc:mysql://prod-db.example.com:3306/prod_db
    username: prod_user
    password: prod_pass
```

##### 2.2如何激活特定的环境配置
###### 2.2.1.使用spring.profiles.active属性：
> 你可以在启动应用时通过命令行参数、环境变量或配置文件来设置spring.profiles.active属性，以激活特定的Profile。

```
java -jar myapp.jar --spring.profiles.active=dev
```

>或者在application.properties或application.yml中设置：

```
# application.properties
spring.profiles.active=dev
```

###### 2.2.2.使用spring-boot-devtools
>如果你使用了spring-boot-devtools依赖，那么在开发环境中，它会自动激活spring.devtools.add-properties=true，这会将spring-boot-devtools的一些属性添加到活动的profiles中，比如spring.devtools.restart.enabled。

##### 2.3动态配置和Spring Cloud Config Server
>对于更复杂或大型的微服务架构，你可能希望使用Spring Cloud Config Server来集中管理配置。在这种情况下，你可以将配置文件托管在Config Server上，并在应用中指定spring.cloud.config.uri和spring.profiles.active来拉取和激活特定环境的配置。

在bootstrap.yml中，你可以这样配置

```
spring:
  cloud:
    config:
      uri: http://config-server:8888
      profile: dev
      label: master
```
> 这里，dev是激活的Profile，而master是Git仓库的分支名，Config Server将从该分支下拉取dev环境的配置。

