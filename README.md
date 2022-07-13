# Intellij IDEA LiveTemplates

These are my custom [IntelliJ IDEA Live Templates](https://www.jetbrains.com/help/idea/using-live-templates.html) for Java that I am currently using.

## Export and Import

You can import LiveTemplates by File -> Manage IDE Settings -> Import Settings -> Select settings.zip

You can export LiveTemplates by File -> Manage IDE Settings -> Export Settings -> Select Live Templates -> Ok

## Java

1. `logger` - Adds SLF4J Logger

```java
private static final org.slf4j.Logger logger = org.slf4j.LoggerFactory.getLogger($CLASS$.class);
```

## JPA

1. `jpa-entity` - JPA Entity

```java
@javax.persistence.Entity
class $entity$ {

    @javax.persistence.Id
    @javax.persistence.GeneratedValue
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
@javax.persistence.Entity
class $name$ {
    @javax.persistence.Id
    @javax.persistence.GeneratedValue
    private Long id;
    private String name;
}
```

3. `jpa-entity-id-seq` - JPA Entity Id of Sequence Generator Type

```java
@javax.persistence.Id
@javax.persistence.GeneratedValue(strategy = javax.persistence.GenerationType.SEQUENCE, generator = "$table$_id_generator")
@javax.persistence.SequenceGenerator(name = "$table$_id_generator", sequenceName = "$table$_id_seq", allocationSize = 50)
private Long id;
```

4. `jpa-many-to-many` - JPA Entity property of ManyToMany Type

```java
@javax.persistence.ManyToMany(cascade = {javax.persistence.CascadeType.PERSIST, javax.persistence.CascadeType.MERGE})
@javax.persistence.JoinTable(
        name = "$join_table_name$",
        joinColumns = {@javax.persistence.JoinColumn(name = "$id_column$", referencedColumnName = "$id_ref_column$")},
        inverseJoinColumns = {@javax.persistence.JoinColumn(name =  "$id_join_column$", referencedColumnName =  "$id_ref_join_column$")})
private Set<$CLASS$> $name$;

```

## SpringBoot

1. `boot-controller` - SpringMVC REST Controller

```java
@org.springframework.web.bind.annotation.RestController
@org.springframework.web.bind.annotation.RequestMapping("/api")
@lombok.RequiredArgsConstructor
@lombok.extern.slf4j.Slf4j
class $CLASS$ {
    
}
```

2. `boot-service` - SpringBoot Service

```java
@org.springframework.stereotype.Service
@org.springframework.transaction.annotation.Transactional
@lombok.RequiredArgsConstructor
@lombok.extern.slf4j.Slf4j
public class $CLASS$ {

}
```

3. `boot-app-properties` - SpringBoot ApplicationProperties binding class

```java
@org.springframework.boot.context.properties.ConfigurationProperties(prefix = "$prefix$")
@lombok.Data
public class ApplicationProperties {
    
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
    org.springframework.test.web.servlet.request.MockHttpServletRequestBuilder request = org.springframework.test.web.servlet.request.MockMvcRequestBuilders
            .get("")
            .contentType(org.springframework.http.MediaType.APPLICATION_JSON);

    mockMvc.perform(request)
            .andExpect(org.springframework.test.web.servlet.result.MockMvcResultMatchers.status().isOk())
            .andExpect(org.springframework.test.web.servlet.result.MockMvcResultMatchers.content().contentType(org.springframework.http.MediaType.APPLICATION_JSON))
            .andExpect(org.springframework.test.web.servlet.result.MockMvcResultMatchers.jsonPath("", org.hamcrest.Matchers.is("")));
}
```

## SQL

1. `flyway-table` - Flyway table creation script

```sql
create sequence $table$_id_seq start with 1 increment by 50;

create table $table$ (
    id bigint DEFAULT nextval('$table$_id_seq') not null,
    created_at timestamp,
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
    <version>3.2.1</version>
    <configuration>
        <from>
            <image>eclipse-temurin:17-jre-focal</image>
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

2. `git-commit-id-plugin` - Adds git-commit-id-plugin

```xml
<plugin>
    <groupId>pl.project13.maven</groupId>
    <artifactId>git-commit-id-plugin</artifactId>
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
    <version>2.17.4</version>
    <configuration>
        <java>
            <googleJavaFormat>
                <version>1.12.0</version>
                <style>AOSP</style>
            </googleJavaFormat>
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
    <version>1.12.0</version>
    <configuration>
        <workingDirectory>${project.basedir}/../frontend</workingDirectory>
        <nodeVersion>v14.15.3</nodeVersion>
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
    <version>1.12.0</version>
    <executions>
        <execution>
            <id>install node and yarn</id>
            <goals>
                <goal>install-node-and-yarn</goal>
            </goals>
            <configuration>
                <workingDirectory>${project.basedir}/../frontend</workingDirectory>
                <nodeVersion>v14.15.3</nodeVersion>
                <yarnVersion>v1.19.2</yarnVersion>
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
    <version>2.6</version>
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
