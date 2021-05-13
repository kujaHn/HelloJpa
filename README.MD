# JPA

## 목차
* 1ch. HelloJPa
  * [JPA 시작](https://github.com/kujaHn/HelloJpa/blob/main/1ch/README/01.%20JPA%EC%8B%9C%EC%9E%91.MD)
  * [영속성이란?](https://github.com/kujaHn/HelloJpa/blob/main/1ch/README/02.%20%EC%98%81%EC%86%8D%EC%84%B1.MD)

* 2ch. 매핑
  * [엔티티 매핑](https://github.com/kujaHn/HelloJpa/blob/main/2ch-mapping/README/01-%EC%97%94%ED%8B%B0%ED%8B%B0%EB%A7%A4%ED%95%91.MD)
  * [다양한 연관관계 매핑](https://github.com/kujaHn/HelloJpa/blob/main/2ch-mapping/README/02-%EB%8B%A4%EC%96%91%ED%95%9C-%EC%97%B0%EA%B4%80%EA%B4%80%EA%B3%84-%EB%A7%A4%ED%95%91.MD)
  * [고급 매핑](https://github.com/kujaHn/HelloJpa/blob/main/2ch-mapping/README/03-%EA%B3%A0%EA%B8%89%20%EB%A7%A4%ED%95%91.MD)

* 3ch. 프록시
  * [최적화](https://github.com/kujaHn/HelloJpa/blob/main/3ch-proxy/README/01-%EC%B5%9C%EC%A0%81%ED%99%94.MD)
  * [영속성 전이](https://github.com/kujaHn/HelloJpa/blob/main/3ch-proxy/README/02-%EC%98%81%EC%86%8D%EC%84%B1%EC%A0%84%EC%9D%B4.MD)

* 4ch. 값타입
  * [기본 값타입](https://github.com/kujaHn/HelloJpa/blob/main/4ch-valuetype/README/01-%EA%B8%B0%EB%B3%B8%EA%B0%92%ED%83%80%EC%9E%85.MD)
  * [컬렉션 값타입](https://github.com/kujaHn/HelloJpa/blob/main/4ch-valuetype/README/02-%EA%B0%92%ED%83%80%EC%9E%85-%EC%BB%AC%EB%A0%89%EC%85%98.MD)

* 5ch. JPQL
  * [기본문법](https://github.com/kujaHn/HelloJpa/blob/main/5ch-JPQL/README/02-%EA%B8%B0%EB%B3%B8%EB%AC%B8%EB%B2%95.MD)
  * [프로젝션과 페이징](https://github.com/kujaHn/HelloJpa/blob/main/5ch-JPQL/README/03-%ED%94%84%EB%A1%9C%EC%A0%9D%EC%85%98%EA%B3%BC%20%ED%8E%98%EC%9D%B4%EC%A7%95.MD)
  * [조인](https://github.com/kujaHn/HelloJpa/blob/main/5ch-JPQL/README/04-%EC%A1%B0%EC%9D%B8.MD)
  * [서브쿼리](https://github.com/kujaHn/HelloJpa/blob/main/5ch-JPQL/README/05-%EC%84%9C%EB%B8%8C%EC%BF%BC%EB%A6%AC.MD)
  * [JPQL 타입 표현](https://github.com/kujaHn/HelloJpa/blob/main/5ch-JPQL/README/06-JPQL%ED%83%80%EC%9E%85%ED%91%9C%ED%98%84-%EA%B8%B0%ED%83%80%EC%8B%9D.MD)
  * [JPQL 기본 함수](https://github.com/kujaHn/HelloJpa/blob/main/5ch-JPQL/README/07-JPQL%EA%B8%B0%EB%B3%B8%ED%95%A8%EC%88%98.MD)

* 6ch. 페치 조인
  * [경로표현식](https://github.com/kujaHn/HelloJpa/blob/main/6ch-fetchjoin/README/01-%EA%B2%BD%EB%A1%9C%ED%91%9C%ED%98%84%EC%8B%9D.MD)
  * [페치 조인](https://github.com/kujaHn/HelloJpa/blob/main/6ch-fetchjoin/README/02-Fetch_Join.MD)
  * [기타 기능](https://github.com/kujaHn/HelloJpa/blob/main/6ch-fetchjoin/README/03-%EA%B8%B0%ED%83%80%EA%B8%B0%EB%8A%A5.MD)

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
