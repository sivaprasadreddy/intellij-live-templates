# Intellij IDEA LiveTemplates

These are my custom [IntelliJ IDEA Live Templates](https://www.jetbrains.com/help/idea/using-live-templates.html) for Java that I am currently using.

## Export and Import

You can import LiveTemplates by File -> Manage IDE Settings -> Import Settings -> Select settings.zip

You can export LiveTemplates by File -> Manage IDE Settings -> Export Settings -> Select Live Templates -> Ok

## Java

1. `log` - Adds SLF4J Logger

```java
private static final org.slf4j.Logger log = org.slf4j.LoggerFactory.getLogger($CLASS$.class);
```

## JPA

1. `jpa-entity` - JPA Entity

```java
@jakarta.persistence.Entity
class $entity$ {

    @jakarta.persistence.Id
    @jakarta.persistence.GeneratedValue
    private java.lang.Long id;
    private java.lang.String name;

    public $entity$() {}

    public $entity$(String name) {
        this.name = name;
    }

    public java.lang.Long getId() {
        return id;
    }

    public void setId(java.lang.Long id) {
        this.id = id;
    }

    public java.lang.String getName() {
        return name;
    }

    public void setName(java.lang.String name) {
        this.name = name;
    }

    @java.lang.Override
    public java.lang.String toString() {
        return "$entity${" +
                "id=" + id +
                ", name='" + name + '\'' +
                '}';
    }
}
```

2. `jpa-entity-lombok` - JPA Entity with Lombok

```java
@lombok.Setter
@lombok.Getter
@lombok.AllArgsConstructor
@lombok.NoArgsConstructor
@jakarta.persistence.Entity
class $name$ {
    @jakarta.persistence.Id
    @jakarta.persistence.GeneratedValue
    private Long id;
    private String name;
}
```

3. `jpa-entity-id-seq` - JPA Entity Id of Sequence Generator Type

```java
@jakarta.persistence.Id
@jakarta.persistence.GeneratedValue(strategy = jakarta.persistence.GenerationType.SEQUENCE, generator = "$table$_id_generator")
@jakarta.persistence.SequenceGenerator(name = "$table$_id_generator", sequenceName = "$table$_id_seq", allocationSize = 50)
private Long id;
```

4. `jpa-many-to-many` - JPA Entity property of ManyToMany Type

```java
@jakarta.persistence.ManyToMany(cascade = {jakarta.persistence.CascadeType.PERSIST, jakarta.persistence.CascadeType.MERGE})
@jakarta.persistence.JoinTable(
        name = "$join_table_name$",
        joinColumns = {@jakarta.persistence.JoinColumn(name = "$id_column$", referencedColumnName = "$id_ref_column$")},
        inverseJoinColumns = {@jakarta.persistence.JoinColumn(name =  "$id_join_column$", referencedColumnName =  "$id_ref_join_column$")})
private Set<$CLASS$> $name$;

```

## SpringBoot

1. `boot-controller` - SpringMVC REST Controller

```java
@org.springframework.web.bind.annotation.RestController
@org.springframework.web.bind.annotation.RequestMapping("/api")
class $CLASS$ {
    
}
```

2. `boot-service` - SpringBoot Service

```java
@org.springframework.stereotype.Service
@org.springframework.transaction.annotation.Transactional(readOnly=true)
public class $CLASS$ {

}
```

3. `boot-app-properties` - SpringBoot ApplicationProperties binding class

```java
@org.springframework.boot.context.properties.ConfigurationProperties(prefix = "$prefix$")
public class $CLASS$ {
    
}
```

4. `boot-clr` - SpringBoot CommandLineRunner

```java
@org.springframework.stereotype.Component
public class $CLASS$ implements org.springframework.boot.CommandLineRunner {
    
    @Override
    public void run(String... args) throws Exception {
        
    }
}
```

5. `boot-add-cors-mappings` - SpringBoot WebMvcConfig addCorsMappings

```java
@Override
public void addCorsMappings(org.springframework.web.servlet.config.annotation.CorsRegistry registry) {
    registry.addMapping("/api/**")
            .allowedMethods("*")
            .allowedHeaders("*")
            .allowedOriginPatterns("*")
            .allowCredentials(true);
}
```

6. `boot-cors-filter` - SpringBoot CORS Filter

```java
@org.springframework.context.annotation.Bean
public org.springframework.boot.web.servlet.FilterRegistrationBean simpleCorsFilter() {
    org.springframework.web.cors.UrlBasedCorsConfigurationSource source = new org.springframework.web.cors.UrlBasedCorsConfigurationSource();
    org.springframework.web.cors.CorsConfiguration config = new org.springframework.web.cors.CorsConfiguration();
    config.setAllowCredentials(true);
    config.setAllowedOrigins(java.util.Collections.singletonList("http://localhost:4200"));
    config.setAllowedMethods(java.util.Collections.singletonList("*"));
    config.setAllowedHeaders(java.util.Collections.singletonList("*"));
    source.registerCorsConfiguration("/**", config);
    org.springframework.boot.web.servlet.FilterRegistrationBean bean = new org.springframework.boot.web.servlet.FilterRegistrationBean(new org.springframework.web.filter.CorsFilter(source));
    bean.setOrder(org.springframework.core.Ordered.HIGHEST_PRECEDENCE);
    return bean;
}
```

7. `boot-open-api-config` - SpringBoot OpenAPI Configuration

```java
import io.swagger.v3.oas.models.ExternalDocumentation;
import io.swagger.v3.oas.models.OpenAPI;
import io.swagger.v3.oas.models.info.Info;
import io.swagger.v3.oas.models.info.License;
import io.swagger.v3.oas.models.security.SecurityScheme;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class $CLASS$ {
    @Bean
    public io.swagger.v3.oas.models.OpenAPI springShopOpenAPI() {
        return new io.swagger.v3.oas.models.OpenAPI()
            .info(info())
            .externalDocs(externalDocumentation())
            .schemaRequirement("bearerAuth", jwtSecurityScheme())
        ;
    }

    private io.swagger.v3.oas.models.info.Info info() {
        return new io.swagger.v3.oas.models.info.Info()
            .title("API Title")
            .description("API description")
            .version("v0.0.1")
            .license(new io.swagger.v3.oas.models.info.License().name("MIT"));
    }

    private io.swagger.v3.oas.models.ExternalDocumentation externalDocumentation() {
        return new io.swagger.v3.oas.models.ExternalDocumentation()
            .description("API Documentation")
            .url("https://github.com/user/repo/README.md");
    }

    private io.swagger.v3.oas.models.security.SecurityScheme jwtSecurityScheme() {
        io.swagger.v3.oas.models.security.SecurityScheme scheme = new io.swagger.v3.oas.models.security.SecurityScheme();
        scheme.setName("bearerAuth");
        scheme.setType(io.swagger.v3.oas.models.security.SecurityScheme.Type.HTTP);
        scheme.setScheme("bearer");
        scheme.setBearerFormat("JWT");
        return scheme;
    }
}
```

8. `boot-mvc-test` - SpringMVC Test method

```java
@org.springframework.beans.factory.annotation.Autowired
private org.springframework.test.web.servlet.MockMvc mockMvc;

@org.junit.jupiter.api.Test
void test$Function$() throws java.lang.Exception {
    var request = org.springframework.test.web.servlet.request.MockMvcRequestBuilders
            .post("")
            .contentType(org.springframework.http.MediaType.APPLICATION_JSON);

    mockMvc.perform(request)
            .andExpect(org.springframework.test.web.servlet.result.MockMvcResultMatchers.status().isCreated())
            .andExpect(org.springframework.test.web.servlet.result.MockMvcResultMatchers.content().contentType(org.springframework.http.MediaType.APPLICATION_JSON))
            .andExpect(org.springframework.test.web.servlet.result.MockMvcResultMatchers.jsonPath("", org.hamcrest.Matchers.is("")));
}
```

9. `boot-dynamic-property-registrar` - Spring Boot DynamicPropertyRegistrar

```java
@org.springframework.context.annotation.Bean
org.springframework.test.context.DynamicPropertyRegistrar dynamicPropertyRegistrar() {
    return (registry) -> {
        registry.add("", "");
    };
}
```

10. `boot-datasource-jpa-properties` - Spring Boot DataSource and JPA Properties

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/postgres
spring.datasource.username=postgres
spring.datasource.password=postgres
spring.jpa.open-in-view=false
spring.jpa.hibernate.ddl-auto=validate
spring.jpa.show-sql=true
#spring.jpa.properties.hibernate.format_sql=true
```

## Testcontainers

1. `tc-magic-jdbc-url` - Spring Boot TestPropertySource with Testcontainers magic JDBC URL

```java
@org.springframework.test.context.TestPropertySource(properties = {
        "spring.test.database.replace=none",
        "spring.datasource.url=jdbc:tc:postgresql:17-alpine:///db"
})
```

2. `tc-postgres` - PostgreSQLContainer

```java
@org.testcontainers.junit.jupiter.Container
static org.testcontainers.containers.PostgreSQLContainer<?> postgres =
        new org.testcontainers.containers.PostgreSQLContainer<>("postgres:17-alpine");
```

## SQL

1. `flyway-table` - Flyway table creation script

```sql
create sequence $table$_id_seq start with 1 increment by 50;

create table $table$ (
    id bigint not null default nextval('$table$_id_seq'),
    created_at timestamp not null default now(),
    updated_at timestamp,
    primary key (id)
);
```

## Maven

1. `jib-maven-plugin` - Add Jib Maven Plugin

```xml
<plugin>
    <groupId>com.google.cloud.tools</groupId>
    <artifactId>jib-maven-plugin</artifactId>
    <version>3.3.4</version>
    <configuration>
        <from>
            <image>eclipse-temurin:21-jre</image>
        </from>
        <to>
            <image>sivaprasadreddy/${project.artifactId}</image>
            <tags>
                <tag>latest</tag>
                <tag>${project.version}</tag>
            </tags>
        </to>
        <container>
            <ports>
                <port>8080</port>
            </ports>
        </container>
    </configuration>
</plugin>
```

2. `git-commit-id-maven-plugin` - Adds git-commit-id-maven-plugin

```xml
<plugin>
    <groupId>io.github.git-commit-id</groupId>
    <artifactId>git-commit-id-maven-plugin</artifactId>
    <executions>
        <execution>
            <goals>
                <goal>revision</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <failOnNoGitDirectory>false</failOnNoGitDirectory>
        <failOnUnableToExtractRepoInfo>false</failOnUnableToExtractRepoInfo>
        <generateGitPropertiesFile>true</generateGitPropertiesFile>
        <includeOnlyProperties>
            <includeOnlyProperty>^git.branch$</includeOnlyProperty>
            <includeOnlyProperty>^git.commit.id.abbrev$</includeOnlyProperty>
            <includeOnlyProperty>^git.commit.user.name$</includeOnlyProperty>
            <includeOnlyProperty>^git.commit.message.full$</includeOnlyProperty>
        </includeOnlyProperties>
    </configuration>
</plugin>
```

3. `spotless-maven-plugin` - Adds spotless-maven-plugin

```xml
<plugin>
    <groupId>com.diffplug.spotless</groupId>
    <artifactId>spotless-maven-plugin</artifactId>
    <version>2.44.2</version>
    <configuration>
        <java>
            <importOrder />
            <removeUnusedImports />
            <palantirJavaFormat>
                <version>2.50.0</version>
            </palantirJavaFormat>
            <formatAnnotations />
        </java>
    </configuration>
    <executions>
        <execution>
            <phase>compile</phase>
            <goals>
                <goal>check</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

4. `frontend-maven-plugin-npm` - Adds frontend-maven-plugin with NPM

```xml
<plugin>
    <groupId>com.github.eirslett</groupId>
    <artifactId>frontend-maven-plugin</artifactId>
    <version>1.15.1</version>
    <configuration>
        <workingDirectory>${project.basedir}/../frontend</workingDirectory>
        <nodeVersion>v20.14.0</nodeVersion>
    </configuration>
    <executions>
        <execution>
            <id>install node and npm</id>
            <goals>
                <goal>install-node-and-npm</goal>
            </goals>
            <phase>generate-resources</phase>
        </execution>
        <execution>
            <id>npm install</id>
            <goals>
                <goal>npm</goal>
            </goals>
            <phase>generate-resources</phase>
            <configuration>
                <arguments>install</arguments>
            </configuration>
        </execution>
        <execution>
            <id>npm build</id>
            <goals>
                <goal>npm</goal>
            </goals>
            <phase>generate-resources</phase>
            <configuration>
                <environmentVariables>
                    <CI>true</CI>
                </environmentVariables>
                <arguments>run build</arguments>
            </configuration>
        </execution>
    </executions>
</plugin>
```

5. `frontend-maven-plugin-yarn` - Adds frontend-maven-plugin with YARN

```xml
<plugin>
    <groupId>com.github.eirslett</groupId>
    <artifactId>frontend-maven-plugin</artifactId>
    <version>1.15.1</version>
    <executions>
        <execution>
            <id>install node and yarn</id>
            <goals>
                <goal>install-node-and-yarn</goal>
            </goals>
            <configuration>
                <workingDirectory>${project.basedir}/../frontend</workingDirectory>
                <nodeVersion>v20.14.0</nodeVersion>
                <yarnVersion>v1.22.22</yarnVersion>
            </configuration>
        </execution>
        <execution>
            <id>yarn install</id>
            <goals>
                <goal>yarn</goal>
            </goals>
            <phase>generate-resources</phase>
            <configuration>
                <arguments>install</arguments>
            </configuration>
        </execution>
        <execution>
            <id>yarn run build</id>
            <goals>
                <goal>yarn</goal>
            </goals>
            <configuration>
                <arguments>run build</arguments>
            </configuration>
        </execution>
    </executions>
</plugin>
```

6. `maven-resources-plugin` - Adds maven-resources-plugin

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-resources-plugin</artifactId>
    <version>3.3.1</version>
    <executions>
        <execution>
            <id>Copy UI build content to public</id>
            <phase>generate-resources</phase>
            <goals>
                <goal>copy-resources</goal>
            </goals>
            <configuration>
                <outputDirectory>${project.build.directory}/classes/public</outputDirectory>
                <overwrite>true</overwrite>
                <resources>
                    <resource>
                        <directory>${project.basedir}/../frontend/build</directory>
                    </resource>
                </resources>
            </configuration>
        </execution>
    </executions>
</plugin>
```

## Docker

1. `boot-Dockerfile` - Creates multistage Dockerfile for Spring Boot application

```
# the first stage of our build will extract the layers
FROM eclipse-temurin:21-jre as builder
WORKDIR application
ARG JAR_FILE=target/*.jar
#ARG JAR_FILE=build/libs/*.jar
COPY ${JAR_FILE} application.jar
RUN java -Djarmode=layertools -jar application.jar extract

# the second stage of our build will copy the extracted layers
FROM eclipse-temurin:21-jre
WORKDIR application
COPY --from=builder application/dependencies/ ./
COPY --from=builder application/spring-boot-loader/ ./
COPY --from=builder application/snapshot-dependencies/ ./
COPY --from=builder application/application/ ./
ENTRYPOINT ["java", "org.springframework.boot.loader.launch.JarLauncher"]
```