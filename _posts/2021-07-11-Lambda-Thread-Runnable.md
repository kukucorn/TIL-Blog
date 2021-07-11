---
layout: post
title: "[20210711] 람다식을 이용한 Thread 와 Runnable"
date: 2021-07-11 22:42
last_modified_at: 2021-07-11 22:42
tags: [java]
toc: true
---

> lambda를 이용해서 Thread와 Runnable을 표현한다.

### 람다식

람다식을 이용하려면 람다식을 사용하여는 인터페이스가 함수형 인터페이스여야 한다.
함수형 인터페이스란 추상 메서드를 단 하나만 가지고 있는 인터페이스이다.

### 자바에서의 쓰레드

자바에서 쓰레드를 사용하기 위해서는 Thread 클래스를 상속받아서 클래스를 구현해야 한다.
하지만, 구현하려는 클래스가 이미 다른 클래스를 상속받고 있다면 Thread 클래스를 상속받을 수가 없다.(자바는 다중 상속을 지원하지 않는다.)
Thread 클래스를 상속받을 수 없을 때, Runnable 인터페이스를 구현하여 쓰레드를 구현하면 된다.
Runnable 인터페이스는 run()이라는 추상 메서드 하나만을 정의하고 있다.
그래서 Runnable 인터페이스는 함수형 인터페이스이다.

### 람다를 이용한 Runnable

Runnable 인터페이스를 이용한 Thread 사용
Runnable 인터페이스를 람다식으로 구현하고 Thread의 생성자 파라미터로 전달하고 있다.

    Runnable runnable = () -> {
    // your code here ...
    }; // 람다식을 이용해서 Runnable을 구현하고 있다.
    Thread t = new Thread(runnable);
    t.start();

Thread 생성자에서 단일 파라미터 생성자는 String과 Runnable 밖에 없으므로 람다식을 이용해도 Runnable로 추론이 가능하다.

    Thread t = new Thread(() -> {
    // your code here ...
    });
    t.start();

쓰레드에 대한 참조가 필요없다면 쓰레드 클래스를 선언하지 않아도 된다.

    new Thread(() -> { // your code hear }).start();

### 람다를 이용하지 않은 Runnable

java8 미만을 사용한다면 람다를 사용하지 못한다...

    Thread t = new Thread(new Runnable() {
        public void run() {
            // your code here ...
        }
    });
    t.start();

람다 짱..!

---

### 참조

[https://alvinalexander.com/java/java-8-lambda-thread-runnable-syntax-examples/](https://alvinalexander.com/java/java-8-lambda-thread-runnable-syntax-examples/)
