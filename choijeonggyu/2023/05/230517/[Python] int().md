## [int()](https://docs.python.org/3/library/functions.html#int)

int(x, base=10)의 동작 원리는 은 다음과 같다.

- int()에 매개변수를 넣지 않으면 0을 반환한다.

- int()의 매개 변수가 숫자가 아니라면 반드시 기수 기반(radix base) string, bytes, bytearray 객체여야 한다. 기수는 문자열의 prefix나 base 매개 변수로 정의할 수 있다.

  > prefix: 10진수, 16진수(0x), 2진수(0b), 8진수(0o)

- int()의 매개변수로 문자열을 전달할 때 다음과 같은 기능을 추가로 제공한다.

  - +나 -로 부호를 지정할 수 있음 `int("+5")`, `int("-777")`

  - 앞이 0으로 채워질 수 있음 `int("00005")`

  - 앞뒤로 공백으로 채워질 수 있음 `int("    5     ")`

  - 자릿수 구분을 위해 underscore를 사용할 수 있음 `int("1_000_000")`
