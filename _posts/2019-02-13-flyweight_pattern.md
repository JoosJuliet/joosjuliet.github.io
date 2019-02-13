---
layout: post
section-type: post
title: "Flyweight Pattern(플라이급 패턴)이란?(feat. Java)"
category: Spring
tags: [ 'Java', 'SKEncarLunchStudy', 'FlyweightPattern', 'DesignPattern' ]
comments: true
---

[!flyweight_pattern](/images/2019-02-13-flyweight_pattern/flyweight_pattern.png)
# Flyweight Pattern 패턴

<span style="background-color:yellow"><b> 동일하거나 유사한 객체들 사이에 가능한 많은 데이터를 서로 공유하여 사용하도록 하여 메모리 사용량을 최소화하는 소프트웨어 디자인 패턴 </b></span>
종종 오브젝트의 일부 상태 정보는 공유될 수 있는데, 플라이웨이트 패턴에서는 이와 같은 상태 정보를 외부 자료 구조에 저장하여 플라이웨이트 오브젝트가 잠깐 동안 사용할 수 있도록 전달한다.

특정 객체들이 모두다 똑같은 객체를 공유하고 있는 경우 그 객체를 공유하는 방식으로 객체를 다시 구성하는 방식이다.
- 많은 객체를 만들때 성능을 향상시킬수 있다.
- 많은 객체를 만들때 메모리를 줄일수 있다.

``` java
public class TreeModel {

  Mesh mesh;

  Texture bark;

  Texture leaves;

   public TreeModel() {

     mesh = new Mesh();

     bark = new Texture("bark");

     leaves = new Texture("leaves");

   }

}

// 실제로 매번 생성할 나무 클래스를 정의한다.

public class Tree {

  TreeModel treeModel; //공유할 객체

  Position position;

  double height;

  double thickness;

}

// 팩토리 메소드를 정의한다.

public class TreeFactory{

  private static final TreeModel sharedTreeModel = new TreeModel();

  static public Tree create(Position position, double height, double thickness) {

     Tree tree = new Tree();   

      tree.setPosition(position);

      tree.setHeight(height);

      tree.setThickness(thickness);

      tree.setTreeModel(sharedTreeModel);

  }

}


```
---
참고:

http://ehpub.co.kr/tag/%ED%94%8C%EB%9D%BC%EC%9D%B4%EA%B8%89-%ED%8C%A8%ED%84%B4-flyweight-pattern/
먼저 여기서 플라이급 패턴과 프락시 패턴 보여준다.
플라이웨이트 패턴 참고 : https://m.blog.naver.com/2feelus/220669069127
