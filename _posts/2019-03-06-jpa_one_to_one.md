---
layout: post
section-type: post
title: "Title"
category: Algorithm
tags: [ 'algorithm', 'python' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---
모든 관리 대상 엔티티에 대해 지속성 컨텍스트에는 엔티티 유형과 식별자가 모두 필요합니다. 따라서 부모 엔티티를로드 할 때 하위 식별자를 알아야하며 관련 post_details 기본 키를 찾는 유일한 방법은 보조 쿼리를 실행하는 것입니다.

가능한 유일한 해결 방법은 바이트 코드 향상뿐입니다.
(관련 url : https://vladmihalcea.com/how-to-enable-bytecode-enhancement-dirty-checking-in-hibernate/)


<b>그래서 그냥 One to One시 @MapsId 사용하면 된다 'ㅅ'</b>

이렇게하면 Post 엔티티 식별자를 사용하여 항상 PostDetails 엔티티를 가져올 수 있기 때문에 양방향 연관조차 필요하지 않습니다.

``` java
@Entity(name = "PostDetails")
@Table(name = "post_details")
public class PostDetails {

    @Id
    private Long id;

    @Column(name = "created_on")
    private Date createdOn;

    @Column(name = "created_by")
    private String createdBy;

    @OneToOne(fetch = FetchType.LAZY)
    @MapsId
    private Post post;

    public PostDetails() {}

    public PostDetails(String createdBy) {
        createdOn = new Date();
        this.createdBy = createdBy;
    }

    //Getters and setters omitted for brevity
}
```

``` java
Post post = entityManager.find(Post.class, 1L);
    PostDetails details = new PostDetails("John Doe");
    details.setPost(post);
    entityManager.persist(details);
```
Post 엔티티 식별자를 사용하여 PostDetails를 가져올 수도 있기 때문에 양방향 연관이 필요하지 않습니다

엔티티 관계를 효율적으로 매핑하는 방법을 알면 애플리케이션 성능 측면에서 많은 차이를 만들 수 있습니다. @OneToOne 연관에 대해서는 항상 기본 키를 상위 테이블과 공유해야하며 바이트 코드 향상을 사용하지 않으려는 경우 양방향 연관을 피해야합니다.

https://vladmihalcea.com/the-best-way-to-map-a-onetoone-relationship-with-jpa-and-hibernate/
