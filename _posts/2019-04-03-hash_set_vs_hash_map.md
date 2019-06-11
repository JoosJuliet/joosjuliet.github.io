---
layout: post
section-type: post
title: "HashSet vs HashMap"
category: JAVA
tags: [ 'Java' ]
comments: true
---

모의면접
#csrf
해커가 유저 토큰 이용해서 사용자 권한 있는 역할을 한다.
방지법 - csrf 토큰으로 원하는 페이지에 난수 포함시켜서 그 때 같이 보내준다.
csrf는 인풋의 hidden 필드에 저장된다.(html에 박혀있따.)
해커입장은 js 코드 콜해서 한거니가 모른다.

#크로스 사이트 스크랩트
session탈취는
document.cokkie로 가져올 수 있는데
내가 메일 보냈는데 그 내부에 해커 url둬가지고 그 스크립트 실행하게 한다.
내 글 보는 순간 내 해킹 url을 통해서 실행되도록

방지법: http-only쓰거나, innerhtml안쓰거나, 필드에 필터링을 해준다.

# nginx만들어진 이유
c10k(한서버에 만개이상의 요청이 오면 힘들다)라는 이유로 만들어졌따.
비동기, 만개이상 요청 들어와도 memory, cpu가 일정수준으로 유지된다.

리엑터 패턴? -> 비동기 이해 
스레드와 프로세스를 안쓰고 동시에 한다.
워커 여러개 있따. 멀티 프로세싱 개념보다 죽 한다.



제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존 중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)


직무중심채용
- 내가 이런 역량 있는데 이걸 당신 회사에서 공헌해 보겠습니다.
합리적 논리적



서버 그루 그중에 orm, Object oriented에 관심많지 시스템레벨도 그래서고
서버와 Object oriented을 좋아하는 개발자입니다. 그동안 3개의 회사를 다니면서 서버의 여러 프레임워크을 써봤습니다. 각 회사를 돌면서 어떤 상황에 어떤 서버를 쓰면 옳다는 것을 더 잘 알게 되었습니다. 매번 빠르게 프레임워크를 알고 우아한 코드를 만들기 위해서는 패턴을 잘 아는 것이 중요했습니다. 그래서 object orient와 functional 프로그래밍, ddd에 큰 관심을 가졌습니다.

책임감은 자기결정에서 온다.
뭔가에 책임을 진다는 것은 부담도 있다.
스스로 결정해야 한다는 사실을 인정하면서 그 결과에 대해 책임까지 져야 한다는 것은 받아들이기 힘들다.
책임은 영다어로 responsibility = response, ability



책임이란 곧 어떤 상황에 대한 반응을 결정할 수 있음을 의미한다.

그러므로 스스로 뭔가를 결정했다는 것은 곧 그 결과에 대한 책임도 자신이 져야 한다. 책임이란 결국 자기결정에서 온다.



자기결정성은 당연하지만 우리가 놓고 있떤 심리적 권리이다. 자신에 대해 아는 것만큼 타인의 의견에 흔들리지 않는 것 중요하다.

세상의 누군가는 자신을 싫어할 수 도 있다는 생각에 마음 아ㅠㅏ할 필요없다.

그보다 더 마음 아픈 것은 그들 시선때문에 자신의 인생이 원치 않는 방향으로 틀어지는 것이다.

인생에 무엇이 중요한지 생각해봐라. 스스로 결정해야 책임감이 생긴다.

저는 효율적으로 일하는 것을 좋아하는 사람입니다.
그래서 그쪽에 관련된 저의 역량을 꾸준히 키워나갔습니다. 효율성을 키우기 위해 재사용성이 높은 코드와 디자인패턴에 관심을 가졌습니다. 그래서 프로젝트를 시작할 때 설계 부분에 공을 많이 들여 작업했습니다. 처음에 사용했던 디자인 패턴은 팩토리 패턴이었습니다. 팩토리 패턴을 사용해 다형성을 높일 수 있었고, 그 덕분에 다양한 옵션이 붙은 객체를 관리하기에 수월하게 되었습니다. 그런데 그 과정에서 상속의 깊이가 깊어져 코드가 복잡하게 되는 약점이 발견되었습니다. 이를 해결하기 위해 함수를 만들어서 객체들을 통과시키며 제가 원하는 방식의 객체가 나오게 하였습니다. 그렇게 하니 상속의 깊이가 길어질 때도 가독성이 크게 개선되었습니다. 그리고 함수형 프로그래밍에 관심을 가져서 자주 사용하는 연산들을 만들어 웹의 개발 속도를 높였습니다. 그래서 글로벌 해커톤과 유니톤 같은 짧은 시간에 개발해야 하는 대회에 나가서 최우수상과 농협은행장 상을 받을 수 있었습니다. 그 후에도 저는 it-chain 오픈소스 프로젝트를 통해 도메인 주도 개발에 대한 깊은 이해를 다져가고 있습니다. 특히 도메인 주도 개발에서 도메인을 더 효율적으로 다루며 함수들을 체계화시키니 관련 실력을 계속 키우고 있습니다. 이렇게 효율적으로 일하는 것을 중점으로 자기개발을 꾸준히 하고 싶습니다. 그래서 이런 노력을 해왔기 때문에 저를 효율적으로 일하는 것을 좋아하는 사람으로 볼 수 있습니다.
신세계
1. 당사에 지원한 이유와 입사를 위해 어떤 노력을 하였는지 구체적으로 기술하시오*

저는 최근 핀테크에 대한 많은 관심을 가지며 관련 오픈소스에 계속 기여하고 있는데, 최근 ssg에서는 페이에 관련된 사업을 계속 늘리고 있어

저의 경쟁력은 이미 spring-boot로 쇼핑몰을 개발해 보았기에 java에 숙련도가 있으며, 회사 생활을 했기에 페어프로그래밍과 코드리뷰에 거부감이 없습니다.
또한 datastructure와 Algorithm, network는 기술 블로그[http://joosjuliet.github.io/]를 쓰며 열심히 전문성을 키워 나가고 있습니다.

Line Fintech에 들어가면 LINE의 글로벌 핀테크 서버 개발과 가상화폐 거래소 개발 업무를 담당할 수 있습니다. 현제 저는ㄴ KOSS LAB에서 주관하는 오픈소스 활동[https://github.com/it-chain/engine]으로 block chain을 커스터마이징해서 사용할 수 있는 프로젝트로 하고 있습니다. 그 프로젝트 내에서는 block-chain부분의 구조를 domain-driven-design으로 설계하고 있습니다. LINE에서 요즘 가장 신경을 쓰기 시작한 것은 Fintech분야로 알고 있습니다. 라인은 끊임없이 공부하고 새로운 걸 만들지 않으면 적응하기 쉽지 않은 곳이라는 라인 개발자의 말을 취업설명회 때 들은 적 있습니다. 저 역시 비록 과는 바꿨지만, 끊임없이 공부하고 새로운 것을 만들기 위해 노력해 나가고 있습니다.


2. 지원한 직군에서 구체적으로 하고 싶은 일과 본인이 그 일을 남들보다 잘할 수 있는 차별화된 능력과 경험을 기술하시오*

역량을 갖추기 위해 노력했던 경험 중 가장 기억나는 것은 최근에 인턴으로 다녔든 회사에서 갑자기 운영하든 사이트에 20만이 넘는 사람들이 몰릴 것이 예상되어 웹서버를 만들었던 것이었습니다.
그때 저는 전 회사에서 배달의 민족 외주를 맡아본 적이 있었지만, DB와 캐시서버까지 있는 상황은 한 번도 경험한 적이 없어 걱정되었습니다.
그래서 일단 동료 개발자와 함께 정보를 찾아보며 공부를 했지만, 서버를 스케일링하고 테스트를 했는데 여전히 문제가 생겼습니다.
문제를 해결하기 위해 동료와 다시 한 번 처음부터 함께 차근히 서버정보를 읽어보았습니다.
그러던 중 캐시 서버에 네트워크 대역 대에 따른 가격정책이 있는 것을 보고 그 부분을 놓쳤다는 걸 깨달았습니다.
그래서 그 부분을 업그레이드시켜 안정적인 서버를 성공적으로 만들어 이벤트를 했습니다.
이 경험으로 어려워 보이는 일이 닥치거나 답이 제대로 보이지 않을 때도 차근히 조금씩 만들어가고 만약에 문제가 생길 시에도 동료들과 함께 노력하면 무엇이든 해결할 수 있을 거라는 자신감을 가졌습니다.

3. 학업 외 가장 열정적이고 도전적으로 몰입하여 성과를 창출했거나 목표를 달성한 경험을 기술하시오*

헌신적으로 수행했던 경험(Passion/헌신)
저는 무언가를 할 때 어떤 상황이든 최선을 다해서 일합니다.
대학생 때 sopt라는 동아리에 들어가 2주 만에 기획자가 가져온 프로토타입을 만드는 캠프에 참여했습니다.
친구들과 함께 2주 동안 합숙을 통해 계속 밤을 새워가며 그 프로젝트를 완수하기 위해 노력을 했습니다.
친구들과 저는 크리스마스와 신년이 있었는데 모두 그때 친구들과 노는 것을 포기하고 그 일에 매달렸습니다.
그리고 아르바이트나 회사에 다니던 친구들도 일이 끝나고 와서 동이 틀 때까지 함께 프로젝트를 했습니다.
특히 끝내야 하는 날짜가 다가올 때 다 함께 마지막 삼 일은 먹지도, 잠도 자지 않고 프로젝트에 매진했습니다. 그렇게 모두가 다 함께 본인이 할 수 있는 최선을 다했습니다.
그 결과 기획자가 원하는 만큼 완벽한 프로토타입을 만들지는 못했지만 모든 비즈니스 로직이 돌아가는 프로그램을 만들었습니다.
그리고 친구들과 전우애를 갖게 되었고, 지금도 좋은 추억으로 남아 프로젝트를 이어나가고 있습니다.
그때의 경험으로 같은 목표를 가진 사람들과 함께하면 헌신적으로 일할 때 얼마나 행복할 수 있는지를 배웠고, 언제든 최선을 다해 일하자는 신념도 갖게 된 경험이었습니다.


객체지향적으로 깊은 조예 무엇인가를 공부할때 언제나 깊게 하는 버릇 성실하고 열정적 책임감
장애 + monitoring 성실함

set과 map이 있는데 그건 interface다.

2. HashSet vs HashMap
HashSet
HashSet class implements the Set interface
In HashSet, we store objects(elements or values)e.g. If we have a HashSet of string elements then it could depict a set of HashSet elements: {“Hello”, “Hi”, “Bye”, “Run”}
HashSet does not allow duplicate elementsthat mean you can not store duplicate values in HashSet.
HashSet permits to have a single null value.
HashSet is not synchronized which means they are not suitable for thread-safeoperations until unless synchronized explicitly.[similarity]

 add contains next notes HashSet O(1) O(1) O(h/n) h is the table
HashMap
HashMap class implementsthe Map interface
HashMap is used for storing key & value pairs. In short, it maintains the mapping of key & value (The HashMap class is roughly equivalent to Hashtable, except that it is unsynchronized and permits nulls.) This is how you couldrepresent HashMap elements if ithas integer key and value of String type: e.g. {1->”Hello”, 2->”Hi”, 3->”Bye”, 4->”Run”}
HashMap does not allow duplicate keys however it allows having duplicate values.
HashMap permits single nullkey and any numberof null values.
HashMap is not synchronized which means they are not suitable for thread-safeoperations untilunless synchronized explicitly.[similarity]

 get containsKey next Notes HashMap O(1) O(1) O(h/n) h is the table
Pleaserefer this article to find more information.



출처 : https://stackoverflow.com/questions/2773824/difference-between-hashset-and-hashmap





java 의 set은 treeset과 hashset이 있다.

A Set represents a generic "set of values". A TreeSet is a set where the elements are sorted (and thus ordered), a HashSet is a set where the elements are not sorted or ordered.

A HashSet is typically a lot faster than a TreeSet.

A TreeSet is typically implemented as a red-black tree (See http://en.wikipedia.org/wiki/Red-black_tree - I've not validated the actual implementation of sun/oracle's TreeSet), whereas a HashSet uses Object.hashCode() to create an index in an array. Access time for a red-black tree is O(log(n)) whereas access time for a HashSet ranges from constant-time to the worst case (every item has the same hashCode) where you can have a linear search time O(n).



출처 : https://stackoverflow.com/questions/5139724/whats-the-difference-between-hashset-and-set



그렇다면 treeset과 hashmap은 무슨차이? 하다가 이글 발견

Set: A Set is a Collection that cannot contain duplicate elements. It models the mathematical set abstraction.

HashSet: HashSet extends AbstractSet and implements the Set interface. It creates a collection that uses a hash table for storage.

Map: The Map interface maps unique keys to values. A key is an object that you use to retrieve a value at a laterdate.

HashMap: The HashMap class uses a hashtable to implement the Map interface. This allows theexecutiontime of basic operations, such as get( ) and put(), to remain constant even for large sets.

TreeSet: TreeSet provides an implementation of the Set interface that uses a tree for storage. Objects are stored in sorted, ascending order. Access and retrieval times are quite fast, which makes TreeSet an excellent choice when storing large amountsof sorted information that must be found quickly.

TreeMap: The TreeMap class implements the Map interface by using a tree. A TreeMap provides an efficient means of storing key/value pairs in sorted order, and allows rapid retrieval. You should note that, unlike a hash map, a tree map guarantees that its elements will be sorted in ascending key order.

For Clarification a hash table: A hash table stores information by using a mechanism called hashing. In hashing, the informational content of a key is used to determine a unique value, called its hash code. The hash code is then used as the index at which the data associated with the key is stored. The transformation of the keyinto its hash code is performed automatically



출처 : https://teamtreehouse.com/community/set-hashset-map-hashmap-treeset-treemap
