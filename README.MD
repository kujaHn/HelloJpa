# JPA

## 목차
* 1ch. HelloJPa
  * JPA 시작
  * 영속성이란?

* 2ch. 매핑
  * 엔티티 매핑
  * 다양한 연관관계 매핑
  * 고급 매핑

* 3ch. 프록시
  * 최적화
  * 영속성 전이

* 4ch. 값타입
  * 기본 값타입
  * 컬렉션 값타입

* 5ch. JPQL
  * 기본문법
  * 프로젝션과 페이징
  * 조인
  * 서브쿼리
  * JPQL 타입 표현
  * JPQL 기본 함수

* 6ch. 페치 조인
  * 경로표현식
  * 페치 조인
  * 기타 기능

## 설치
### 1. 프로젝트 생성
`Maven`을 사용해서 프로젝트를 생성하자.  
  
![image](https://user-images.githubusercontent.com/72388950/112182618-c96b9a80-8c40-11eb-80df-4c6a93ccaf2b.png)  
프로젝트 이름은 본인이 원하는 이름 아무거나 상관없다.

### 2. H2 데이터 베이스 설치
공부의 목적이기 떄문에 `가볍고` `빠른` H2를 채택하였다.  
[H2 설치](http://www.h2database.com/html/main.html) 링크를 통해 H2를 설치하자.  

### 3. 디펜던시를 통해 라이브러리 다운
`pom.xml`에 다음과 같은 `디펜던시`를 추가하자.  
```
        <!-- JPA 하이버네이트 -->
        <dependency>
            <groupId>org.hibernate</groupId>
            <artifactId>hibernate-entitymanager</artifactId>
            <version>5.3.10.Final</version>
        </dependency>
        <!-- H2 데이터베이스 -->
        <dependency>
            <groupId>com.h2database</groupId>
            <artifactId>h2</artifactId>
            <!-- H2 설치 버전에 맞게 수정 -->
            <version>1.4.200</version>
        </dependency>
```
* **H2 데이터베이스 버전은 다운받은 버전에 맞게 수정을 해주자.**    
* `java: package javax.persistence does not exist` 이슈  
  * JDK 일정 버전 이상에서 `javax`를 찾지 못하는 이슈가 있다. 디펜던시를 추가로 설정해야 한다.  
  ```
  <dependency>
    <groupId>javax.xml.bind</groupId>
    <artifactId>jaxb-api</artifactId>
    <version>2.3.1</version>
  </dependency>
  ```

# 출처 
* [자바 ORM 표준 JPA 프로그래밍 강의 (강사 김영한)](https://www.inflearn.com/course/ORM-JPA-Basic/dashboard)  
* 자바 ORM 표준 JPA 프로그래밍 (저자 김영한)
* [JPA Reference](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#reference)
