# jpashop
실전! 스프링 부트와 JPA 활용1 - 웹 애플리케이션 개발

## `show_sql: true`를 쓰지마라

Hibernate를 쓰면서 SQL 로그를 보기 위해 `spring.jpa.properties.hibernate.show_sql=true`를 쓰는데, 이것은 `System.out`을 쓰기 때문에 적절하지 않다.
로거를 사용하기 위해서는 `logging.level.org.hibernate.SQL=debug`를 쓴다.

## `@Rollback(false)`하면 롤백 안 한다

테스트 작성할 때, `@Transactional`은 테스트가 끝나면 롤백하는데, `@Rollback(false)`를 추가하면 롤백하지 않는다.

## 테스트에서 insert 쿼리 조차 날리지 않는다

테스트에서 `@Rollback(false)`가 없으면 `save()`를 호출해도 insert 쿼리를 날리지 않는다.

`save()` 호출 후 `find()`할 때에도, select 쿼리를 날리지 않는다. 영속성 컨텍스트에 있는 것을 가져오기 때문이다. 
