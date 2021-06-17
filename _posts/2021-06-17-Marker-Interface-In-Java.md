---
layout: post
title: "[20210617] Marker Interface in java"
date: 2021-06-17 23:00
last_modified_at: 2021-06-17 23:00
tags: [java]
toc: true
---

> 완전히 비어있는 인터페이스인 Marker Interface를 알아보자.

### Marker Interface란?

인터페이스에 메서드, 변수, 상수 모두 정의되어 있지 않다면 이를 marker interface라 한다.
즉, 비어있는 인터페이스를 marker interface또는 tagging interface라 한다.
이는 객체에 대한 런타임 타입 정보를 제공해준다. 그래서 컴파일러나 JVM은 해당 객체에 대한 추가적인 정보를 얻는다.
marker interface가 여전히 사용되고 있다. 하지만, marker들은 아무런 행동도 정의하지 않기때문에 code smell을 발생시킬 수 있기에 조심히 사용해야 한다.
Java 5 이후, marker interface대신 똑같은 결과를 얻을 수 있는 어노테이션 방식이 더 선호하고 있다.

### Built-in Marker Interfaces

java는 built-in marker interface로 Serializable, Cloneable and Remote가 있다.

Cloneable interface를 구현하지 않고 객체를 clone하려 한다면, JVM은 CloneNotSupportedException을 발생시킨다.
이러한 이유로, Cloneable interface는 우리가 Object.clone() 메서드를 호출할 수 있는지에 대한 지표를 JVM에게 해준다.

유사하게, Serializable marker interface도 NotSerializableException을 발생시킨다.

### Marker Interfaces vs Annotations

Java 5에서 어노테이션 방식이 소개되면서 marker interfaces와 동일한 결과를 얻을 수 있는 대안으로 사용할 수 있게 되었다.
어노테이션 방식은 marker interface와 같이, 어느 클래스든 어노테이션을 적용할 수 있고, 동일한 행동을 할 수 있도록 지표로 사용할 수도 있다.

그렇다면 둘의 차이점이 뭘까?

어노테이션과 다르게, 인터페이스는 다형성에 이점이 있다. 결과적으로, 우리는 marker interface에 추가적인 제한을 추가할 수 있다. 이는 어노테이션으로는 할 수 없는 일이다.

---

### 출처

https://www.baeldung.com/java-marker-interfaces
