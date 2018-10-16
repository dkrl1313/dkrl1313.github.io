---

layout: post title: [iOS Swift입문] Class

tags: [Swift]
-------------

### Class

1.	데이터 모델의 주요한 구성요소
2.	오브젝트를 생성
3.	참조로 동작

##### - 페이스북

1.	https://developers.facebook.com/ 이동
2.	[페이스북 클라이언트 ID 생성 참고](https://dreamyoungs.github.io/tip/facebook-login-connect)

### 2. [ pom.xml ] dependency 추가

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
    <version>1.4.1.RELEASE</version>
</dependency>
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-oauth2-client</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-oauth2-jose</artifactId>
</dependency>
```

### 3. [application.properties] 파일에 클라이언트 ID, 비밀번호 입력

##### - 구글

```
spring.security.oauth2.client.registration.google.client-id=
spring.security.oauth2.client.registration.google.client-secret=
```

##### - 페이스북

```
spring.security.oauth2.client.registration.facebook.client-id=
spring.security.oauth2.client.registration.facebook.client-secret=
```

### 4. [WebSecurityConfiguration.java]

```
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

@Configuration
public class WebSecurityConfiguration extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
                .anyRequest().authenticated()
                .and()
                .oauth2Login();

        http.logout()
                .invalidateHttpSession(true)
                .logoutUrl("/logout")
                .deleteCookies("JSESSIONID","SPRING_SECURITY_REMEMBER_ME_COOKIE")
                .logoutSuccessUrl("/");
    }
}
```

[참고 : Overriding Spring Boot 2.0 Auto-configuration](https://docs.spring.io/spring-security/site/docs/current/reference/html/jc.html)
