## 두 개 이상의 iterable을 평행하게 참조하기

다음과 같은 요구사항이 있다.

> N개의 노선에 대하여 북으로 갈 때는 north_lane = [...]만큼 시간이 걸리고, 남쪽으로 갈 땐 south_lane = [...]만큼 걸린다. 각 노선 중 두 거리의 합이 가장 큰 값을 구하라

나는 이 문제를 해결하기 위해 list comprehension을 사용하여 다음과 같은 코드를 작성하였다.

```python
max(n, s for n in north_lane for s in south_lane)
```

그러나 위 코드는 의도하지않은 결과를 낳았다. 잘못 사용했기 때문이다.

위 코드를 list comprehension을 사용하지 않고 작성하면 다음과 같다.

```python
tmp = []
for n in north_lane:
    for s in south_lane:
        tmp.append(n + s)
max(tmp)
```

내가 원한건 길이가 같은 서로 다른 배열에서 같은 인덱스의 값을 n과 s로서 참조하고 싶었지만 nested loop을 작성한 것이었다.

내 의도에 맞는 코드는 다음과 같다.

```python
max(n + s for n, s in zip(north_lane, south_lane))
```

### [zip()](https://docs.python.org/3/library/functions.html#zip)

zip(\*iterables, strict=false)는 Python 내장 함수로서 여러개의 iterable 객체를 매개변수로 받아 동일한 인덱스들의 값을 튜플로 묶어 반환한다. (정확하게 말해선 튜플들의 iterator를 반환)

> zip()을 다르게 생각하면 행을 열로 바꾸고 열을 행으로 바꾼다고 생각할 수 있다. 즉, 전치 행렬을 만드는데도 사용할 수 있다는 뜻이다.

> zip()은 lazy iterator로서 실제 튜플을 한 번에 생성하는 것이 아니라 반복될 때마다 그때그때 생성한다.

zip의 매개변수로 iterable 객체들을 넘겨줄 때 이들의 길이가 다를 수 있다. 이 경우 3가지로 나누어 처리한다.

- 기본값: 하나의 iterable 객체가 모두 끝나면 다른 iterable 객체들의 값이 남아있더라도 튜플 생성을 멈춘다.

- 일반적인 상황: iterable의 객체들의 길이가 모두 같을 경우 이상적인 상황으로서 모든 튜플을 생성한다. 이때 strict=True를 매개변수로 넘겨주면 iterable들의 길이가 같은 줄 알았는데 실제로 다른 경우 error를 출력할 수 있다.

- 패딩: 짧은 iterable 객체를 상수로 패딩하여 긴 iterable 객체에 맞출 수 다. 이를 위해선 `itertools.zip_longest()`를 사용해야한다.
