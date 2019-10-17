@REM  => Comment
---------------------------------------------
SETLOCAL

Set options to control the visibility of environment variables in a batch file.
Syntax
      SETLOCAL

      SETLOCAL {EnableDelayedExpansion | DisableDelayedExpansion}  {EnableExtensions | DisableExtensions}

Key
   EnableDelayedExpansion  Expand variables at execution time rather than at parse time.

   DisableDelayedExpansion Expand variables at parse time rather than at execution time.

   EnableExtensions        Attempt to enable Command extensions. 

   DisableExtensions       Attempt to disable Command extensions. 

-----------------------------------------------
Bash scripting ..

Like fi for if and done for for, esac is the required way to end a case statement.

-----------------------------------------------

A symlink or a Symbolic Link is simply enough a shortcut to another file. It is a file that points to another file.

ln -s target_path link_path

ln -s ~/Desktop/rad_folder ~/Desktop/awesome_link

cd ~/Desktop/awesome_link

-----------------------------------------------

Maven wrapper : https://www.baeldung.com/maven-wrapper & https://github.com/takari/maven-wrapper

These files are from Maven wrapper. It works similarly to the Gradle wrapper.

This allows you to run the Maven project without having Maven installed and present on the path. It downloads the correct Maven version if it's not found (as far as I know by default in your user home directory).

To create or update all necessary Maven Wrapper files execute the following command:

mvn -N io.takari:maven:wrapper
To use a different version of maven you can specify the version as follows:

mvn -N io.takari:maven:wrapper -Dmaven=3.3.3
Both commands require maven on PATH (add the path to maven bin to Path on System Variables) if you already have mvnw in your project you can use ./mvnw instead of mvn in the commands.

-----------------------------------------------

Filter SuppressionFilter rejects audit events for Check violations according to a suppressions XML document in a file. If there is no configured suppressions file or the optional is set to true and suppressions file was not found the Filter accepts all audit events.

A suppressions XML document contains a set of suppress elements, where each suppress element can have the following attributes:

files - a Regular Expression matched against the file name associated with an audit event. It is optional.
checks - a Regular Expression matched against the name of the check associated with an audit event. Optional as long as id or message is specified.
message - a Regular Expression matched against the message of the check associated with an audit event. Optional as long as checks or id is specified.
id - a string matched against the check id associated with an audit event. Optional as long as checks or message is specified.
lines - a comma-separated list of values, where each value is an integer or a range of integers denoted by integer-integer. It is optional.
columns - a comma-separated list of values, where each value is an integer or a range of integers denoted by integer-integer. It is optional.

-----------------------------------------------

editorconfig => https://medium.com/@edvinsantonovs/why-development-teams-should-use-editorconfig-f58011b1cc56

https://editorconfig.org/

EditorConfig helps developers define and maintain consistent coding styles between different editors and IDEs. The EditorConfig project consists of a file format for defining coding styles and a collection of text editor plugins that enable editors to read the file format and adhere to defined styles.

-----------------------------------------------

The glassfish-web.xml file configures a web application (WAR file). The element hierarchy is as follows:

-----------------------------------------------

Cargo is a thin wrapper that allows you to manipulate various type of application containers (Java EE and others) in a standard way.

Cargo provides the following APIs and tools:

A Java API to start/stop/configure any of the supported containers.
A Java API to (remotely or locally) deploy modules into these containers, be it a server alone, a farm or a cluster.
A Java API to parse/create/merge J2EE modules.
ANT tasks wrapping the Java API for configuring, starting, stopping and deploying applications to all supported containers.
A Web interface that wraps the Java API that can be used to configure, start and stop all containers supported by Cargo remotely and at any time.
Maven2/Maven3 plugins wrapping the Java API for configuring, starting, stopping and deploying applications to all supported containers as well as parsing, creating and merging J2EE modules.
These tools and APIs can be used in a standalone fashion or via various IDEs.


-----------------------------------------------

org.springframework.boot.test.web.client.TestRestTemplate
Convenient alternative of RestTemplate that is suitable for integration tests. 

Note: To prevent injection problems this class intentionally does not extend RestTemplate. If you need access to the underlying RestTemplate use getRestTemplate().

If you are using the @SpringBootTest annotation, a TestRestTemplate is automatically available and can be @Autowired into your test. If you need customizations (for example to adding additional message converters) use a RestTemplateBuilder @Bean.


public org.springframework.web.client.RestTemplate getRestTemplate()
Returns the underlying RestTemplate that is actually used to perform the REST operations.

 RequestEntity request = RequestEntity.post(new URI("https://example.com/foo")).accept(MediaType.APPLICATION_JSON).body(body);
 ResponseEntity<MyResponse> response = template.exchange(request, MyResponse.class);

HTTP Req

TestRestTemplate testRestTemplate = new TestRestTemplate();
ResponseEntity<String> response = testRestTemplate.
  getForEntity(FOO_RESOURCE_URL + "/1", String.class);
  
assertThat(response.getStatusCode(), equalTo(HttpStatus.OK));

TestRestTemplate provides a constructor with which we can create a template with specified credentials for basic authentication.

TestRestTemplate testRestTemplate = new TestRestTemplate("user", "passwd");
ResponseEntity<String> response = testRestTemplate.getForEntity(URL_SECURED_BY_AUTHENTICATION, String.class);
  
assertThat(response.getStatusCode(), equalTo(HttpStatus.OK));

-----------------------------------------------

TestRestTemplate can work as a wrapper for RestTemplate, e.g. if we are forced to use it because we are dealing with legacy code. You can see below how to create such a simple wrapper:

RestTemplateBuilder restTemplateBuilder = new RestTemplateBuilder();
restTemplateBuilder.configure(restTemplate);
TestRestTemplate testRestTemplate = new TestRestTemplate(restTemplateBuilder);
ResponseEntity<String> response = testRestTemplate.getForEntity(FOO_RESOURCE_URL + "/1", String.class);
assertThat(response.getStatusCode(), equalTo(HttpStatus.OK));

-----------------------------------------------

TestRestTemplate is not an extension of RestTemplate, but rather an alternative that simplifies integration testing and facilitates authentication during tests. It helps in customization of Apache HTTP client, but also it can be used as a wrapper of RestTemplate.

-----------------------------------------------

Integration Testing with the Maven Cargo plugin

A very common need in the lifecycle of a project is setting up integration testing. Luckily, Maven has built-in support for this exact scenario, with the following phases of the default build lifecycle (from the Maven documentation):

pre-integration-test: Perform actions required before integration tests are executed. This may involve things such as setting up the required environment.

integration-test: Process and deploy the package if necessary into an environment where integration tests can be run.

post-integration-test: Perform actions required after integration tests have been executed. This may including cleaning up the environment.

In order for the package maven phase to generate a deployable war file, the packaging of the project must be: <packaging>war</packaging>.


-----------------------------------------------

pre-clean	execute processes needed prior to the actual project cleaning
clean	remove all files generated by the previous build
post-clean	execute processes needed to finalize the project cleaning

-----------------------------------------------

SpringBootServletInitializer

Extending the SpringBootServletInitializer class also allows us to configure our application when it's run by the servlet container, by overriding the configure() method.

Now, if we package our application as a WAR, we'll be able to deploy it on any web container in a traditional way, which will also execute the logic we added in the configure() method.

If we want to package it as a JAR file, then we'll need to add the same logic to the main() method so that the embedded container can pick it up as well.

-----------------------------------------------

Configuration properties - Spring boot


We use @Configuration so that Spring creates a Spring bean in the application context.

We also use @PropertySource to define the location of our properties file. Otherwise, Spring uses the default location (classpath:application.properties).

@ConfigurationProperties works best with hierarchical properties that all have the same prefix. So we add a prefix of mail.

The Spring framework uses standard Java bean setters, so it is essential that we declare setters for each of the properties.

Note: If we don't use @Configuration in the POJO, then we need to add @EnableConfigurationProperties(ConfigProperties.class) in the main Spring application class to bind the properties into the POJO:



@Configuration
@PropertySource("classpath:configprops.properties")
@ConfigurationProperties(prefix = "mail")
public class ConfigProperties {
     
    private String hostName;
    private int port;
    private String from;
 
    // standard getters and setters
}

@SpringBootApplication
@EnableConfigurationProperties(ConfigProperties.class)
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}

#Simple properties
mail.hostname=host@mail.com
mail.port=9000
mail.from=mailer@mail.com

Nested properties 

public class Credentials {
    private String authMethod;
    private String username;
    private String password;
 
    // standard getters and setters
}

public class ConfigProperties {
 
    private List<String> defaultRecipients;
    private Map<String, String> additionalHeaders;
    private Credentials credentials;
  
    // standard getters and setters
}

mail.credentials.username=john
mail.credentials.password=password
mail.credentials.authMethod=SHA1

We have explored the @ConfigurationProperties annotation and saw some of the handy features it provides like relaxed binding and Bean Validation.

-----------------------------------------------

Spring Boot jars are shipped with meta-data files that provide details of all supported configuration properties. The files are designed to allow IDE developers to offer contextual help and “code completion” as users are working with application.properies or application.yml files.

The majority of the meta-data file is generated automatically at compile time by processing all items annotated with @ConfigurationProperties.


-----------------------------------------------

public class WebServerPortFileWriter
extends Object
implements org.springframework.context.ApplicationListener<WebServerInitializedEvent>

An ApplicationListener that saves embedded server port and management port into file. This application listener will be triggered whenever the server starts, and the file name can be overridden at runtime with a System property or environment variable named "PORTFILE" or "portfile".

-----------------------------------------------

-----------------------------------------------

-----------------------------------------------
