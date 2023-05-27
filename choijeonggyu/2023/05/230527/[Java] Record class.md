## Record class

Record class는 Java 14에 처음 등장하여 15를 거쳐 16에서 완성된 Java 문법이다.

### 목적

Record class의 목적은 다음과 같다.

- 고정된 데이터를 모델링하기 위한 클래스이다. (일반적인 클래스처럼 확장을 하려고 사용해선 안된다.)
- 반복되는 메서드를 자동으로 생성하여 이를 누락하여 발생하는 실수를 방지하고 코드 수를 줄인다.

### 특징

Record class는 다음과 같은 특징을 갖는다.

- 클래스를 선언할 때 필드를 매개변수처럼 선언
- 모든 필드는 final로 되어있어 인스턴스가 생성된 후 필드 값을 변경할 수 없음
- 모든 필드를 매개변수로 갖는 생성자를 자동으로 생성
- **필드 이름와 동일한** getter를 자동으로 생성
  - name -> `name()`
- 필드 값을 사용하는 `equals()`, `hashCode()`, `toString()`을 자동으로 생성
- final 필드가 아닌 추가 필드는 static 변수만 허용

### 사용법

Record class는 다음과 같은 모습을 가진다

```java
record 레코드클래스이름(필드){메서드}
```

게시글을 Post 클래스로 나타낼 때 제목, 내용, 작성일자를 필드로 갖는 Record class는 다음과 같다.

```java
record Post(

        Long id,
        String title,
        String content,
        LocalDateTime createdAt
) {
    static Long sequenceNumber = 0L;

    /* compact constructor */
    public Post {
        if (Objects.isNull(title)) {
            throw new IllegalArgumentException("제목은 필수입니다.");
        }
        // canonical constructor 실행
    }

    /* custom constructor */
    public Post(String title, String content) {
        this(++sequenceNumber, title, content, LocalDateTime.now());
    }

    // method
    public boolean containsTitle(String title) {
        return this.title.contains(title);
    }
}
```

compact 생성자로 canonical 생성자를 실행하기 전에 할 일을 정의할 수 있다.

> canonical constructor는 모든 필드를 매개변수로 갖는 생성자를 말한다.
