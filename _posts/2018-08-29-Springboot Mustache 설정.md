---
layout:     post
title:      "Springboot Mustache .yml 설정"
subtitle:   "스프링부트에서 Mustache를 사용하기위한 설정"
date:       2018-08-29 12:00:00
author:     "Nekisse"
header-img: "img/post-bg-02.jpg"
---

# Springboot Mustache 설정

pom.xml에 추가

```
<dependency>
 		<groupId>org.springframework.boot</groupId>
         	<artifactId>spring-boot-starter-mustache</artifactId>
 </dependency>
```




.yml 에 추가

```
  mustache:
     allow-request-override: false
     allow-session-override: false
     cache: false
     charset: UTF-8
     check-template-location: true
     content-type: text/html
     enabled: true
     expose-reques˚t-attributes: false
     expose-session-attributes: false
     expose-spring-macro-helpers: true
     spring.mustache.prefix=classpath: /templates/
     request-context-attribute:
     suffix: .html
     spring.mustache.view-names:
```

​
