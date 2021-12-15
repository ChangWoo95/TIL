#JPA

## 어노테이션

### @Entity
- 선언한 클래스를 테이블과 매핑한다고 JPA에 알려주는 어노테이션
- 이렇게 @Entity가 사용된 클래스

### @Table
- 엔티티 클래스에 매핑할 테이블 정보를 알려줌
- name 속성을 이용해 엔티티(클래스)를 테이블로 매핑한다, 생략 시, 클래스 이름을 테이블 이름으로 매핑함

### @Id
- 엔티티 클래스의 필드를 테이블의 기본 키에 매핑

### @Column
- 필드를 컬럼에 매핑


## JPA 표준 속성
- javax.persistence.jdbc.driver: JDBC 드라이버
- javax.persistence.jdbc.user: 데이터베이스 접속 아이디
- javax.persistence.jdbc.password: 데이터베이스 접속 비밀번호
- javax.persistence.jdbc.url: 데이터베이스 접속 URL

## 하이버네이트 속성
- hibernate.dialect: 데이터베이스 방언(Dialect) 설정
- 방언: JPA는 특정 데이터베이스에 종속적이지 않기 위해 제작한 표준 문법을 설정해주는 것
- hibernate.show_sql: 하이버네이트가 실행한 SQL을 출력
- hibernate.format_sql: 하이버네이트가 실행한 SQL을 출력할 때 보기 쉽게 정렬
- hibernate.use_sql_comments: 쿼리를 출력할 때 주석도 함께 출력
- hibernate.id.new_generator_mappings: JPA 표준에 맞춘 새로운 키 생성 전략을 사용

## 생성 주기
1. persistence.xml의 설정 정보를 이용해 엔티티 매니저 팩토리를 생성 
```java
    EntityManagerFactory emf = Persistence.createEntityManagerFactory(name);
```
JPA를 동작시킬 객체와 구현체에 따라 connection pool도 만들어줌 -> **따라서 애플리케이션 전체에서 딱 한 번만 생성하고 공유해서 사용해야함!**

2. 엔티티 매니저 생성
```java
     EntityManager em = emf.createEntityManager();
```
- 엔티티 매니저 팩토리가 엔티티 매니저를 생성한다. 
- JPA의 기능 대부분은 엔티티 매니저가 제공(ex. 엔티티 메니저를 통해 등록/수정/삭제/조회)

3. 종료
```java
  em.close(); // 엔티티 매니저 종료
  emf.close(); // 엔티티 매니저 팩토리 종료
```

### JPQL
- 엔티티 객체를 대상으로 쿼리함
- 데이터베이스 테이블을 전혀 알지 못한다. 