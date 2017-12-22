# cloud
spring-cloud的eureka组件，用来简化与服务器的交互、作为轮询负载均衡器，并提供服务的故障切换支持

#项目启动

idea启动：运行com.cloud.cloud.CloudApplication 类文件就可以了

#项目部署
1：jar包部署:
~~~
    mvn clean && mvn package
    nohup java -jar cloud.jar >log.file 2>&1 &
    tail -f logfile

~~~

2.war包部署：

1：添加pom.xml
~~~
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>javax.servlet-api</artifactId>
		</dependency>

		<!--打war包时加入此项 告诉spring-boot tomcat相关jar包用外部的-->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-tomcat</artifactId>
			<scope>provided</scope>
		</dependency>
  
~~~

2.修改com.cloud.cloud.CloudApplication 类

~~~
@EnableEurekaServer
@SpringBootApplication
public class CloudApplication  extends SpringBootServletInitializer {

	public static void main(String[] args) {
		SpringApplication.run(CloudApplication.class, args);
	}

	protected SpringApplicationBuilder configure(SpringApplicationBuilder builder) {
		builder.sources(this.getClass());
		return super.configure(builder);
	}
}

  
~~~