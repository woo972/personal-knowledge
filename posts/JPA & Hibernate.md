---
tags:
  - dev
  - jpa
  - hibernate
dg-publish: true
---
## Context
---
JPA를 활용하여 entity manager를 통해 entity를 관린한다는 것은 persistence context에 entity를 관리한다는 의미이다. persistence context는 entity를 캐시에 관리한다.
- 조회 시 바로 꺼내볼 수 있다.
- 동일성을 보장한다.
- lazy transaction을 지원하여 한 번에 커밋한다.
- dirty checking이 가능하다. (변경이 있을 때 update() 같은 메서드를 명시적으로 호출하지 않아도 캐쉬에 있는 스냅샷과 데이터를 비교하여 DB에 업데이트 한다)
## Annotations
---
- @Column
- @Enumerated: Java Enum을 String으로 변환하여 저장한다
- @Temporal: Java Date를  String으로 변환하여 저장한다
- @Transient: DB에 매핑하지 않을 컬럼을 지정한다
- @ManyToOne
- @OneToMany
- @JoinColum(name="..."): 조인 키 컬럼
- @...(mapped by = "..."): 양방향 매핑 시 반대편의 필드명 지정 (owner는 외래키를 관리하는 테이블)
- @...(fetch=FetchType.LAZY): 프록시를 사용해 지연로딩
- @DynamicUpdate: deprecated된 hibernate기능. update에 대해 엔티티 전체가 아니라 변경된 컬럼만 update구문에 넣게 하는 어노테이션. 
	- pros & cons가 존재하기 때문에 사용시 주의 필요.
		- https://velog.io/@wwlee94/JPA-%EC%82%AC%EC%9A%A9%EC%8B%9C-%EB%8F%99%EC%8B%9C%EC%84%B1-%EC%9D%B4%EC%8A%88
- @SQLDelete: JPA delete 쿼리 호출 시 지정된 쿼리로 soft delete를 수행한다
- @Where: select 시 해당 어노테이션에 지정된 조건을 제외한다 (주로 @SQLDelete와 함께 사용)
- @AttributeOverride: 상속하거나 embeding한 테이블의 컬럼명을 바꿀 때 사용한다. @AttributeOverrides를 통해 여러 필드를 한번에 바꾸는 것도 가능한다
- @MappedSuperClass: 다른 엔티티들에서 공통으로 사용하는 매핑정보를 BaseEntity에 붙이는 어노테이션. 통상 BaseEntity는 추상클래스로 작성한다.
- @JdbcTypeCode: db에 저장되는 타입 설정
- @CreatedDate / @LastModifiedDate: 엔티티가 생성되어 저장되거나 수정될 때 자동으로 감지하여 날짜를 넣어준다. (이를 활용하기 위해서 @EnableJpaAuditing 어노테이션이 필수다)
## 참고
---
- Kotlin, SpringBoot3에서 QueryDSL 설정: https://velog.io/@hana0627/Kotlin-SpringBoot3-QueryDsl-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0