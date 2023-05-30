## Kotlin 클래스 상속

Java에서 클래스를 정의하고 이를 상속하는 방법은 다음과 같다.

```java
class MyBaseClass {
    public void myFunction() {
        System.out.println("Base class function");
    }
}

class MyDerivedClass extends MyBaseClass {
    @Override
    public void myFunction() {
        System.out.println("Derived class function");
    }
}
```

이를 Kotlin에서 다음과 같이 구현한다.

```kotlin
open class MyBaseClass {
    open fun myFunction() {
        println("Base class function")
    }
}

class MyDerivedClass : MyBaseClass() {
    override fun myFunction() {
        println("Derived class function")
    }
}
```

Java와 달리 Kotlin 클래스와 메서드는 기본적으로 `final`이다. 따라서 기본적으로는 자식 클래스가 부모 클래스를 override 할 수 없다.

이때, `open` 키워드를 부모 클래스와 부모 클래스의 메서드에 사용하면 override 할 수 있다.
