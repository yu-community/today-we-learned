## method reference

Post 객체가 담긴 List를 순회할 때 다음과 같이 for-each문을 사용할 수 있다.

```java
for (Post post : postList) {
    System.out.println(post);
}
```

그러나 Java collection에서 제공하는 `Collection.foreach()`와 Java에서 제공하는 인터페이스인 Consumer를 사용하면 다음과 같이 작성할 수 있다.

```java
postList.forEach(post -> System.out.println(post));
```

위 코드는 아래 코드와 동일하다.

```java
postList.forEach(System.out::println)
```

이렇게 특정 클래스 메서드를 method reference로 쉽게 작성할 수 있다.
