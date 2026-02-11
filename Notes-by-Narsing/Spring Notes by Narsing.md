> [!NOTE]
>
> # Spring Core
>

####   **What are the key features of the Spring Framework?**
>  **Definition,** Spring framework is a light weight, loosely coupled, integrated, open-source framework for development of enterprise application in java.

* **Lightweight,** doesn't force developer to implement any interface.
* **Loose coupling,** we can develop loosely coupled applications using DI . loosely coupled means classes and methods are completely independent to each other . means we can make code changes easily.
* **Ready-made Templates,** it provides readymade templates of hibernate like jdbctemplate, jpa where no need to write lots of code for connections, exception handling and committing the transections all are done automatically.
* **Fast development**
* **Powerful abstraction**

### **What is IOC container?** 

* Inversion of Control (IOC) is the design principle where the control of object creation, configuration and management is transferred from programmer to spring framework.
* IOC container is a core part of spring framework which is used to manage the application beans
* It is responsible for Dependency Injection and managing the life cycle of beans.
* Task of IOC container, Instantiating, Assembling, Configuration of beans.

### **Types of IOC container?**

*** Bean Factory**, is a basic container. Its depreciated now.

```java
    Resource resource=new ClassPathResource("bean.xml");
    BeanFactory beanFactory=new XmlBeanFactory(resource);
```

* **Application Context,** advance container which provide more functionalities than bean Factory. 
```java
ApplicationContext context=new ClassPathXmlApplicationContext("bean.xml");
```

> Note , bean file should be in resource folder

### **Explain Dependency Injection (DI) in Spring.**

Dependency Injection is a design pattern where the dependencies of a class are injected by the Spring container rather than being instantiated manually.

**Example,**

**Without DI ,**

// without DI Here is dependacy between employee and address because employee forced

//to use same add object

```java
public  class  Employee {
Address address;
Employee(){
Address  add = new  Address(); // creating instance
}
}
```

**With DI ,**

// there is no dependancy between employe and address bacause

//employee is not forced to use same address

```java
**public** **class** Employee {

Address address;

**Employee**( Address address){

**this**.address=address; // not creating instance

}

}
```

**Ways of DI,**

1. **DI by using Constructor,** we can inject value by constructor <constructor-args> sub element of bean.
2. **DI by using Setter Method ,** we can use setter method for DI by using <property> sub element of bean.

Example ,

```xml
<!-- setter based injection -->

<bean id="studentbean" class="com.springtutorial.Student">

<property name="name" value="Nirav"></property>

</bean>


<!-- constructor based injection -->

<bean id="stdbean" class="com.springtutorial.Student">

<constructor-arg name="name" value="Nikita"></constructor-arg>

</bean>
```

```java
public   class  Student {

 private  String name;

 public  String  getName () {

 return  name;

}

// setter based DI

 public   void   setName (String name) {

 this .name = name;

}

// constrctor based DI

 public   Student (String name) {

 this .name = name;

}

 public   Student () {

 super ();

}

 public   void   display () {

System. out .println("Hello mr . "  name);

}

}
```

## **Spring Bean and Configuration**

### **Bean Life Cycle**

1. Bean is instantiated
2. Dependency is injected
3. Bean Initializations
4. Bean used
5. Bean destroyed

## Spring - Bean Scopes

|  |  |
| --- | --- |
| Sr.No. | Scope & Description |
| 1 | **singleton**  A single instance per Spring IoC container (default). @Scope(“singleton”) |
| 2 | **prototype**  new instance created each time when bean is requested. |
| 3 | **request**  new instance created each new HTTP request. |
| 4 | **session**  New bean created for each new HTTP Session. |
| 5 | **global-session**  This scopes a bean definition to a global HTTP session. |

## **What are different ways to configure a Spring Bean?**

1. **XML Configuration (beans.xml)**

**Example ,**

XML configuration was a common way to define beans. You specify the beans and their dependencies in an XML file, typically named `applicationContext.xml`.

```xml
<?xml version = "1.0" encoding = "UTF-8"?>

<beans xmlns = "http,//www.springframework.org/schema/beans"

xmlns,xsi = "http,//www.w3.org/2001/XMLSchema-instance"

xsi,schemaLocation = "http,//www.springframework.org/schema/beans

http,//www.springframework.org/schema/beans/spring-beans-3.0.xsd">

<!-- DI inection using constructor -->

<bean id="constructorbased" class="com.DependencyInjectionTutorial.Person">

<constructor-arg name="name" value="narsing"></constructor-arg>

<constructor-arg name="age" value="45"></constructor-arg>

<constructor-arg name="surname" value="pendharkar"></constructor-arg>

</bean>

<!-- DI injection using setter method -->

<bean id="setterbased" class="com.DependencyInjectionTutorial.Person">

<property name="age" value="28"></property>

<property name="name" value="narsing"></property>

<property name="surname" value="pendharkar"></property>

</bean>

</beans>
```

1. **Java-Based Configuration (@Configuration)**

* Java-based configuration allows you to configure beans using Java classes. You can use the **@Configuration** and **@Bean** annotations.
* Annotating a class with the **@Configuration** indicates that the class can be used by the Spring IoC container as a source of bean definitions.
* The **@Bean** annotation tells Spring that a method annotated with **@Bean** will return an object that should be registered as a bean in the Spring application context.

**Example ,**

```java
@Configuration

@ComponentScan("com.DependencyInjectionTutorial")

public class PersonJavaBasedConfig {

@Bean("constructorBasedPerson")

public Person constructorBasedPerson() {

Person person1 = new Person("JavaBased", 1, "Configuration Using constructor");

return person1;

}

@Bean("setterBasedPerson")

public Person setterBasedPerson() {

Person person2 = new Person();

person2.setAge(1);

person2.setName("JavaBased");

person2.setSurname("Configuration Using Setter Mathod");

return person2;

}

}
```
1. **Annotation-Based Configuration** (@Component, @Service, @Repository)

* Once <context,annotation-config/> is configured, you can start annotating your code to indicate that Spring should automatically wire values into properties, methods, and constructors

**Example ,**

```java
@Component("personbean")

public class PersonAnnotationBasedConfig {

private String name;

private int age;

private String surname;

PersonAnnotationBasedConfig() {

this.age = 2;

this.name = "Annotation based";

this.surname = "Configuration";

}

public PersonAnnotationBasedConfig(String name, int age, String surname) {

super();

this.name = name;

this.age = age;

this.surname = surname;

}

@Override

public String toString() {

return "Person [name="  name  ", age="  age  ", surname="  surname  "]";

}

}

```

### **Steps to Create a Spring Core Application**

1. Create a Maven Application

* Use the Quickstart archetype to generate a basic Maven project.

1. Add Dependencies

* Add **Spring Core** and **Spring Context dependencies** in pom.xml.

1. Create an Entity Class (POJO)

* Define a simple class with private fields, getters/setters, and constructors.

1. Configure Beans (Based on Configuration Type)

* **XML-Based**, Create beans.xml inside the resources folder and define beans.
* **Java-Based,** Create a @Configuration class and define beans using @Bean.
* **Annotation-Based,** Use @Component on a class to let Spring manage it.

1. Initialize Application Context in Main Class

* Use **ClassPathXmlApplicationContext** for XML-based configuration.
* Use **AnnotationConfigApplicationContext** for Java-based and annotation-based configuration.

1. Retrieve and Use Beans

* Call **getBean()** from **ApplicationContext** to retrieve and use the beans in the application.

1. Run the Application

* Execute the main class to verify that Spring loads and manages beans correctly.

Example,
```java
public class MainApplicationToRun

{

public static void main(String[] args) {

// 1️ Create IOC container using XML-based configuration

ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");

// Retrieve beans from XML configuration (setter-based and constructor-based)

Person p = (Person) context.getBean("setterbased");

System.err.println("XML Configuration (Setter-based Bean), "  p);

Person p2 = (Person) context.getBean("constructorbased");

System.err.println("XML Configuration (Constructor-based Bean), "  p2);

// 2️ Annotation-based configuration


ApplicationContext annotationContext = new AnnotationConfigApplicationContext(PersonAnnotationBasedConfig.class);

// Retrieve bean from @Component-based configuration

PersonAnnotationBasedConfig annotatedBean = (PersonAnnotationBasedConfig) annotationContext.getBean("personbean");

System.out.println("Annotation-based Configuration, "  annotatedBean);


// 3️⃣ Java-based configuration


ApplicationContext javaContext = new AnnotationConfigApplicationContext(PersonJavaBasedConfig.class);

// Retrieve beans from Java-based configuration

Person javaPerson1 = (Person) javaContext.getBean("constructorBasedPerson");

System.out.println("Java-based Configuration (Constructor-based Bean), "  javaPerson1);

Person javaPerson2 = (Person) javaContext.getBean("setterBasedPerson");

System.out.println("Java-based Configuration (Setter-based Bean), "  javaPerson2);

}

}
```

###  **What is the difference between @Component, @Service, and @Repository?**

|  |  |
| --- | --- |
| **Annotation** | **Purpose** |
| @Component | Generic bean for any class |
| @Service | Specifically for business logic/service layer |
| @Repository | Used in the DAO layer and integrates exception translation |

###  **What is the difference between @Bean and @Component?**

|  |  |  |
| --- | --- | --- |
| **Feature** | @**Bean** | @**Component** |
| Usage | Method-Level | Class-Level |
| Configuration Required | Yes (@Configuration) | No |
| Auto-Scanning | No | Yes |

**Example,**
```java
@Configuration

class AppConfig {

@Bean

public Engine engine() {

return new Engine();

}
}

```
# **Spring MVC**

**What is Spring MVC and its features.**

* Spring MVC is the sub framework of spring which is used for the development of web applications.
* Spring MVC follows the MVC pattern which separates the application in three parts i.e Model , View and Controller
* **Easy Development,** MVC pattern makes easy development
* **Rapid Development**, it helps for faster development.
* Powerful configuration.
* It uses all features of spring core.
* It is flexible, easy to test and much features.

**Explain the flow of a Spring MVC application.**

1. **Client Request** → client Sent request to the Dispatcher Servlet
2. **DispatcherServlet** → receive request from client and request to the appropriate Controller
3. **Controller** → Processes request and returns Model(data) and View (name of view)
4. **ViewResolver** → Selects the appropriate view (JSP, Thymeleaf, etc.)
5. **View (JSP/Thymeleaf)** → Data and view merged as sent as response

![Spring DispatcherServlet](data,image/png;base64...)

**Explain Dispatcher Servlet in Spring MVC.**

* Dispatcher servlet serve as Front Controller who manage all the request and sent it to respective controller.
* Dispatcher Servlet is a class which receive all incoming request from client and maps it to appropriate controller, model, and view.
* Configuration of Dispatcher servlet done in `web.xml` file as below

```xml
<servlet>

<servlet-name>HelloWeb</servlet-name>

<servlet-class>

org.springframework.web.servlet.DispatcherServlet

</servlet-class>

<load-on-startup>1</load-on-startup>

</servlet>

<servlet-mapping>

<servlet-name>HelloWeb</servlet-name>

<url-pattern>\*/</url-pattern>

</servlet-mapping>
```

![](data,image/png;base64...)

**Explain InternalViewResolver in Spring MVC.**

* It is a class which is used to resolve the internal view in Spring MVC.
* We can define the properties like prefix and suffix where prefix contains location of view and suffix contains extension of view page.
* Example ,

*<!-- used to map vies according to controller -->*

<bean name="viewResolver"

class="org.springframework.web.servlet.view.InternalResourceViewResolver">

<property name="prefix" value="/WEB-INF/views/" />

<property name="suffix" value=".jsp" />

</bean>

Explain Model,ModelMap and ModelAndView in Spring MVC.

1. Model , it is used to pass information from controller to view using model object.

```java
Model model = new Model();

model.addAttribute("msg", “hello “));
```

1. ModelMap , it is similar to model only difference is that it provides map functionalities.
   Methods , addAttribute(), get(),put()
2. ModelAndView, If you want to return model and view in same object then we can use ModelAndView class object.

```java
public ModelAndView showWelcomePage() {

ModelAndView mav = new ModelAndView();

mav.setViewName("welcome");

mav.addObject("message", "Hello, Spring MVC!");

return mav;

}
```

What are @RequestMapping and its variants?

* @RequestMapping("/path") → General mapping
* @GetMapping("/path") → Maps HTTP GET request
* @PostMapping("/path") → Maps HTTP POST request
* @PutMapping("/path") → Maps HTTP PUT request
* @DeleteMapping("/path") → Maps HTTP DELETE request

What is @ModelAttribute in Spring MVC?

It binds form data to a model object.

Example,

```java
@PostMapping("saveTask")

public String saveTask(@ModelAttribute Tasks tasks, BindingResult bindingResult,

@RequestParam("assignee") int userid, Model model) throws SQLException {

if (bindingResult.hasErrors()) {

model.addAttribute("message", "Plese enter proper detials");

return "redirect,/createtask";

} else {

User assigenedUser = userService.userbyid(userid);

tasks.setAssignedUser(assigenedUser);

taskserviceImpl.saveTask(tasks);

System.*out*.println("saved");

model.addAttribute("message", "Task added !");

return "redirect,/tasks-list";

}

}
```

Core Spring Annotations-

These annotations are primarily used for dependency injection (DI) and component scanning in Spring.

@Component , Marks a Java class as a Spring-managed bean
Example,


```java
 @Component
public class MyComponent {

public void sayHello() {

System.*out*.println("Hello from MyComponent");

}

}
```

@Service

* Definition, Specialized version of @Component, used to mark a service layer class which contains business.

Example,
```java
*@Service*

public class UserService {

public String getUser() {

return "Nirav";

}
```

@Repository

* Definition, Used to indicate that a class is responsible for data access logic (DAO layer) and interaction with database.

Example,
```java
@Repository

public class UserRepository {

public void saveUser() {

System.out.println("User saved!");

}
}
```

@Autowired

* Definition, Automatically injects dependencies where required.

Example,
 *@Autowired*

private TaskRepository taskRepository;

@Qualifier

* Definition, Used along with @Autowired to resolve ambiguity when multiple beans of the same type exist.

Example,
```java
@Component("bean1")

public class MyBean1 {}

@Component("bean2")

public class MyBean2 {}

@Service
public class MyService {

@Autowired

@Qualifier("bean1")

private MyBean1 myBean;

}

```
@Value
* Definition, Injects values from properties files into Spring beans or assign default value to methods.

Example,
```java
@Value("${app.name}")

private String appName;
```

@Scope

* Definition, Defines the scope of a Spring bean (singleton, prototype, request, etc.).

Example,
```java
@Component
@Scope("prototype")
public class PrototypeBean {}
```

### Spring MVC Annotations

@Controller

* Definition, Marks a class as a Spring MVC controller to handle HTTP requests.

Example,
*@Controller*

public class TaskController {}

@RestController

* Definition, A combination of @Controller and @ResponseBody, used for RESTful APIs.

Example,

```java
@RestController

public class ApiController {

*@GetMapping*("/data")

public String getData() {

return "Hello API!";

}

}
```

@RequestMapping

* Definition, Maps HTTP requests to controller methods.

Example,
```java
@Controller

@RequestMapping("/user")

public class UserController {

@GetMapping("/profile")

public String showProfile() {

return "profile";

}

}
```

@GetMapping, @PostMapping, @PutMapping, @DeleteMapping

* Definition, Shortcut annotations for specific HTTP methods.

Example,
```java
@GetMapping("dashboard" )

public String dashboardPage(Model model) {

return "Dashboard";

}
```

@PathVariable

* Definition, Extracts values from the URL path.
* URL , *localhost,8080/deleteTask/2*

Example,
```java
@GetMapping("deleteTask/{id}")

public String deleteTask(*@PathVariable*("id") int taskId, Model model) throws SQLException {

taskserviceImpl.deleteTask(taskId);

model.addAttribute("message", "Task deleted!");

return "redirect,/tasks-list";

}
```

@RequestParam

* Definition, Extracts query parameters from the URL*.*
* *URL* *, localhost,8080/search?keyword=”google*”

Example,
*@GetMapping*("/search")

public String search(*@RequestParam* String keyword) {

return "Searching for, "  keyword;

}

@ModelAttribute

* Definition, Binds from data into java object.

Example,
*@PostMapping*("/register")

public String registerUser(*@ModelAttribute* User user) {

userService.save(user);

return "success";

}

@ExceptionHandler ,@ControllerAdvice

* Definition, This annotation used to handle the specific exceptions and sending custom message and controller advice annotation is used to handle exceptions globally

Example,
```java
@ControllerAdvice

public class GlobalExceptionHandler {

// Exception handler method to catch InvalidUserException

@ExceptionHandler(InvalidUserException.class)

public String handleInvalidUserException(InvalidUserException ex, Model model) {

model.addAttribute("message", ex.getMessage());

return "Login";

}
```

Spring Boot Annotations

@SpringBootApplication

* Definition, Marks the main Spring Boot application class.

Example,
```java
@SpringBootApplication

public class DemoAppMssqlApplication {

public static void main(String[] args) {

SpringApplication.*run*(DemoAppMssqlApplication.class, args);

}

```
@JsonIgoner & @JsonIgnoreProperties

* Definition, used to filter out the fields data form response. These fields are not sent in response.

Example,
```java
@Entity

@JsonIgnoreProperties({"password", "username"})

public class User {

@Id

@GeneratedValue(strategy = GenerationType.*SEQUENCE*,generator = "userseq")

@SequenceGenerator(name="userseq",sequenceName = "userseq", initialValue = 1000, allocationSize = 1)

private Long id;

@Column(unique = true, nullable = false)

private String username;

@Column(nullable = false)

@JsonIgnore

private String password;
```

@Configuration

* Definition, Marks a class as a Spring configuration class and it is a source of beans.

Example,
 ```java
@Configuration

public class AppConfig {

@Bean

public MyService myService() {

return new MyService();

}

}
 ```

@EnableScheduling

* Definition, Enables scheduling tasks. When @EnableScheduling Annotation added in Configuration class then spring looks for @Scheduled annotated method and runs that method automatically in fixed period of time.

Example,
```java
 @EnableScheduling

public class SchedulerConfig {}

@Scheduled(fixedRate = 5000)

public void scheduleTask() {

System.out.println("Running every 5 seconds");

}
```

Spring Data JPA Annotations

Used for database interaction.

```java
@Entity

* Definition, Marks a class as a JPA entity (database table representation).

Example,
@Entity

public class Tasks {

@Id

@GeneratedValue(strategy = GenerationType.IDENTITY)

private Long task\_id;

@NotNull

private String title;

@NotNull

private String description;

@Temporal(TemporalType.DATE)

private Date deadline;

@Enumerated(EnumType.STRING)

private Priority priority;

@Enumerated(EnumType.STRING)

private TaskStatus status;

@ManyToOne

@JoinColumn(name = "user\_id")

private User assignedUser;
```

@Transactional

* Definition, it is used with methods or classes that are communicating with database and performing some operation. If some reason method is failed or error occurred to complete the operation then this annotation automatically rollback the transactions.
* @EnableTransactionManagements , To use above annotation we need to add this annotation to your main application class.
* Example,

```java
@SpringBootApplication

@EnableTransactionManagement

public class DemoAppMssqlApplication {

public static void main(String[] args) {

SpringApplication.run(DemoAppMssqlApplication.class, args);

}
```

```java
@Transactional

public void updateUser(User user) {

userRepository.save(user);

}
```

Spring Security Annotations

Used for authentication and authorization.

@EnableWebSecurity

* Definition, Enables Spring Security in the application.

Example,
 @EnableWebSecurity

public class SecurityConfig extends WebSecurityConfigurerAdapter {}

@PreAuthorize

* Definition, Restricts access to a method based on roles.

Example:

`@PreAuthorize("hasRole('ADMIN')")`

public void adminOnly() {}

What is the difference between Spring MVC and Spring Boot?

|  |  |  |
| --- | --- | --- |
| Feature | Spring MVC | Spring Boot |
| Configuration | Manual | Auto-configured |
| Embedded Server | No | Yes (Tomcat, Jetty) |
| Dependencies | More setup needed | Minimal setup |

What is @SpringBootApplication?

It is a combination of,

* @Configuration
* @EnableAutoConfiguration
* @ComponentScan

# Spring Data JPA & Transactions

What is Spring Data JPA?

Spring Data JPA simplifies database operations by providing a repository abstraction layer.

Example,

*@Repository*

public interface EmpRepository extends JpaRepository<Employee, Long>{

}

Spring Security Questions

How do you secure a Spring Boot application?

* Use Spring Security (spring-boot-starter-security)
* Configure authentication (UserDetailsService)
* Implement JWT (JSON Web Token)

Example,

@Configuration

@EnableWebSecurity

public class SecurityConfig {

@Bean

public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {

http.authorizeHttpRequests(auth -> auth.anyRequest().authenticated())

.formLogin();

return http.build();

}

}

# Microservices & Cloud Questions

What is Spring Cloud?

Spring Cloud is used for developing distributed microservices-based applications. It provides features like,

* Service Discovery (Eureka)
* API Gateway (Zuul / Spring Cloud Gateway)
* Load Balancing (Ribbon)
* Circuit Breaker (Resilience4J)

What is @FeignClient in Spring Cloud?

Feign is a REST client that simplifies HTTP calls in microservices. Example,

@FeignClient(name = "user-service")

public interface UserClient {

@GetMapping("/users/{id}")

User getUserById(@PathVariable Long id);

}

What is Spring AOP?

Aspect-Oriented Programming (AOP) is used to separate cross-cutting concerns (logging, security, transactions).

Example,

@Aspect

@Component

public class LoggingAspect {

@Before("execution(\* com.example.service.\*.\*(..))")

public void logBefore(JoinPoint joinPoint) {

System.out.println("Method Called, "  joinPoint.getSignature().getName());

}

}

What is the difference between @RestController and @Controller?

* @Controller → Returns views (JSP, Thymeleaf)
* @RestController → Returns JSON/XML responses

Example,

@RestController

@RequestMapping("/api")

public class ApiController {

@GetMapping("/hello")

public String sayHello() {

return "Hello, World!";

}

}

What is the difference JDBC, JDBC template, JPA, Spring Data JPA?

|  |  |  |  |
| --- | --- | --- | --- |
| JDBC | JDBC Template | JPA | Spring Data JPA |
| Write java code | Small java code | Just provide Mapping | Use JPARepository Interface it will take care of everything. |
| Write Sql Queries | Write SQL Queries | No need to write Query | No need to write Query |

What is Spring Security?

Answer,

* Spring Security is a powerful authentication and authorization framework for Java applications, primarily used in Spring-based projects.
* It provides built-in security features like,

1. Authentication (Who are you?)
2. Authorization (What can you do?)
3. Protection against security threats like CSRF, XSS, session fixation, clickjacking, etc.
4. Integration with OAuth2, JWT, LDAP, and custom authentication mechanisms

Example,
If a user tries to access /admin, Spring Security will check whether they have the ADMIN role before granting access.

Spring Security architecture

![Spring Security Architecture](data,image/png;base64...)

Security filter chain ,

* This is used to filter the requests and it also authenticate and authorise the user
* Filter run the first in processing order
* We can add custom filters in applications

Authentication ,

* When user submit login form
* AuthenticationManager receive the request
* It used DaoAuthenticationProvider object to fetch user details by using userservicedetails
* And also, user password encoder to compare password
* If authentication is successful, it returns authentication manager object

Authorisation ,

* Once authentication is successful , system will check the roles of user and according to that resource access is granted
* If not, then system give exception.

Why use Spring Security?

*  Provides authentication and authorization
   Prevents common security threats (CSRF, XSS, SQL Injection, etc.)
   Supports integration with OAuth2, JWT, LDAP, etc.
   Highly customizable

Adding Spring Security to a Spring Boot Project

1. Dependencies (Maven) for spring boot,

<dependency>

<groupId>org.springframework.boot</groupId>

<artifactId>spring-boot-starter-security</artifactId>

</dependency>

1. For Spring MVC

<!--spring-webmvc -->

<dependency>

<groupId>org.springframework</groupId>

<artifactId>spring-webmvc</artifactId>

<version>7.0.0-M2</version>

</dependency>

<!--spring-context -->

<dependency>

<groupId>org.springframework</groupId>

<artifactId>spring-context</artifactId>

<version>7.0.0-M2</version>

</dependency>

<!-- spring-security-web -->

<dependency>

<groupId>org.springframework.security</groupId>

<artifactId>spring-security-web</artifactId>

<version>6.4.3</version>

</dependency>

<!-- spring-security-core -->

<dependency>

<groupId>org.springframework.security</groupId>

<artifactId>spring-security-core</artifactId>

<version>6.4.3</version>

</dependency>

<!-- spring-security-config -->

<dependency>

<groupId>org.springframework.security</groupId>

<artifactId>spring-security-config</artifactId>

<version>6.4.3</version>

</dependency>

* By default, Spring Security provides a login form with a generated username (user) and password (logged in the console).

Configuring Spring Security (Basic Authentication)

Custom Security Configuration (IN Memory Authentication)

@Configuration

@EnableWebSecurity

public class SecurityConfig {

@Bean

public BCryptPasswordEncoder passwordEncoder() {

return new BCryptPasswordEncoder();

}

// In-memory authentication setup

@Bean

public UserDetailsService userservice() {

UserDetails user1 = User.withUsername("user")

.password(passwordEncoder().encode("u123"))

.authorities("USER")

.build();

UserDetails admin = User.withUsername("admin")

.password(passwordEncoder().encode("a123"))

.authorities("ADMIN")

.build();

return new InMemoryUserDetailsManager(user1, admin);

}

@Bean

public SecurityFilterChain filter(HttpSecurity http) throws Exception {

http.csrf(csrf -> csrf.disable())

.authorizeHttpRequests(auth -> auth

.requestMatchers("/admin/\*\*").hasAuthority("ADMIN")

.requestMatchers("/user/\*\*").hasAuthority("USER")

.anyRequest().authenticated()

)

.formLogin(form -> form

.defaultSuccessUrl("/home", true)

.permitAll()

)

.logout(logout -> logout

.permitAll()

)

.exceptionHandling(exception -> exception

.accessDeniedHandler((request, response, accessDeniedException) -> {

response.setStatus(403); // Forbidden

response.getWriter().write("You are not authorized to access this resource!");

})

);

return http.build();

}

@Bean

public AuthenticationManager authManager(UserDetailsService userDetailsService) {

DaoAuthenticationProvider provider = new DaoAuthenticationProvider();

provider.setUserDetailsService(userDetailsService);

provider.setPasswordEncoder(passwordEncoder());

return new ProviderManager(provider);

}

}

User Authentication (Database)

Replace in-memory authentication with database authentication using UserDetailsService.

Step 1, Create User Entity

@Entity

@Table(name = "users")

public class Users {

@Id

@GeneratedValue(strategy = GenerationType.IDENTITY)

private Long id;

private String username;

private String password;

private String role;

Step 2, Create UserRepository

@Repository

public interface Userrepository extends JpaRepository<Users, Integer> {

Optional<Users> findByUsername(String username);

}

Step 3, Implement UserDetailsService

@Service

public class Usersservice implements UserDetailsService {

@Autowired

private Userrepository userrepository;

@Override

public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {

Users foundUser=userrepository.findByUsername(username).orElseThrow(()->new UsernameNotFoundException("User not found"));

return new User(foundUser.getUsername(),

foundUser.getPassword(),

Collections.singletonList(new SimpleGrantedAuthority(foundUser.getRole())));

}

Step 4, Update Security Configuration

@Autowired

private Usersservice usersservice;

@Bean

public BCryptPasswordEncoder passwordEncoder() {

return new BCryptPasswordEncoder();

}

@Bean

public AuthenticationManager authManager() { DaoAuthenticationProvider

authenticationProvider=new DaoAuthenticationProvider();

authenticationProvider.setUserDetailsService(usersservice);

authenticationProvider.setPasswordEncoder(passwordEncoder()); return new

ProviderManager(authenticationProvider);

}

Note , if we don’t define AuthenticationManager bean in our application and we implemented UserServiceDetails and service bean is injected in config class then spring automatically create authenticationmanager bean .

# JWT Authentication & Authorization in Spring Security

## What is JWT?

JWT (JSON Web Token) is a compact, URL-safe token used for authentication and authorization. It consists of three parts,

🔹 Header – Contains token type (JWT) and signing algorithm (e.g., HS256).

🔹 Payload – Contains claims (user details, roles, expiration).

🔹 Signature – Ensures integrity and authenticity of the token.

## How JWT Works in Spring Security

1. User logs in → Sends username & password to the authentication endpoint.
2. Spring Security validates credentials using AuthenticationManager.
3. JWT is generated and returned to the client.
4. Client stores JWT (localStorage/sessionStorage) and includes it in the Authorization header for further requests.
5. Spring Security filters validate the JWT on every request.

### Flow to Implement JWT Authentication in Spring Boot

Here is a step-by-step guide to creating your JWT Authentication project based on the code you've provided.

## Step 1, Set Up the Spring Boot Project

* Create a Spring Boot project using Spring Initializr or manually with spring-boot-starter-security, spring-boot-starter-web, spring-boot-starter-data-jpa, and jjwt.

## Step 2, Configure Application Properties

* Define JWT properties and database configuration in application.properties or

narsing.app.Secret= ======================Narsing=token===========================

narsing.app.ExpirationMs=360000

## Step 3, Create the Person Entity

* This entity will represent the user in the database.

@Entity

@Table(name = "users")

public class Person {

@Id

@GeneratedValue(strategy = GenerationType.IDENTITY)

private Long id;

private String username;

private String password;

private String role;

## Step 4, Create the PersonRepository

* This repository will interact with the database.

@Repository

public interface PersonRepository extends JpaRepository<Person, Long> {

Optional<Person> findByUsername(String username);

}

## Step 5, Implement PersonService for User Authentication

* This service will load user details from the database and encode passwords.

@Service

public class PersonService implements UserDetailsService{

@Autowired

private PersonRepository userRepository;

@Autowired

private PasswordEncoder passwordEncoder;

@Override

public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {

Person databasePerson = userRepository.findByUsername(username).orElseThrow(()->new UsernameNotFoundException("User not found"));

SimpleGrantedAuthority userRole = new SimpleGrantedAuthority("ROLE\_"  databasePerson.getRole());

User user = new User(databasePerson.getUsername(), databasePerson.getPassword(),

Collections.singletonList(userRole));

return user;

}

## Step 6, Implement MethodsOfJwt for Token Generation & Validation

* This utility class generates, parses, and validates JWT tokens.

@Component

public class MethodsOfJwt {

private static Logger logger = LoggerFactory.getLogger(MethodsOfJwt.class);

@Value("${narsing.app.Secret}")

private String sercretKey;

@Value("${narsing.app.ExpirationMs}")

private int expiryTime;

public String generateTokenFromUsername(UserDetails userDetails) throws InvalidKeyException {

String username = userDetails.getUsername();

return Jwts.builder().subject(username).issuedAt(new Date())

.expiration(new Date((new Date()).getTime()  expiryTime)).signWith(key()).compact();

}

public String getUsernamefromToken(String token) {

String username = Jwts.parser().verifyWith((SecretKey) key()).build().parseSignedClaims(token).getPayload()

.getSubject();

return username;

}

public boolean validateToken(String authToken) {

try {

System.out.println("Validate");

Jwts.parser().verifyWith((SecretKey) key()).build().parseSignedClaims(authToken);

return true;

} catch (MalformedJwtException e) {

logger.error("Invalid JWT token, {}", e.getMessage());

} catch (ExpiredJwtException e) {

logger.error("JWT token is expired, {}", e.getMessage());

} catch (UnsupportedJwtException e) {

logger.error("JWT token is unsupported, {}", e.getMessage());

} catch (IllegalArgumentException e) {

logger.error("JWT claims string is empty, {}", e.getMessage());

}

return false;

}

private Key key() {

return Keys.hmacShaKeyFor(Decoders.BASE64.decode(sercretKey));

}

public String getJwtFromHeader(HttpServletRequest request) {

String bearerToken = request.getHeader("Authorization");

logger.debug("Authorization Header, {}", bearerToken);

if (bearerToken != null && bearerToken.startsWith("Bearer ")) {

return bearerToken.substring(7); // Remove Bearer prefix

}

return null;

}

}

## Step 7, Implement TokenFilter for Request Filtering

* This filter extracts the JWT token and sets authentication.

@Component

public class TokenFilter extends OncePerRequestFilter {

private static final Logger logger = LoggerFactory.getLogger(TokenFilter.class);

@Autowired

private PersonService personService;

@Autowired

private MethodsOfJwt jwtmethod;

@Override

protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain)

throws ServletException, IOException {

logger.debug("AuthTokenFilter called for URI, {}", request.getRequestURI());

try {

String jwt = parseJwt(request);

if (jwt != null && jwtmethod.validateToken(jwt)) {

String username = jwtmethod.getUsernamefromToken(jwt);

UserDetails userDetails = personService.loadUserByUsername(username);

UsernamePasswordAuthenticationToken authentication = new UsernamePasswordAuthenticationToken(

userDetails, null, userDetails.getAuthorities());

logger.debug("Roles from JWT, {}", userDetails.getAuthorities());

authentication.setDetails(new WebAuthenticationDetailsSource().buildDetails(request));

SecurityContextHolder.getContext().setAuthentication(authentication);

}

} catch (Exception e) {

logger.error("Cannot set user authentication, {}", e);

}

filterChain.doFilter(request, response);

}

private String parseJwt(HttpServletRequest request) {

String jwt = jwtmethod.getJwtFromHeader(request);

logger.debug("AuthTokenFilter.java, {}", jwt);

return jwt;

}

}

## Step 8, Configure Spring Security

* Define security rules and set JWT authentication.

@Configuration

@EnableWebSecurity

@EnableMethodSecurity

public class AuthSecurityConfig {

@Bean

public EntryPoint entryPoint() {

return new EntryPoint();

}

@Bean

public TokenFilter getTokenFilter() {

return new TokenFilter();

}

@Bean

public BCryptPasswordEncoder passwordEncoder() {

return new BCryptPasswordEncoder();

}

@Bean

SecurityFilterChain defaultSecurityFilterChain(HttpSecurity http) throws Exception {

http.authorizeHttpRequests(authorizeRequests -> authorizeRequests.requestMatchers("/", "/login").permitAll()

.requestMatchers("/authuser").permitAll().requestMatchers("/admin").hasRole("ADMIN")

.requestMatchers("/user").hasAnyRole("ADMIN", "USER").anyRequest().authenticated());

http.sessionManagement(session -> session.sessionCreationPolicy(SessionCreationPolicy.STATELESS));

http.exceptionHandling(exception -> exception.authenticationEntryPoint(entryPoint()));

http.headers(headers -> headers.frameOptions(frameOptions -> frameOptions.sameOrigin()));

http.csrf(csrf -> csrf.disable());

http.addFilterBefore(getTokenFilter(), UsernamePasswordAuthenticationFilter.class);

return http.build();

}

@Bean

public AuthenticationManager getAuthenticationManager(AuthenticationConfiguration configuration) throws Exception {

return configuration.getAuthenticationManager();

}

}

## Step 9, Create Authentication Controller

* This handles user login and JWT generation.

@Controller

public class Homecontrol {

@Autowired

private AuthenticationManager authenticationManager;

@Autowired

private MethodsOfJwt methodsOfJwt;

@GetMapping("/hello")

@ResponseBody

public String sayHello() {

return "Hello";

}

@GetMapping(value = { "/", "/login" })

public String loginHello() {

return "login";

}

@PreAuthorize("hasRole('USER')")

@GetMapping("/user")

@ResponseBody

public String userEndpoint() {

return "Hello, User!";

}

@PreAuthorize("hasRole('ADMIN')")

@GetMapping("/admin")

@ResponseBody

public String adminEndpoint() {

return "Hello, Admin!";

}

// validate user

@PostMapping("/authuser")

public ModelAndView validateUser(@ModelAttribute Person person) {

Authentication auth;

try {

String username = person.getUsername();

String password = person.getPassword();

auth = authenticationManager.authenticate(new UsernamePasswordAuthenticationToken(username, password));

} catch (Exception e) {

ModelAndView errorView = new ModelAndView("errorPage"); // Return errorPage.jsp

errorView.addObject("message", "Bad credentials");

errorView.addObject("status", false);

return errorView;

}

SecurityContextHolder.getContext().setAuthentication(auth);

UserDetails userDetails = (UserDetails) auth.getPrincipal();

String jwtToken = methodsOfJwt.generateTokenFromUsername(userDetails);

List<String> roles = userDetails.getAuthorities().stream().map(item -> item.getAuthority())

.collect(Collectors.toList());

ModelAndView mv = new ModelAndView("responsePage"); // Return responsePage.jsp

mv.addObject("username", userDetails.getUsername());

mv.addObject("roles", roles);

mv.addObject("token", jwtToken);

return mv;

}

}

## Step 10, Create EntryPoint Class to handle unauthorised

public class EntryPoint implements AuthenticationEntryPoint {

private static final Logger logger = LoggerFactory.getLogger(EntryPoint.class);

@Override

public void commence(HttpServletRequest request, HttpServletResponse response,

AuthenticationException authException) throws IOException, ServletException {

logger.error("Unauthorized error, {}", authException.getMessage());

response.setContentType(MediaType.APPLICATION\_JSON\_VALUE);

response.setStatus(HttpServletResponse.SC\_UNAUTHORIZED);

final Map<String, Object> body = new HashMap<>();

body.put("status", HttpServletResponse.SC\_UNAUTHORIZED);

body.put("error", "Unauthorized");

body.put("message", authException.getMessage());

body.put("path", request.getServletPath());

final ObjectMapper mapper = new ObjectMapper();

mapper.writeValue(response.getOutputStream(), body);

}

}

Now, your JWT authentication project is fully implemented!

JWT (JSON Web Token) is used for stateless authentication.

Common Spring Security Annotations

|  |  |
| --- | --- |
| Annotation | Purpose |
| @EnableWebSecurity | Enables Spring Security |
| @PreAuthorize("hasRole('ROLE\_ADMIN')") | Method-level security |
| @Secured("ROLE\_USER") | Restrict method access |
| @RolesAllowed({"ROLE\_USER", "ROLE\_ADMIN"}) | Allows multiple roles |

Example, Securing Methods

@Service

public class UserService {

@PreAuthorize("hasRole('ADMIN')")

public String adminOnlyMethod() {

return "Admin Access";

}

@Secured({"ROLE\_USER"})

public String userAccessMethod() {

return "User Access";

}

}

How does authentication and authorization work in Spring Security?

Answer,
Spring Security uses filters and interceptors to handle authentication and authorization.

*Authentication Flow (Who are you?)*

1. A user sends login credentials (username & password).
2. AuthenticationManager checks credentials using UserDetailsService and PasswordEncoder.
3. If valid, Spring Security stores the user details in the SecurityContextHolder.

*Authorization Flow (What can you do?)*

1. After authentication, the system checks roles and permissions.
2. If the user has access rights, the request proceeds.
3. If not, Spring Security denies access (403 Forbidden error).

Example, Restricting Access

@Bean

public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {

http

.csrf(csrf -> csrf.disable())

.authorizeHttpRequests(auth -> auth

.requestMatchers("/admin/\*\*").hasAuthority("ROLE\_ADMIN")

.requestMatchers("/user/\*\*").hasAuthority("ROLE\_USER")

.requestMatchers("/doctor/\*\*").hasAuthority("ROLE\_DOCTOR")

.requestMatchers("/", "/login", "/register").permitAll()

.anyRequest().authenticated()

)

.formLogin(login -> login

.loginPage("/medcare/login")

.loginProcessingUrl("/login")

.defaultSuccessUrl("/dashboard", true)

.permitAll()

)

.logout(logout -> logout

.logoutUrl("/medcare/logout")

.logoutSuccessUrl("/medcare/login")

.permitAll()

)

.exceptionHandling(exception -> exception

.authenticationEntryPoint((request, response, authException) -> {

response.sendRedirect("/medcare/login"); // Redirect to login page instead of /error

})

);

return http.build();

}

What is the difference between @PreAuthorize, @Secured, and @RolesAllowed?

Answer,
These annotations are used for method-level security in Spring Security.

|  |  |  |
| --- | --- | --- |
| Annotation | Description | Example |
| @PreAuthorize | Checks before the method executes | @PreAuthorize("hasRole('ADMIN')") |
| @Secured | Restricts access to a method based on roles | @Secured("ROLE\_USER") |
| @RolesAllowed | Similar to @Secured, but uses Java EE standard | @RolesAllowed({"ROLE\_USER", "ROLE\_ADMIN"}) |

* Example, Using @PreAuthorize

@Service

public class UserService {

@PreAuthorize("hasRole('ADMIN')")

public String getAdminData() {

return "Admin Data";

}

@PreAuthorize is preferred over @Secured because it supports SpEL (Spring Expression Language) for complex conditions.

What is JWT? How does it work?

Answer,
JWT (JSON Web Token) is a stateless authentication mechanism used to secure APIs. It consists of three parts,

1. Header – Algorithm & Token Type (HS256)
2. Payload – User data (username, roles)
3. Signature – Ensures integrity using a secret key

*JWT Authentication Flow*

1. The user logs in with credentials.
2. The server generates a JWT token.
3. The token is sent in the Authorization header (Bearer <token>).
4. On subsequent requests, the server verifies the token instead of checking session data.

Example, Generating JWT Token

public String generateToken(String username) {

return Jwts.builder()

.setSubject(username)

.setIssuedAt(new Date())

.setExpiration(new Date(System.currentTimeMillis()  1000 \* 60 \* 60)) // 1 hour validity

.signWith(SignatureAlgorithm.HS256, secretKey)

.compact();

}

🔹 JWT is preferred for REST APIs because it eliminates session management.

How to disable CSRF in Spring Security?

Answer,
CSRF (Cross-Site Request Forgery) protection is enabled by default in Spring Security.
However, for REST APIs, CSRF can be disabled as they don’t use cookies for authentication.

Example, Disabling CSRF in Spring Security

@Bean

public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {

http

.csrf(csrf -> csrf.disable())

.authorizeHttpRequests(auth -> auth

.requestMatchers("/admin/\*\*").hasAuthority("ROLE\_ADMIN")

.requestMatchers("/user/\*\*").hasAuthority("ROLE\_USER")

.requestMatchers("/", "/home", "/login", "/register").permitAll()

.anyRequest().authenticated()

)

.formLogin(login -> login

.loginPage("/login") // Redirects to this page when login is required

.defaultSuccessUrl("/dashboard", true)

.permitAll()

)

.logout(logout -> logout

.logoutUrl("/logout")

.logoutSuccessUrl("/login")

.permitAll()

)

.exceptionHandling(exception -> exception

.authenticationEntryPoint((request, response, authException) -> {

response.sendRedirect("/login"); // Redirect to login page instead of /error

})

);

return http.build();

}

|  |  |  |
| --- | --- | --- |
| **Scenario** | **CSRF Enabled **✅ | **CSRF Disabled** ❌ |
| Session-based apps (e.g., banking, admin panels) | ✅ Yes | ❌ No |
| REST APIs / Microservices | ❌ No | ✅ Yes |
| JWT authentication | ❌ No | ✅ Yes |
| Mobile Apps | ❌ No | ✅ Yes |

Rule of Thumb, Enable CSRF for form-based login apps and disable it for APIs, JWT, and stateless services.

Spring Security Flow for the Given Configuration

1. User Requests a Page

* If it's a public page (**/home, /login, /register**), it loads normally.
* If it's a secured page (**/admin/\*\***,** /user/\*\***), authentication is checked.

1. Authentication Flow (Login)

* User submits credentials at /login.
* AuthenticationManager uses DaoAuthenticationProvider.
* DaoAuthenticationProvider calls UserService (which implements UserDetailsService) to fetch user details.
* Password is verified using BCryptPasswordEncoder.
* If valid, user details are stored in SecurityContextHolder.
* On success → Redirects to /dashboard, else → Redirects back to /login?error.

1. Authorization Flow

* If a user accesses /admin/\*\*, Spring Security checks for "ROLE\_ADMIN".
* If a user accesses /user/\*\*, it checks for "ROLE\_USER".
* If unauthorized, redirects to /login.

1. Logout Flow

* User clicks logout (/logout).
* Spring Security clears the session and redirects to /login.

1. Exception Handling

* If an unauthenticated user tries accessing a restricted page, they are redirected to /login.

File Handling in Java Spring Framework

Introduction

* File handling in Spring allows us to upload, store, retrieve, and download files using Spring Boot, MultipartFile, and FileSystem or Database.
* Spring provides the MultipartFile interface to handle file uploads.

File Handling Approaches in Spring

There are two common ways to handle files in a Spring application,

1. Store files on the local file system and store metadata (path, name, type) in a database.specially when we are working with large size files use this.
2. Store files directly in a database as binary data (BLOB).

## File Upload in Spring Boot

Spring Boot provides a simple way to upload files using MultipartFile.

✅ Step 1, Enable Multipart Support

Add this configuration in application.properties,

    spring.servlet.multipart.enabled=true
    
    spring.servlet.multipart.max-file-size=5MB
    
    spring.servlet.multipart.max-request-size=10MB
    
    spring.servlet.multipart.file-size-threshold=5KB

✅ Step 2, Create Entity Class

If storing only the file path,

```java
@Entity

@Table(name="filedetails")

@Data

@NoArgsConstructor

@AllArgsConstructor

public class Filedetails {

@Id

@GeneratedValue(strategy = GenerationType.IDENTITY)

private long id;

private String filename;

private String filepath;

private String filetype;

private Long fileSize;
```

If storing the file as binary data,

```java
@Entity

@Data

@AllArgsConstructor

@NoArgsConstructor

@Table(name = "filedata")

public class Filedata {

@Id

@GeneratedValue(strategy = GenerationType.IDENTITY)

private long id;

private String fileName;

private String type;

@Lob

@Column(columnDefinition = "VARBINARY(MAX)")

private byte[] fileData;

✅ Step 3, File Upload Service

If storing the file as binary data,

public String uploadFile(MultipartFile file) throws IOException {

Filedata filedata = new Filedata();

filedata.setFileName(file.getOriginalFilename());

filedata.setType(file.getContentType());

filedata.setFileData(file.getBytes());

fileRepository.save(filedata);

return filedata.getFileName();

}

public Filedata getFileByName(String fileName) {

return fileRepository.findByFileName(fileName).orElse(null);

}

If storing only the file path,

private FileRepository fileRepository;

private static final String UPLOAD\_DIR = "D,\\Test uploads";

static {

if (!new File(UPLOAD\_DIR).exists()) {

new File(UPLOAD\_DIR).mkdir();

}

}

// Upload File and Store Path in Database

public String uploadFile(MultipartFile multipartFile) {

try {

if (multipartFile.isEmpty()) {

return "File is empty. Please select a valid file.";

}

String filePath = Paths.get(UPLOAD\_DIR, multipartFile.getOriginalFilename()).toString();

// automatically detect path

Files.copy(multipartFile.getInputStream(), Paths.get(filePath), StandardCopyOption.REPLACE\_EXISTING);

// Save file details in the database

Filedetails details = new Filedetails();

details.setFilename(multipartFile.getOriginalFilename());

details.setFilepath(filePath);

details.setFiletype(multipartFile.getContentType());

details.setFileSize((multipartFile.getSize()) % 1024);

// Assuming you have a JPA repository

fileRepository.save(details);

return "File uploaded successfully, "  filePath;

} catch (IOException e) {

return "Error storing file, "  e.getMessage();

}

}
```

// Retrieve File Path from Database

```java
public byte[] downloadFile(String filename) {

Optional<Filedetails> foundFile = fileRepository.findByFilename(filename);

if (foundFile.isPresent()) {

String filePath = foundFile.get().getFilepath();

try {

return Files.readAllBytes(Paths.get(filePath));

} catch (Exception e) {

throw new RuntimeException("Error reading file, "  e.getMessage());

}

} else {

throw new RuntimeException("File not found!");

}

}
```

✅ Step 4, File Upload download Controller

If storing the file as binary data,

```java
@PostMapping("/upload")

public ResponseEntity<String> uploadFile(@RequestParam("file") MultipartFile file) {

try {

return ResponseEntity.ok(fileService.uploadFile(file));

} catch (Exception e) {

return ResponseEntity.status(HttpStatus.INTERNAL\_SERVER\_ERROR).body("error occured ");

}

}

@GetMapping("/download/{fileName}")

public ResponseEntity<byte[]> downloadFile(@PathVariable String fileName) {

Filedata fileData = fileService.getFileByName(fileName);

if (fileData == null) {

return ResponseEntity.status(HttpStatus.NOT\_FOUND).body(null);

}

HttpHeaders headers = new HttpHeaders();

headers.setContentType(MediaType.parseMediaType(fileData.getType())); // Set correct content type

headers.setContentDisposition(ContentDisposition.attachment()

.filename(fileData.getFileName(), StandardCharsets.UTF\_8)

.build());

return new ResponseEntity<>(fileData.getFileData(), headers, HttpStatus.OK);

}

```
If storing only the file path,

// Upload File Endpoint

```java
@PostMapping("/upload")

public String uploadFile(@RequestParam("file") MultipartFile file, RedirectAttributes redirectAttributes) {

try {

String msg = fileService.uploadFile(file);

redirectAttributes.addFlashAttribute("msg", msg); // Add flash attribute for success message

return "redirect,/home"; // Redirect to index page

} catch (Exception e) {

redirectAttributes.addFlashAttribute("msg", "Error, "  e.getMessage());

return "redirect,/home"; // Redirect back to index even in case of error

}

}
```

// Download File Endpoint

```java
@GetMapping("/download/{fileName}")

public ResponseEntity<byte[]> downloadFile(@PathVariable String fileName) {

try {

byte[] fileData = fileService.downloadFile(fileName);

HttpHeaders headers = new HttpHeaders();

headers.setContentType(MediaType.APPLICATION\_OCTET\_STREAM);

headers.setContentDisposition(ContentDisposition.attachment().filename(fileName).build());

return new ResponseEntity<>(fileData, headers, HttpStatus.OK);

} catch (RuntimeException e) {

return ResponseEntity.status(HttpStatus.NOT\_FOUND).body(null);

}

}

```
How It Works?

1. Retrieves the file path from the database.
2. Reads the file from the system.
3. Returns the file as a Resource with a Content-Disposition header.

File View in Browser

To allow files (like images, PDFs) to open in a browser instead of downloading,

```java
@GetMapping("/view/{id}")

public ResponseEntity<Resource> viewFile(@PathVariable Long id) {

FileDetails fileDetails = fileService.getFileById(id);

if (fileDetails == null) {

return ResponseEntity.notFound().build();

}

try {

Path path = Paths.get(fileDetails.getFilepath());

Resource resource = new UrlResource(path.toUri());

if (resource.exists() && resource.isReadable()) {

return ResponseEntity.ok()

.contentType(MediaType.parseMediaType(fileDetails.getFiletype()))

.body(resource);

} else {

return ResponseEntity.status(HttpStatus.INTERNAL\_SERVER\_ERROR).build();

}

} catch (Exception e) {

return ResponseEntity.status(HttpStatus.INTERNAL\_SERVER\_ERROR).build();

}

}
```

📌 This method will open PDFs, images, and other supported file types directly in the browser.

Delete File from System and Database

```java
@GetMapping("/delete/{id}")

public String deleteFile(@PathVariable long id, RedirectAttributes redirectAttributes) {

if (fileService.deleteFile(id)) {

redirectAttributes.addFlashAttribute("msg", "File deleted with ID, "  id);

} else {

redirectAttributes.addFlashAttribute("msg", "Failed to delete file with ID, "  id);

}

return "redirect,/home";

}
```

Delete Logic in Service

```java
// delete file from database and direcotry

public boolean deleteFile(Long id) {

Filedetails filetodelete=fileRepository.findById(id).orElse(null);

if(filetodelete==null) {

return false;

}

Path path=Paths.get(filetodelete.getFilepath());

try {

Files.deleteIfExists(path);

fileRepository.delete(filetodelete);

return true;

} catch (Exception e) {

return false;

}

}
```

# JPA Configuration in Spring MVC project


# Two Database Configuration in Spring Boot – Notes

**1. Why Multiple Databases in Spring Boot?**
In real-world applications (banking, audit, reporting): One database for core business data Another database for audit / logs / reports Sometimes read & write databases are separated Spring Boot supports multiple DataSources, but we must configure them manually.

------------


**2. Application Properties Configuration**

Define connection details for each database Each database is identified using a custom prefix

Key Point :
👉 When using multiple databases, do NOT use spring.datasource
👉 Use custom prefixes like datasource.primary, datasource.secondary

Example (`application.properties`)


```yaml
spring.application.name=twodb
server.port=8181

datasource.primary.jdbc-url=jdbc:h2:mem:dbone
datasource.primary.username=one
datasource.primary.password=one
datasource.primary.driverClassName=org.h2.Driver

datasource.secondary.jdbc-url=jdbc:h2:mem:dbtwo
datasource.secondary.username=two
datasource.secondary.password=two
datasource.secondary.driverClassName=org.h2.Driver

spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```



Note : jdbc-url is mandatory when DataSourceBuilder is used @ConfigurationProperties binds these values automatically

------------


**3. DataSource Configuration**

What is DataSource?
Represents database connection pool Holds URL, username, password, driver Why @ConfigurationProperties? Automatically maps properties using prefix Avoids hardcoding credentials Primary DataSource

```java
@Primary
@Bean
@ConfigurationProperties(prefix = "datasource.primary")
public DataSource primaryDataSource() {
    return DataSourceBuilder.create().build();
}
```

Important Annotations Annotation

- @Bean Creates Spring-managed bean 
- @ConfigurationProperties Loads DB properties 
- @Primary Default DataSource if no qualifier is used

------------


**4. EntityManagerFactory Configuration**

What is EntityManagerFactory?
Responsible for:
Managing entities
Creating EntityManager
Handling persistence context
Why Separate EntityManagerFactory?
Each database:
- Has different entities
- Has different persistence unit
- Configuration

```java
@Primary
@Bean
public LocalContainerEntityManagerFactoryBean primaryEntityManagerFactory(
        EntityManagerFactoryBuilder builder) {

    return builder
            .dataSource(primaryDataSource())
            .packages("com.example.twodb.primary.entity")
            .persistenceUnit("primaryPU")
            .build();
}
```


packages() → tells where entity classes are persistenceUnit() → logical name for DB One DB = One EntityManagerFactory

------------


**5. TransactionManager Configuration**

Why TransactionManager?
Handles:
- Commit
- Rollback
- Transaction boundaries

Each database must have:  Its own TransactionManager

```java
@Primary
@Bean
public PlatformTransactionManager primaryTransactionManager(
        @Qualifier("primaryEntityManagerFactory") EntityManagerFactory emf) {

    return new JpaTransactionManager(emf);
}
```

Why @Qualifier?
Multiple EntityManagerFactory beans exist Spring needs to know which one to inject

------------


**6. @EnableJpaRepositories Configuration Why Required?**
When multiple databases exist: Spring cannot auto-detect repositories We must explicitly define: Repository package EntityManagerFactory TransactionManager Configuration


```java
@EnableJpaRepositories(
    basePackages = "com.example.twodb.primary.repo",
    entityManagerFactoryRef = "primaryEntityManagerFactory",
    transactionManagerRef = "primaryTransactionManager"
)
```


Interview Question
What happens if this is not configured? 👉 Spring throws No qualifying bean or wrong DB mapping errors

------------


**7. Complete Primary DB Configuration Class**


```java
@Configuration
@EnableTransactionManagement
@EnableJpaRepositories(
    basePackages = "com.example.twodb.primary.repo",
    entityManagerFactoryRef = "primaryEntityManagerFactory",
    transactionManagerRef = "primaryTransactionManager"
)
public class UserDbConfig {

    @Primary
    @Bean
    @ConfigurationProperties(prefix = "datasource.primary")
    public DataSource primaryDataSource() {
        return DataSourceBuilder.create().build();
    }

    @Primary
    @Bean
    public LocalContainerEntityManagerFactoryBean primaryEntityManagerFactory(
            EntityManagerFactoryBuilder builder) {

        return builder
                .dataSource(primaryDataSource())
                .packages("com.example.twodb.primary.entity")
                .persistenceUnit("primaryPU")
                .build();
    }

    @Primary
    @Bean
    public PlatformTransactionManager primaryTransactionManager(
            @Qualifier("primaryEntityManagerFactory") EntityManagerFactory emf) {

        return new JpaTransactionManager(emf);
    }
}
```


------------


**8. Secondary Database Configuration**
Key Differences No @Primary Different: Property prefix Entity package Repository package Persistence unit


```java
@Configuration
@EnableTransactionManagement
@EnableJpaRepositories(
    basePackages = "com.example.twodb.secondary.repo",
    entityManagerFactoryRef = "secondaryEntityManagerFactory",
    transactionManagerRef = "secondaryTransactionManager"
)
public class AddressDbConfig {

    @Bean
    @ConfigurationProperties(prefix = "datasource.secondary")
    public DataSource secondaryDataSource() {
        return DataSourceBuilder.create().build();
    }

    @Bean
    public LocalContainerEntityManagerFactoryBean secondaryEntityManagerFactory(
            EntityManagerFactoryBuilder builder) {

        return builder
                .dataSource(secondaryDataSource())
                .packages("com.example.twodb.secondary.entity")
                .persistenceUnit("secondaryPU")
                .build();
    }

    @Bean
    public PlatformTransactionManager secondaryTransactionManager(
            @Qualifier("secondaryEntityManagerFactory") EntityManagerFactory emf) {

        return new JpaTransactionManager(emf);
    }
}
```

------------


**9. Package Structure (Best Practice)**

com.example.twodb
 ├── primary
 │   ├── entity
 │   ├── repo
 │   └── config
 ├── secondary
 │   ├── entity
 │   ├── repo
 │   └── config

