---
title: [Spring]01.Autowired 어노테이션
categories:
- Spring
feature_image: "https://picsum.photos/2560/600?image=872"
---

@Autowired 어노테이션을 적용하면 반드시 주입할 의존 객체가 존재해야 한다. 

만약 xml 설정파일에 해당하는 객체가 존재하지 않으면, @Autowired가 적용된 대상에 주입할 객체를 찾을 수 없기 때문에 Exception이 발생한다.
@Autowired 어노테이션에 require 속성을 이용해, 대상에 꼭 의존 객체를 주입하지 않아도 된다고 설정할 수 있다. 

@Autowired(require=false)

이 경우 @Autowired 어노테이션이 적용된 대상에 주입할 의존 객체가 없더라도 required=false이기 때문에 스프링 컨테이너를 생성하는 과정에서 Exception을 발생시키지 않는다. (대신 null이 됨)

required=false인 경우 의존 객체가 주입되지 않는 것이 아니다. 

주입할 의존 객체가 존재하면 해당 객체는 @Autowired 적용 대상에 주입되는 것은 같지만 required=false인 경우 주입할 의존 객체가 존재하지 않아도 Exception을 발생시키지 않는다. 

@AUTOWIRED 어노테이션의 적용순서
의존 객체를 찾는 순서.

1.타입이 같은 빈 객체를 검색하고 한 개라면 그 빈 객체를 사용한다. @Qualifier가 명시되어 있으면 @Qualifier와 같은 값을 갖는 빈 객체여야 한다.
2.타입이 같은 빈 객체가 두 개 이상 존재하면 @Qualifier로 지정한 빈 객체를 찾는다. 존재하면 그 객체를 사용한다.
3.타입이 같은 빈 객체가 두 개 이상 존재하고 @Qualifier가 없을 경우 이름이 같은 빈 객체를 찾는다. 존재하면 그 객체를 사용한다.
위 단계에 해당되지 않으면 스프링 컨테이너는 Exception을 발생시킨다.

@AUTOWIRED와 파라미터
@Autowired 어노테이션을 적용한 생성자나 메서드에 파라미터가 두 개 이상인 경우, @Qualifier 어노테이션을 적용할 땐 해당 파라미터에 직접 지정해주면 된다. 파라미터가 한 개인 경우에도 지정할 수 있다.

public class ContactBook{
    private Contact contact;
    private ContactCategory category;
 
    @Autowired
    public void injectDependency(Contact contact,
        @Qualifier("category1") ContactCategory category){
        this.contact = contact;
        this.category = category
    }
}
