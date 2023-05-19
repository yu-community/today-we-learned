## unchecked exception vs checked exception

unchecked exception

- RuntimeException과 이를 상속하는 모든 클래스

- 에러를 발생시켜 실행 로직을 중단시키기 위함

- try로 반드시 감쌀 필요가 없음

checked exception

- unchecked exception이 아닌 exception (Exception의 상속을 받는 exception)

- 에러를 발생시키되 복구해야하는 에러일 경우

- try로 반드시 감싸야 함

- throws를 통해 해당 메서드를 호출한 코드로 에러를 넘길 수 있음. main까지 넘어갈 경우 JVM이 처리
