---
layout: post
section-type: post
title: "[ JPA ] @Converter @JsonConverter란?"
category: Spring
tags: [ 'Spring', 'JPA' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---
``` java

@JsonTypeInfo(
		use = JsonTypeInfo.Id.NAME,
		property = "type"
)
@JsonSubTypes({
		@JsonSubTypes.Type(value = Success.class, name = "success"),
		@JsonSubTypes.Type(value = Fail.class, name = "fail")
})
public static abstract class Result {
}

@Getter
@Builder
@JsonTypeName("success")
public static class Success extends Result {
	@NotBlank
	private String bidderId;

	@NotNull
	@JsonSerialize(using = ManualJsonConverter.LocalDateTimeSerializer.class)
	private LocalDateTime successAt;
}

@JsonDeserialize(using = ManualJsonConverter.LocalDateTimeDeserializer.class)
private LocalDateTime joinDt;
``` 








- 컨버터를 사용하면 엔티티의 데이터를 변환해서 데이터베이스에 저장할 수 있다.
- 예를들어 회원 VIP여부를 자바의 boolean 타입을 사용하고 싶다고 가정 할 때 JPA를 사용하면 자바의 boolean 타입은 방언에 따라 다르지만 데이터베이스에 저장될 때 0 또는 1인 숫자로 저장된다.
- 그런데 데이터베이스에 숫자 대신 문자 Y 또는 N으로 저장하고 싶다면 컨버터를 이용하면 된다.

``` java
@Entity
@Data
public class Member {

  @Id
  private String id;

  private String name;

  @Convert(converter = BooleanToYNConverter.class)
  private boolean vip;
}
```

회원 엔티티의 vip 필드는 boolean 타입이다. @Convert 를 적용해서 데이터베이스에 저장되기 직전에 BooleanToYNConverter 컨버터가 동작하도록 했다.

``` java
@Converter
public class BooleanToYNConverter implements AttributeConverter<Boolean, String> {

  public String convertToDatabaseColumn(Boolean attribute) {
    return (attribute != null && attribute) ? "Y" : "N";
  }

  public Boolean convertToEntityAttribute(String s) {
    return "Y".equals(s);
  }
}
```

컨버터 클래스는 @Converter 어노테이션을 사용하고 AttributeConverter 인터페이스를 구현해야 한다. 현재 우리는 Boolean타입을 String 타입으로 변환했다.
AttributeConverter 인터페이스는 두개의 메서드가 존재 한다.

convertToDatabaseColumn() : 엔티티의 데이터를 데이터베이스 컬럼에 저장할 데이터로 변환한다. 위에서는 true이면 Y 아니면 false면 N을 반환하도록 했다.
convertToEntityAttribute() : 데이터베이스에서 조회한 컬럼 데이터를 엔티티의 데이터로 변환한다. 위에서는 Y면 true아니면 false를 반환했다.

컨버터 클래스 레벨로 가능하다.

``` java
@Entity
@Data
@Convert(converter = BooleanToYNConverter.class, attributeName = "vip")
public class Member {

  @Id
  private String id;

  private String name;

  private boolean vip;
}
```

글로벌하게 설정도 가능하다.
``` java
@Converter(autoApply = true)
public class BooleanToYNConverter implements AttributeConverter<Boolean, String> {

  public String convertToDatabaseColumn(Boolean attribute) {
    return (attribute != null && attribute) ? "Y" : "N";
  }

  public Boolean convertToEntityAttribute(String s) {
    return "Y".equals(s);
  }
}
```

이렇게하면 자동으로 boolean 값은 모두 컨버터 된다.



@Convert(converter = JpaConverter.YearConverter.class)
@Column(name = "form_year", nullable = false)
private Year formYear;						// 형식연도
