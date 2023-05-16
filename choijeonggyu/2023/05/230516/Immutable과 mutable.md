## Immutable과 mutable

Immutable과 mutable의 **차이점은 값을 수정할 수 없음**이다. 알고 있었지만 말 그대로 알고만 있었다. 다음 코드를 보자.

```java
List<Post> postList = new ArrayList<>();
post.add(new Post("안녕하세요", "반갑습니다"));
post.add(new Post("Hello", "World!"));

// 값 수정
Post result = postList.get(1);
result.content = "세계!";

postList.forEach(System.out::println); // [..., "Hello", "세계!"]
```

자바에서 객체는 주소로서 참조되므로 `result`에는 `postList`의 1번째 객체의 주소가 저장된다.

그렇기 때문에 `result`의 값을 수정하면 `postList` 속의 내용도 변경된다.

```java
List<Integer> numList = new ArrayList<>();
numList.add(1);
numList.add(2);
numList.add(3);

// 값 수정
Integer result = numList.get(i);
result = 777;

// expect: [1, 777, 3], actual: [1, 2, 3]
numList.forEach(System.out::println);
```

Integer 또한 객체이므로 result는 numList의 첫 번째 Integer 객체의 주소를 가지고 있다.

그러나 수정된 값이 반영되지 않는다 왜일까?

### Immutable은 수정할 수 없다

말 그대로 Immutable은 수정할 수 없기 때문이다. 그렇다면 `result = 777`은 어떻게 되는 것일까? 이는 새로운 777 Integer 객체를 생성하여 새로 생성한 객체의 주소를 result에 저장한다.

> 사실 777은 primitive int이지만 Integer형 변수에 저장하려고 하기 때문에 auto boxing으로 Integer로 변환된다.

즉, `list.get()`으로 얻은 Integer 객체에 대한 참조는 사라지고 새로운 777 객체를 `result`에 저장한다. 값의 수정은 발생하지 않는다.

이에 비해 Post는 임의로 선언한 mutable 객체로서 값의 수정이 가능하다.

다음과 같이 hashCode()를 통해 동일한 객체인지 확인할 수 있다.

```java
Integer result = numList.get(1);
int before = result.hashCode();
result = 777;
int after = result.hashCode();
System.out.println(before == after) // false

Post result = postList.get(1);
int before = result.hashCode();
result.content = "세계!";
int after = result.hashCode();
System.out.println(before == after) // true
```
