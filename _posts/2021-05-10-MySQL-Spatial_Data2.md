---
layout: post
title: "[20210510] Client Test Using RestTemplate"
date: 2021-05-10 23:40
last_modified_at: 2021-05-10 23:40
tags: [Test]
toc: true
---

## Client test

### Rest Template

> controller를 통합 테스트 하기 위한 http client

Spring Framework 5와 함께 Web Flux가 출시되면서 새로운 http client인 Web Client가 소개 되었다. 이는 다음에 다루기로 하며 오늘은 이전까지 사용되어 왔던 Rest Template를 공부하려 한다.

http method get 뿐만 아니라 post, head, options 등 모두 지원하지만 여기서는 get만 다뤄보려 한다.

    RestTemplate restTemplate = new RestTemplate();
    String fooResourceUrl = "http://localhost:8080/spring-rest/foos";

공통적인 선언이다.  
첫 번재로, JSON으로 반환 받기이다.

    ResponseEntity<String> response = restTemplate.getForEntity(fooResourceUrl + "/1", String.class);

반환형으로 String class를 선언하고 있다.  
String으로 반환받은 값을 Jackson을 사용하여 변환해서 사용하면 된다.

두 번째로, POJO로 반환 받기이다.

    Foo foo = restTemplate.getForObject(fooResourceUrl + "/1", Foo.class);

해당 클래스를 파라미터에 선언하면 된다.(해당 클래스는 기본 생성자가 있어야 한다.)

세 번째로, 객체 리스트 반환 받기이다.

    ResponseEntity<Employee[]> response = restTemplate.getForEntity("http://localhost:8080/employees/",Employee[].class);

혹은,

    public class EmployeeList {
    private List<Employee> employees;

    public EmployeeList() {
        employees = new ArrayList<>();
    }

    // standard constructor and getter/setter

}

Wrapper 클래스를 생성하면 된다.

다른 http method를 사용하려면 유사한 함수와 유사한 파라미터를 사용하면 되기에 검색하여 사용하면 될 것이다.

---

### 출처

The Guide to RestTemplate : <https://www.baeldung.com/rest-template#rest-template-is-deprecated>
