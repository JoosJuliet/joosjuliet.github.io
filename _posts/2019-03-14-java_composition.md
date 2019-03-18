---
layout: post
section-type: post
title: "java_composition"
category: Java
tags: [ 'Java', 'composition' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---

"가급적 상속(Inheritance)보다는 컴포지션(composition)을 사용하자"

# 상속의 안전함과 위험함.
## 안전함
- 동일한 프로그래머가 서브 클래스와 슈퍼 클래스의 구현을 관장하는, 같은 패키지 내에서 상속을 하는 것은 안전합니다
- 클래스가 상속을 위해 특별히 설계되었으며, 문서화가 잘 된 클래스를 "확장(extends)"의 목적으로 상속하는 것도 안전합니다.

## 위험함
- 상속의 오용 ( 서로 다른 패키지에 있으며, 확장을 목적으로 설계되지 않은 일반적인 클래스를 상속받는 것은 위험합니다.)
- 상위 클래스 변경이 어려움.

# 무엇이 그렇게 위험한가?
- 상속은 캡슐화에 위배합니다.
  - 하위 클래스가 정상 동작하기 위해서는 상위 클래스의 구현에 의존할 수 수 밖에 없다.
  - 이 때 수퍼 클래스의 구현 내용은 소프트웨어 배포판이 바뀌면서 변경될 수 있습니다.
  - 이렇게 되면 서브 클래스의 코드를 그냥 사용하게 되면 제대로 동작하지 않을 가능성이 높다.
  - 수퍼클래스의 변화를 항상 감지하고, 맞춰 진화가 되어야만 하는데 쉽지 않다.
> *캡슐화*
    모든 method는 기능 중심이어야 하고, 특정 객체의 변화를 주려면 그 객체의 method에서 나와야 한다.
  - 1) Tell, Don’t Ask
    - 데이터를 물어보지 않고 , 기능을 실행해 달라고 말하라는 규칙.
    -  
      if (member.getExpiryDate() != null && member.getExpiryDate().getDate() < System.currentTimeMillis() ) { // BAD }
      if (memer.isExpired()) { // GOOD }      
  - 2) Law of Demeter
    - 메서드에서 생성한 객체의 메서드만 호출
    - 파라미터로 받은 객체의 메서드만 호출
    - 필드로 참조하는 객체의 메서드만 호출
  따라서 데미테르 법칙을 따르려면, 위 코드를 member 객체에 대한 한 번의 메서드 호출로 변경해 주어야 한다.
  if (member.getDate().getTime() < ..) -> if (member.isSomeGoodTime())
  이를 통해 데이터 중심이 아닌 기능 중심으로 코드를 작성하도록 유도해준다.

- 개발자가 실수를 할 수 있는 여지가 많다.
  - 추후 배포판의 수퍼 클래스에 새 메소드를 추가할 때 그 메소드와 signature 는 동일하고, return type 이 다른 메소드의 함수가 서브 클래스에 이미 있다면, 잘못된 오버라이딩으로 서브 클래스에서 컴파일 에러가 생깁니다.
  - 반대로, 서브 클래스의 새 함수와 같은 signature 와 return type 을 가진 함수를 수퍼클래스에서 정의한다면, 잘못된 오버라이딩을 한 셈이 됩니다.

- 클래스의 내부 구현을 쓸데 없이 노출시킬수도 있습니다.
  - 그렇게 되면, 외부 API 와 내부 구현이 밀접하게 연계되어 클래스의 성능을 제한하게 되지요.
  - 심각하게는 클라이언트가 내부 메소드나 필드를 직접 접근할 수도 있다는 것입니다.
  - 더 심각한 것은, 클라이언트가 수퍼 클래스를 직접 수정하여 서브 클래스의 불변성을 저해할 수 있습니다.

# 그럼 방법은 무엇인가?
기존 클래스를 상속받는 대신, 새로운 클래스에 기존 클래스 객체를 참조하는 private 필드를 하나 두는 것으로 위와 같은 문제를 예방할 수 있습니다. 이런 설계 기법을 구성(Composition)이라고 부르는데, 기존 클래스가 새 클래스의 일부(component)가 되기 때문입니다. 새로운 클래스에 포함된 각각의 메서드는 기존 클래스에 있는 메서드 가운데 필요한 것을 호출해서 그 결과를 반환하면 됩니다. 이런 구현 기법을 전달(forwarding)이라고 부릅니다. 구성 기법을 통해 구현된 클래스는 견고합니다. 기존 클래스의 구현 세부사항에 종속되지 않기 때문입니다. 기존 클래스에 또 다른 메서드가 추가되더라도, 새로 만든 클래스에는 영향이 없을 것입니다. 이렇게 함으로서 새 클래스는 기존 클래스의 내부 구현에 종속되지 않으며, 새로운 메소드를 추가하더라고 새 클래스에는 영향을 주지 않습니다. 이런 클래스를 wrapper class 라고 합니다.

```java
// 계승을 잘못 사용한 사례!
public class InstrumentedHashSet<E> extends HashSet<E> {
  // 요소를 삽입하려 한 횟수
  private int addCount = 0;

  public InstrumentedHashSet() {
  }

  public InstrumentedHashSet(int initCap, float loadFactor) {
    super(initCap, loadFactor);
  }

  @Override public boolean add(E e) {
    addCount++;
    return super.add(e);
  }

  @Override public boolean addAll(Collection<? extends E> c) {
    addCount += c.size();
    return super.addAll(c);
  }

  public int getAddCount() {
    return addCount;
  }
}

```
``` java
InstrumentedHashSet<String> s = new InstrumentedHashSet<String>();
s.addAll(Arrays.asList("Snap", "Crackle", "Pop"));

```
getAddCount 메서드가 3을 반환할 것이라고 기대하지만, 실제로는 6을 반환합니다. 무엇이 잘못된 것일까요? 사실 HashSet의 addAll 메서드는 add 메서드를 통해 구현되어 있습니다. 그리고 HashSet 문서에는 그런 사실이 명시되어 있지 않습니다. InstrumentedHashSet에 정의된 addAll 메서드는 addCount에 3을 더하고 상위 클래스인 HashSet의 addAll 메서드를 super.addAll과 같이 호출하는데, 이 메서드는 InstrumentedHashSet에서 재정의한 add 메서드를 삽입할 원소마다 호출하게 됩니다. 각각의 add 메서드가 호출될 때마다 addCount는 1씩 증가할 것이므로, 총 6만큼 증가하게 되는 것입니다. addAll 메서드로 추가한 요소는 중복 계산하게 되는 것입니다.

``` java
// 계승 대신 구성을 사용하는 포장(wrapper) 클래스
public class InstrumentedSet<E> extends ForwardingSet<E> {
  private int addCount = 0;

  public InstrumentedSet(Set<E> s) {
    super(s);
  }

  @Override public boolean add(E e) {
    addCount++;
    return super.add(e);
  }

  @Override public boolean addAll(Collection<? extends E> c) {
    addCount += c.size();
    return super.addAll(c);
  }

  public int getAddCount() {
    return addCount;
  }

}

// 재사용 가능한 전달(forwarding) 클래스
public class ForwardingSet<E> implements Set<E> {
  private final Set<E> s;
  public ForwardingSet(Set<E> s) { this.s = s; }

  public void clear()           { s.clear(); }
  public boolean contains(Object o)   { return s.contains(o); }
  public boolean isEmpty()        { return s.isEmpty(); }
  public int size()           { return s.size(); }
  public Iterator<E> iterator()     { return s.iterator(); }
  public boolean add(E e)         { return s.add(e); }
  public boolean remove(Object o)     { return s.remove(o); }
  public boolean containsAll(Collection<?> c)
                      { return s.containsAll(c); }
  public boolean addAll(Collection<? extends E> c)
                      { return s.addAll(c); }
  public boolean removeAll(Collection<?> c)
                      { return s.removeAll(c); }
  public boolean retainAll(Collection<?> c)
                      { return s.retainAll(c); }
  public Object[] toArray()       { return s.toArray(); }
  public <T> T[] toArray(T[] a)     { return s.toArray(a); }
  @Override public boolean equals(Object o)
                      { return s.equals(o); }
  @Override public int hashCode()   { return s.hashCode(); }
  @Override public String toString()  { return s.toString(); }
}

```

https://12bme.tistory.com/191
# Composition & Forwarding 을 하는 Wrapper class 는 단점이 없는가?
- 객체 자신의 참조를 다른 객체에게 전달하는 콜백 프레임워크( callback framework ) 에서의 사용은 부적합합니다. 래퍼 객체에 포함된 객체는 자신의 래퍼 객체를 알지 못하므로, 콜백을 할 경우 자신의 참조만을 다른 객체에 전달하기 때문입니다.

- Forwarding method 들의 호출 또는 Wrapper instance 의 빈번한 메모리 할당과 해지가 성능에 영향을 주지는 않을까 싶지만, 실제로 큰 영향을 주지 않는다는 것으로 밝혀졌다고 합니다.


# 그럼 상속( Inheritance ) 는 언제 쓸 수 있는것인가?

- 두 클래스가 "is-a" 관계일 때 클래스 B를 클래스 A의 서브 클래스로 확장(상속)해야 합니다. 만일 클래스 B를 클래스 A의 서브 클래스로 만들고 싶다면 "모든 B 객체가 진정한 A인가?" 라는 질문을 던져봐야 합니다. 자신있게 "예" 라고 대답할 수 없다면 상속을 하지 말아야 합니다. 바로 Composition 을 고려해봐야 합니다. B에서 A의 instance 를 private 으로 포함하고, 작고 간단한 API 메소드를 포함하는 것이죠.

- 수퍼클래스의 API 에 결함은 없는지, 결함이 있다면 그 결함을 그대로 상속받을 것인지를 생각해보아야 합니다. 결함이 있고, 그 결함을 받아들일 수 없다면, Composition 을 사용하는 것이 좋습니다.  Composition 으로 그 결함을 감출 수 있기 때문이죠.



그러나 다른 패키지에 걸쳐 일반적인 실체 클래스로부터 상속을 받는 것은 위험하다.
슈퍼 클래스와 동일한 시그니처 및 반환 타입을 갖고 있다면, 의도하지 않은 오버라이딩을 한 셈이 되어 또 다른 문제가 발생한다.
클래스를 확장(상속)하는 대신 기존 클래스의 인스턴스를 참조하는 private 필드를 새로운 클래스에 두는 컴포지션(composition) 으로 상속의 문제점들을 해결할 수 있다.
새 클래스의 각 인스턴스 메소드에서는 포함된 기존 클래스 인스턴스의 대응되는 메소드를 호출하여 결과를 반환할 수 있다. ( 포워딩(forwarding) )
새 클래스는 기존 클래스의 내부 구현에 종속되지 않으며, 기존 클래스에 새로운 메소드를 추가하더라도 새 클래스에는 영향을 주지 않는다.


컴포지트를 이용하여 모든 public 함수들을 forwarding 한 클래스를 래퍼(wrapper) 클래스라고 하는데,
이것을 데코레이터 패턴(decorator pattern) 이라고도 한다. ( 기존 클래스에 덧붙여 치장(decorate)하기 때문 )
래퍼 클래스의 단점은 거의 없지만, 컴포지트 된 객체 자신의 참조를 다른 객체에게 전달하는 콜백 프레임워크(callback framework)에서의 사용은 부적합하다.
래퍼 객체에 포함된 객체는 자신의 래퍼 객체를 알지 못하기 때문이다.

---

출처:
http://aroundck.tistory.com/617
http://aroundck.tistory.com/3112
출처: https://12bme.tistory.com/191 [길은 가면, 뒤에 있다.]
