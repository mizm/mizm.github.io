---
layout: post
title:  "Abstract Class Vs Interface"
date:   2021-05-15T10:02:52-05:00
author: miz
categories: Java
---

# Abstract Class( 추상 클래스 )
- 추상 클래스랑 클래스에 선언에 `abstract` 키워드가 쓰여진 경우
- 추상 메서드를 포함하지 않을수도 있다.
- `abstract` 메서드가 있다면 무조건 `abstract` 클래스로 선언해주어야한다
- 클래스와 동일하게 static, final, protected, private 등 모든 선언이 가능하다.
```java
public abstract class Unit {

    abstract void move():
}

```
- 추상 메서드를 상속받는 클래스들은 abstract 메서드를 모두 구현해야한다.


# Interface ( 인터페이스 )
- 인터페이스는 선언할때 `interface`로 선언한다
- 메서드에는 `public abstract`가 생략된다.
- 인스턴스변수에는 `public static final`이 생략 된다.
- 자바 8부터는 static, default를 통해 메서드를 구현할 수 있다.
- 다중 여러개의 인터페이스를 구현 할 수 있다.
```java
public interface Moveable {

    void move();
}

```


# 차이점
- 사용하는 용도가 다르다
- Interface
    - 특정 클래스의 행동을 알려주고 싶은데, 어떤 식으로 구현이 되는지는 신경쓰지 않는경우
    - 서로 관련성이 없는 클래스들이 비슷한 행동을 사용하는 경우

- abstract class
    - 클래스들 간의 관련성이 높을 때 중복 된 코드를 관리하기 위해
    - 클래스 들의 중복 코드(메서드, 필드) 가 많고 public 이외의 접근제어자 사용이 필요할떄
    - 템플릿 메서드 패턴에서 주로 사용