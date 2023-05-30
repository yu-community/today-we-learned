## Kotlin 인터페이스 구현

Java에서 인터페이스를 정의하고 이를 구현하는 방법은 다음과 같다.

```java
interface MyInterface {
    void doSomething();
}

class MyClass implements MyInterface {
    @Override
    public void doSomething() {
        System.out.println("Doing something");
    }
}
```

이를 Kotlin에서 다음과 같이 구현한다.

```kotlin
interface MyInterface {
    fun doSomething()
}

class MyClass : MyInterface {
    override fun doSomething() {
        println("Doing something")
    }
}
```
