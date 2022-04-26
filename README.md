# SpringBoot Codebase

스프링부트 코드베이스

Tech Stack
```
Spring Data JPA
Spring Security
JWT
MySQL
Swagger2
Docker
```

## How to Use

- docker-compose.yml을 수정해주세요
  - DB 관련 Secrert 값 수정
  - 경로 및 포트 수정
      ```yaml
      version: '3.8'
    
      services:
        backend:
          image: backend:latest
          ports:
            - 8080:8080
          depends_on:
            - mysql
    
        mysql:
          image: library/mysql:5.7
          platform: linux/bamd64
          volumes:
            - db_datas:/var/lib/mysql
          environment:
            - MYSQL_DATABASE=**디비이름**
            - MYSQL_ROOT_HOST='%'
            - MYSQL_ROOT_PASSWORD=**비밀번호**
            - TZ= Asia/Seoul
          ports:
            - 13306:3306
    
      volumes:
        db_datas:
    
      ```
- application-jwt.yml을 수정해주세요
  ```yaml
  jwt:
  header: Authorization
  secret : '시크릿값'
  token-validity-in-seconds : 3600
    ```

- application-mysql.yml을 수정해주세요
    ```yaml
    spring:
      datasource:
        username: root
        password: **비밀번호**
        url: jdbc:mysql://localhost:13306/**디비이름**?allowPublicKeyRetrieval=true&useSSL=false
      jpa:
        hibernate:
          ddl-auto: create-drop
        properties:
          hibernate:
            show_sql: true
            format_sql: true
        defer-datasource-initialization: true
      sql:
        init:
          schema-locations:
          data-locations: classpath:sql/data.sql
          mode: ALWAYS
    
    ```