## Spring mybatis 에서 ${ }문법과 #{ }문법의 차이점

### 1. #{ }

   - 파라미터가 String 형태로 들어와 자동적으로 '파라미터' 형태가 된다.

   - 비밀번호 값이 123이라면 mybatis 쿼리에는 user_password ='123'의 형태가 된다.

   - SQL Injection을 예방할 수 있어 보안측면에서 유리합니다.




### 2. ${ }

   - 파라미터가 바로 출력된다.

   - 비밀번호 값이 123이라면 mybatis 쿼리에는 user_password =123의 형태가 된다.

   - SQL Injection을 예방할 수 없어 보안측면에서 불리합니다.




### 3. sql injection 

   - 응용 프로그램 보안 상의 허점을 의도적으로 이용해, 악의적인 SQL문을 실행되게 함으로써 데이터베이스를 비정상적으로 조작하는 코드 인젝션 공격방법입니다.

   - ${ }을 사용했을 때 발생할 수 있는 문제로,

   - #{ }문법을 사용해 대처합니다.
