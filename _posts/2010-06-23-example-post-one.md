---
title: [Spring]01.@
categories:
- Spring
feature_image: "https://picsum.photos/2560/600?image=872"
---

@Autowired 어노테이션을 적용하면 반드시 주입할 의존 객체가 존재해야 한다. 

만약 xml 설정파일에 해당하는 객체가 존재하지 않으면, @Autowired가 적용된 대상에 주입할 객체를 찾을 수 없기 때문에 Exception이 발생한다.

Caused by: org.springframework.beans.factory.UnsatisfiedDependencyException: 
    Error creating bean with name 'userRepositoryUserDetailsService' defined in file 
    [../UserRepositoryUserDetailsService.class]: 
    Unsatisfied dependency expressed through constructor argument with index 0 of type 
[org.cru.cloud.management.data.UserRepository]: : No qualifying bean of 
    type [org.cru.cloud.management.data.UserRepository] found for dependency: 
        expected at least 1 bean which qualifies 
        as autowire candidate for this dependency. 
.....
Colored by Color Scripter
cs


@Autowired 어노테이션에 require 속성을 이용해, 대상에 꼭 의존 객체를 주입하지 않아도 된다고 설정할 수 있다. 

1
@Autowired(require=false)
cs


이 경우 @Autowired 어노테이션이 적용된 대상에 주입할 의존 객체가 없더라도 required=false이기 때문에 스프링 컨테이너를 생성하는 과정에서 Exception을 발생시키지 않는다. (대신 null이 됨)



required=false인 경우 의존 객체가 주입되지 않는 것이 아니다. 

주입할 의존 객체가 존재하면 해당 객체는 @Autowired 적용 대상에 주입되는 것은 같지만 required=false인 경우 주입할 의존 객체가 존재하지 않아도 Exception을 발생시키지 않는다. 
