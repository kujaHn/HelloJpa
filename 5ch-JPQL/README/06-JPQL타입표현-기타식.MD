#JPQL 타입 표현

`TypeExpression.java`참고

### 문자
* `single quotation marks(')` 사용, (') 기호를 표시하고 싶을때는 두번('') 쓰기  
  * ex: `'HELLO'` = `HELLO`  /  `'She''s'` = `She's`


### 숫자
* Long은 `L`, Double은 `D`, Float는 `F`를 숫자뒤에 입력
    * ex: `10L` : Long / `10D` : Double / `10F` : Float 
    

### Boolean
* `TRUE`, `FALSE`


### ENUM
* 자바 패키지명을 포함해서 입력해야 함.
    * ex: `domain.MemberType.Admin` : Admin , `domain.MemberType.Guest` : Guest
<br></br>
* `패키지 명`을 JPQL에서 입력하는 방법도 있고
    ```jpaql
    select m.userName, 'TypeExTest1', true from Member m  +
           where m.type = domain.MemberType.ADMIN;
    ```

* 파라미터 바인딩을 이용하는 방법도 있다.
    ```jpaql
    String query = "select m.userName, 'TypeExTest1', true from Member m " +
            "where m.type = :userType";

    List<Object[]> resultList = em.createQuery(query)
           .setParameter("userType", MemberType.ADMIN)
           .getResultList();
    ```
  

### 엔티티 타입
* `EntityTypeExperssion.java`를 참고하자<br></br>

* `상속관계`에서 `특정 엔티티타입`만 쓰고 싶을때 사용  
  ex: Item을 상속하고 있는 엔티티들 중에 `Book 타입`만 쓰고 싶다 => `TYPE(i) = Book`
  ```jpaql
  em.createQuery("select p from Product p where type(p) = Book", Product.class)
  ```
  

## JPQL 기타식
* SQL과 문법이 같은 식 (`SameAsSql.java` 참고)
  * `EXISTS`, `IN` : 한 컬럼의 값이 같은 데이터를 여러개 가져올 때 사용  
    ex: `"SELECT m FROM Member m where exists (select t FROM Team T where t.name = 'TeamA')"`
    <br></br>
  * `AND`, `OR`, `NOT`  <br></br>

  * `비교 연산자`  
    ex: `"select o from Order o where o.orderAmount > All (select p.stockAmount from Product p)"`
    <br></br>
  
  * `BETWEEN`, `LIKE`, `IS NULL`  
    ex: `"select m.userName From Member m where m.userName is not null"`  
    ex2: `"select m.userName From Member m where m.age between 1 and 20"`  
    <br></br>
    

## 조건식
`CASE`식은 자바의 `SWITCH`문과 유사하다.
### 기본 CASE 식
* 범위를 지정할 수 있다. `CaseMain.java` 참고
```jpaql
select 
    case when m.age <= 10 then '학생요금'
         when m.age >= 60 then '경로요금'
         else '일반요금'
    end
from Member m
```

### 단순 CASE 식
* 정확하게 일치해야 한다.
```jpaql
select 
    case t.name
         when '팀A' then '인센티브110%'
         when '팀B' then '인센티브120%'
         else '인센티브100%'
    end
from Team t
```

### COALESCE
* 하나씩 조회해서 `null`이 아니면 데이터 그대로 반환, 아니면 입력된 파라미터를 반환.
`CoalesceMain.java 참고`  

* 예시  
  사용자 이름이 없으면 이름 없는 회원을 반환  
  `select coalesce(m.username, '이름 없는 회원') from Member m`
  

### NULLIF
* 두 값이 같으면 `null` 반환, 다르면 `첫번째 값` 반환
  `NullIfMain.java` 참고  
* 예시
  이름이 `관리자`이면 이름을 `Null`로 반환  
  `select nullif('관리자', m.userName) from Member m`